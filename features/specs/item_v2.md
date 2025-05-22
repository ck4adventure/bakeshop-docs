 `InventoryStatusBar`, based on `Inventory` and `ParMinimum`. 

 `RefillByDate`, which is the last date a `Batch` can be made in order to have enough for the next day's `BakeQuota`. In order to know about `BakeQuotas`, the `Item` has a weekly `QuotaSchedule` where each `DayOfWeek` has the number of items to be baked for that day, called the `BakeQuota`. This displays as a slim card with abbreviated day names: Mon, Tue, Wed, Thu, Fri, Sat, Sun, and their counts below such as 0 0 12 15 12 18 15. There is an edit button to the right of the bar to open a modal with controls for each of the days of the week, submit updates all the fields at once. 

 ### Optional Active/Inactive Item Status
Active/Inactive as a flag for each item allows the system to filter items for the daily bake order list, and other things. Rules can be enforced on just active items, such as requiring a weekly quota schedule.

 ## User Stories
### Item Creation
An initial entry is made to the transaction log when an Item is created. This starts the count, default is 0. There should only be one inital entry per item in the translog. 

### Batch Creation
An entry is made everytime a new batch is submitted.
/inventory/batch
/transaction/batch