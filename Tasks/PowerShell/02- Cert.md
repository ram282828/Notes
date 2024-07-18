

```powershell
# Example Query

# Valid Certificate
# .\BindCertificateToPort.ps1 -storeName "Root" -serialNumber "6cd49c49cf5abfa3472fd73145244dfe" -targetPort 5019 -applicationGuid d9a31eaf-970b-43f1-a0f4-eec8ede06a8b -deleteBeforeCreating true

# Invalid / Expired Certificate
# .\BindCertificateToPort.ps1 -storeName "Root" -serialNumber "1ab8feb2298b11ab447251ac6cc5cb46" -targetPort 5019 -applicationGuid d9a31eaf-970b-43f1-a0f4-eec8ede06a8b -deleteBeforeCreating true


param ( 
    # Trusted Root Certification Authority Store
    [string]$storeName = "Root",

    # Certificate Serial Number
    [string]$serialNumber, # = "1ab8feb2298b11ab447251ac6cc5cb46"

    # Target Port Number
    [string]$targetPort, # 5023

    # Application GUID
    [string]$applicationGuid,

    # Flag to delete the certificate before creating a new one
    [switch]$deleteBeforeCreating
)

# Get the current directory
$currentDirectory = Get-Location

# Log folder
$logFolder = "Logs"

# Log File
$logFile = "certsbinding.log"

# Log Folder Path
$logFolderPath = Join-Path -Path $currentDirectory -ChildPath $logFolder

# Log File Path
$logFilePath = Join-Path -Path $logFolderPath -ChildPath $logFile

# Get the certificate from the store
$cert = Get-ChildItem -Path "Cert:\LocalMachine\$storeName" | Where-Object { $_.SerialNumber -eq $serialNumber }

# Delete the certificate if the deleteBeforeCreating flag is set
if ($deleteBeforeCreating -and $cert) {
    try {
        Remove-Item -Path "Cert:\LocalMachine\$storeName\$($cert.Thumbprint)" -Force
        $logMessage = "Certificate with serial number $serialNumber has been deleted as per the flag`n"
        Write-Host $logMessage
        Add-Content -Path $logFilePath -Value $logMessage
    } catch {
        $logMessage = "Failed to delete SSL certificate: $_"
        Write-Error $logMessage
        Add-Content -Path $logFilePath -Value $logMessage
        # Exit the script if certificate deletion fails
        exit 1
    }
    # Reset $cert variable since the certificate has been deleted
    $cert = $null
}

# Check if the certificate was found
if ($cert) {
    Write-Host "Certificate found with serial number $serialNumber in the $storeName store"
} else {
    Write-Host "No certificate found with serial number $serialNumber in the $storeName store"
    Write-Host "Creating a new self-signed certificate..."

    # Create a new self-signed certificate in the MY store
    $cert = New-SelfSignedCertificate -DnsName "localhost" -CertStoreLocation "Cert:\LocalMachine\My" -FriendlyName "NewCert" -KeyAlgorithm RSA -KeyLength 2048 -HashAlgorithm SHA256 -NotAfter (Get-Date).AddYears(1)

    # Move the certificate to the desired store
    $store = New-Object System.Security.Cryptography.X509Certificates.X509Store($storeName, "LocalMachine")
    $store.Open("ReadWrite")
    $store.Add($cert)
    $store.Close()

    # Get the serial number of the new certificate
    $serialNumber = $cert.SerialNumber
    Write-Host "New certificate created with serial number $serialNumber and moved to $storeName store"
}

# Get the certificate thumbprint
$thumbprint = $cert.Thumbprint

# Unbind the target port from any previous binding
try {
    $params_del = "netsh http delete sslcert ipport=0.0.0.0:$targetPort"
    cmd.exe /c $params_del --%

    $logMessage = "Port at $targetPort tied to application $applicationGuid has been unbound`n"
    Write-Host $logMessage
    Add-Content -Path $logFilePath -Value $logMessage
} catch {
    $logMessage = "Failed to unbind SSL certificate: $_"
    Write-Error $logMessage
    Add-Content -Path $logFilePath -Value $logMessage
}

# Bind the target port using the found certificate and the application to use it.
try {
    $params_add = "netsh http add sslcert ipport=0.0.0.0:$targetPort certhash=$thumbprint appid={$applicationGuid}"
    cmd.exe /c $params_add --%

    $logMessage = "Port at $targetPort tied to application $applicationGuid has been bound to certificate with serial number $serialNumber`n"
    Write-Host $logMessage
    Add-Content -Path $logFilePath -Value $logMessage
} catch {
    $logMessage = "Failed to bind SSL certificate: $_"
    Write-Error $logMessage
    Add-Content -Path $logFilePath -Value $logMessage
}


	```