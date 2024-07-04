
### Description: 

[[IC-557] [IC] Migrate icedetectionservice to NET 6 - Jira (vestas.net)](https://onejira.tools.vestas.net/browse/IC-557)

Repo to update: [https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice](https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice "Follow link")  >> Done 
- Migrate to NET 6 framework
- Remove NSSM that is starting/registering service at the moment and implement direct service registration like in ADLS project [https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.adls](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.adls "Follow link")
    - service should be visible in task manager on its own name

This will allow automatic starting/stopping service during E2E tests

----
Similar Pull Request in ADLS: [Pull request 5447: ENVCTRL-4643-Updated to .NET 6 - Repos (azure.com)](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.adls/pullrequest/5447?_a=files)

Pull Request: [Pull request 12353: feature/migrate_icedetectionservice_to_net_6 - Repos (azure.com)](https://dev.azure.com/VestasScada/Scada/_git/icedetectionservice/pullrequest/12353?_a=files)



