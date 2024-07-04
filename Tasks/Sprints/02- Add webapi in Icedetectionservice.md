
### Description: 

[[IC-562] [IC] Add webapi in Icedetectionservice - Jira (vestas.net)](https://onejira.tools.vestas.net/browse/IC-562)

Repo to update: [https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice](https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice "Follow link")

- Create webapi on port 5009(http), 5019 (https)
- Add port configuration to appsettings (see reference [https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.batprotection?path=/vestas.scada.environmentalcontrol.batprotection/Appconfig.json)](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.batprotection?path=/vestas.scada.environmentalcontrol.batprotection/Appconfig.json) "Follow link") 

- property BatProtectionAddress (in this service it should be IcedetectionserviceAddress)
- Host name should be automatically updated during deployment (update deploy.ps1 script) for reference to see how to set BatProtectionAddress  look in [https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.batprotection?path=/vestas.scada.environmentalcontrol.batprotection/Deploy.ps1](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.batprotection?path=/vestas.scada.environmentalcontrol.batprotection/Deploy.ps1 "Follow link")

At the moment of writing this, there is no https implementation merged yet, it is in PR state but still it should be used as a reference: [https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.adls/pullrequest/12182](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.adls/pullrequest/12182 "Follow link")

For help please reach out [FNVJP@vestas.com.![](https://onejira.tools.vestas.net/images/icons/mail_small.gif)](mailto:FNVJP@vestas.com. "Follow link") He was implementing HTTPS in our services

----
Ports: [TCP port assignment - VOB/VOC - Consolidated SCADA - product space - https://wiki.tsw.vestas.net](https://wiki.tsw.vestas.net/pages/viewpage.action?pageId=296084014)

Pull Request: [Pull request 12406: [C-557] add_webapi - Repos (azure.com)](https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice/pullrequest/12406?_a=files)

