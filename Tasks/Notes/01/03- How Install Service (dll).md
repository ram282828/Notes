
let's say you want to install `adls` service 

1. Go to [Built-in Package Repository - Octopus Deploy](http://dkcdcpadeploy01/app#/library/builtinrepository)
2. Search about `adls`
3. Right click on `download icon`, then save link as
4. download `vestas.scada.environmentalcontrol.adls.2.6.0.1`

5. Move `vestas.scada.environmentalcontrol.adls.2.6.0.1.nupkg` to another folder
6. Change the extension of the file to `.zip`
7. Run `PowerShell` as administrator
8. Go to the project path, then run `Deploy.ps1`

9. Open `Services` and find `vestas.scada.environmentalcontrol.adls` services
10. Finally make sure it is in the `Task Manager Services`