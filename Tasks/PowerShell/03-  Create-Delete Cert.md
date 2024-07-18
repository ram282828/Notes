
```powershell
# Create a new self-signed certificate in the MY store
$certName = "myselfsignedcert01"
$storeName = "Root"

$cert = New-SelfSignedCertificate -DnsName "localhost" -CertStoreLocation "Cert:\LocalMachine\My" -FriendlyName $certName -KeyAlgorithm RSA -KeyLength 2048 -HashAlgorithm SHA256 -NotAfter (Get-Date).AddYears(1)

# Move the certificate to the desired store
$store = New-Object System.Security.Cryptography.X509Certificates.X509Store($storeName, "LocalMachine")
$store.Open("ReadWrite")
$store.Add($cert)
$store.Close()

Write-Host "Certificate generated with thumbprint: $($cert.Thumbprint) and serial number: $($cert.SerialNumber) "
```




```powershell
# Delete the certificate
$serialNumber = "121C19101EA8E0A64DD8F8172E2B9757"
$storeName = "Root"

# Open the Root certificate store
$store = New-Object System.Security.Cryptography.X509Certificates.X509Store($storeName, "LocalMachine")
$store.Open("ReadWrite")

# Retrieve the certificate by its friendly name
$cert = $store.Certificates | Where-Object { $_.SerialNumber -eq $serialNumber }

if ($cert) {
    # Output the certificate details
    Write-Host "Certificate found with thumbprint: $($cert.Thumbprint) and serial number: $($cert.SerialNumber)"

    # Remove the certificate
    $store.Remove($cert)
    Write-Host "Certificate removed successfully."
} else {
    Write-Host "Certificate not found."
}

# Close the store
$store.Close()
```