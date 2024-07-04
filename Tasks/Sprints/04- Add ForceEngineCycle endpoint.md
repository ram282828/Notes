
### Description: 

[[IC-559] [IC] Add ForceEngineCycle endpoint for Icedetectionservice - Jira (vestas.net)](https://onejira.tools.vestas.net/browse/IC-559)

In other services we have special endpoint that allows forcing (speeding up) engine cycle on backend service to speedup tests.

In normal conditions ice detection service calculates new data every 10 minutes.

In vestas.scada.environmentalcontrol.ui.webapi service add endpoint "icedetectionservice /forceenginecycle" that will call endpoint below:

In Icedetectionservice service add endpoint "`api/status/forceenginecycle`"

that will calculate data on demand.

Use case:
- Clean last 10 min data sample from db
- prepare some 10 min input data
- force calculation
- check if calculated TDeicingData result matches.

Without this endpoint we would have to wait 10 minutes

---

Pull Request:


`[C-559] add_force_engine_cycle_endpoint`

