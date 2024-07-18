
```cs

namespace vestas.scada.environmentalcontrol.icecontrol
{
    public static class LoggerInDB
    {
        public static void Logger(string msg)
        {
            using (var sqlConnection = new SqlConnProxy(DbConnection.GetWindmanDbConnection()))
            {
                sqlConnection.Open();

                sqlConnection.Execute($"insert into [AALoger] ([text]) values ('{msg}')");
            }

        }
    }
}


            System.Text.StringBuilder @string = new System.Text.StringBuilder();
            @string.Append($"Called from ({nameof(UpdatePlantSystemConfiguration)}) function at ({DateTime.Now}):");
            @string.Append(System.Text.Json.JsonSerializer.Serialize(sysConfig, new System.Text.Json.JsonSerializerOptions { WriteIndented = true }));
            LoggerInDB.Logger(@string.ToString());

```



```sql 

select * from [dbo].[AALoger]
delete from [dbo].[AALoger]

```