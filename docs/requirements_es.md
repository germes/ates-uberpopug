| Requirement | Actor | Command | Data | Event |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| Таск-трекер должен быть отдельным дашбордом и доступен всем сотрудникам компании UberPopug Inc. | Account | Login to task tracker app | Account public id | Account.LoggedIn |
| Новые таски может создавать кто угодно (администратор, начальник, разработчик, менеджер и любая другая роль). У задачи должны быть описание, статус (выполнена или нет) и попуг, на которого заассайнена задача. | Account | Create task | Task | Tasks.Created |
| Менеджеры или администраторы должны иметь кнопку «заассайнить задачи», которая возьмёт все открытые задачи и рандомно заассайнит каждую на любого из сотрудников (Update: кроме менеджера и администратора) | Account with role Manager/Admin | Assign tasks | Task + Actor public ID | *Batch of events for each task*: Tasks.Assigned |
| Каждый сотрудник должен иметь возможность видеть в отдельном месте список заассайненных на него задач + отметить задачу выполненной. | Account with role Employee | Mark task as Completed | Data + Account public ID | Tasks.Completed |
| Аккаунтинг должен быть в отдельном дашборде и доступным для всех сотрудников. У обычных попугов доступ к информации о собственных счетах (аудит лог + текущий баланс). У админов и бухгалтеров должен быть доступ к общей статистике по деньгами заработанным. | Account | Login to accounting app | Account public ID | Account.LoggedIn |
| Цены на задачу определяется единоразово, в момент появления в системе (можно с минимальной задержкой) | Event Tasks.Created | Calculate prices for the task | Task public ID + prices | Tasks.PricesCalculated |
| Деньги списываются сразу после ассайна на сотрудника | Event Tasks.Assigned | Withdraw from the employee account | Account public ID, Task public ID, Sum | Accounting.Withdraw |
| Деньги начисляются после выполнения задачи | Tasks.Completed | Refill the employee account | Account public ID, Task public ID, Sum | Accounting.Refill |
| В конце дня необходимо: считать сколько денег сотрудник получил за рабочий день| System scheduler | Finish day | Account public ID + day balance | *Batch of events for each task*: Accounting.DayBalanceCalculated |
|  Положительный баланс <br/> - отправлять на почту сумму выплаты<br/> - После выплаты баланса (в конце дня) он должен обнуляться, и в аудитлоге всех операций аккаунтинга должно быть отображено, что была выплачена сумма| Event Accounting.DayBalanceCalculated | Reset current day balance and send notification | Account public ID + day balance | Accounting.DayBalancePaid |
|  Отрицательный баланс переносится на следующий день | Event Accounting.DayBalanceCalculated | Reset current day balance and set the start balance value for the next day | Account public ID + day balance | Accounting.DayBalanceReset |
| Аналитика. Нужно указывать, сколько заработал топ-менеджмент за сегодня и сколько попугов ушло в минус. | Event Accounting.DayBalanceReset | Update aggregated analytics data - income | - | Analytics.IncomeUpdated |
| Аналитика. Нужно показывать самую дорогую задачу за день, неделю или месяц. | Event Tasks.Completed | Update aggregated analytics data - expensive tasks | - | Analytics.ExpensiveTasksUpdated |


