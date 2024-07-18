
### Description: 

[[IC-680] No ice control database configuration snapshot - Jira (vestas.net)](https://onejira.tools.vestas.net/browse/IC-680)

When any of marked fields changes in UI, we should create new rows in db instead of updating current rows.

Tables:
```
select * from TDeIcingConfiguration
select * from TParkUnit_TDeIcingConfiguration
select * from TDeIcingTrigger
select * from TDeIcingTriggerConfiguration
```


TDeIcingConfiguration -> new row should have flad ConfigurationEnabled = 1 and update other and set to ConfigurationEnabled = 0

TDeIcingTriggerConfiguration   
TDeIcingTrigger   
TParkUnit_TDeIcingConfiguration 

If any trigger threashold value changes on UI we should create all 8 rows in TDeIcingTriggerConfiguration + TDeIcingTrigger with [DeIcingTriggerEnabled] = 1(set other TDeIcingTrigger  to 0  
+new row in TDeIcingConfiguration 

If any TParkUnit_TDeIcingConfiguration changes then create a copy of all rows that points to same TDeIcingConfiguration   
+new row in TDeIcingConfiguration 

Repo: [https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.icecontrol](https://dev.azure.com/VestasScada/Scada/_git/vestas.scada.environmentalcontrol.icecontrol)

------

Endpoint: 
```c#
        [HttpPost]
        [ActionName("savesystemconfiguration")]
        //[Authorize(Roles = AuthorizationConstants.EcUiSettingsRole)]
        public async Task<HttpResponseMessage> SaveSystemConfiguration(
            [FromBody] ConfigChangeDto<IceControlPlantConfigurationDto> systemConfig)
        {

            var update = new UIUpdate {SystemConfig = systemConfig};
            return await this.ProcessHttpRequest(_logger, _configuration.UpdateConfiguration, update);
        }
```


```sql 

select * from TDeIcingConfiguration
select * from TParkUnit_TDeIcingConfiguration

select * from TDeIcingTrigger
select * from TDeIcingTriggerConfiguration

select * from TParkUnit



select top 10 * from TDeIcingData where parkunitid = 2 order by 1 desc
select * from TDeIcingStagingData
```