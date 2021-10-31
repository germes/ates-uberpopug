##Services and domains schema

![Services and domains schema](schema.jpg)

##Business events

| Event | Data | Producer | Consumer(s) |
| ----------- | ----------- | ----------- | ----------- |
| Tasks.Created | Task data | Task service | Accounting service |
| Tasks.Assigned | Task status<br>Assignee public ID | Task service | Accounting service |
| Tasks.Completed | Task status<br>Datetime<br>Actor public ID<br>priceCompleted | Task service | Accounting service<br>Analytics service |
| Accounting.DayBalanceCalculated | Account public ID<br>Day balance | Accounting service<br>(System scheduler) | Accounting service<br>Analytics service |
| Accounting.DayBalanceReset | Account public ID<br>Day balance | Accounting service | Analytics service |

##CUD events

| Event | Data | Producer | Consumer(s) |
| ----------- | ----------- | ----------- | ----------- |
| Tasks.Created | Task data | Task service | Accounting service |
| Tasks.Completed |  Task status<br>Datetime<br>Actor public ID<br>priceCompleted | Task service | Accounting service<br>Analytics service |
| Tasks.PricesCalculated | Public task ID<br>priceAssign<br>priceCompleted | Accounting service | Task service |
|   | Account | Login | Account |