# Inventory

### As a baker, I want to be able to view a page showing my CurrentInventory, so that I don't have to open any freezer doors.

Mobile View is a `scrolling list of mini-cards` with `Name` and `InventoryCount` of each `Item`. There would be a color-coded `InventoryStatusBar`, maybe even can choose different styles of left, bottom, or whole card. Green would indicate there was at least `ParMinimum` count of items in stock. Orange would indicate less than `ParMinimum` items were in stock, but not completely out yet. Red would indicate there weren't enough for the next day's `bake quota`. Darkred/Black indicates zero items in stock. Might even fit in the date that stock will run out, for planning purposes.

### As a baker, I want to see the InventoryPage for an Item
Clicking/tapping an `item card` takes the user to a `item view page`. It lists `Name`, `InventoryCount` and it's corresponding `InventoryStatusBar` and shows the `RefillByDate`, which is the last date a `Batch` can be made in order to have enough for the next day's `BakeQuota`. In order to know about `BakeQuotas`, the `Item` has a weekly `QuotaSchedule` where each `DayOfWeek` has the number of items to be baked for that day, called the `BakeQuota`. This displays as a slim card with abbreviated day names: Mon, Tue, Wed, Thu, Fri, Sat, Sun, and their counts below such as 0 0 12 15 12 18 15. There is an edit button to the right of the bar to open a modal with controls for each of the days of the week, submit updates all the fields at once. 

A `BakeCalendar` can be built on query to project out the daily bakes, paying special attention to finding the `ParMinimumDate` and `ZeroItemsDate`. Could eventually use the calendar for other things, such as reminders.

Below all that would be a `BakedownChart` showing the expected `InventoryCount` for each day, again visually highlighting when the stock count reaches the `ParMinimum`, `DailyBakeQuota`, `ZeroItems`, etc.


# Weekly Quota Schedule
A quota schdule is an object with the days of the week and the scheduled count for each day. This displays as a slim card with abbreviated day names: Mon, Tue, Wed, Thu, Fri, Sat, Sun, and their counts below such as 0 0 12 15 12 18 15. The daily counts are used in the `ProjectedInventoryLog`, which in turn informs the p`ProjectedInventoryCounts`. 

## Creating a Quota Schedule
On adding an item the manager can specify a bake schedule. Form with fields for each day of the week and the expected count for each as a number counter. Save or cancel buttons

### Optional Active/Inactive Item Status
Active/Inactive as a flag for each item allows the system to filter items for the daily bake order list, and other things. Rules can be enforced on just active items, such as requiring a weekly quota schedule.

## As a manager, I want to override the scheduled daily bake quota with a different number
Usually it is to bake less than the scheduled quota, but also sometimes more. This could be a holiday, general uptick in sales or better than expected sales in some way. This number cannot be changed by the manager once the baker marks it complete.



# Today's Bake Order

## As a baker, I want to view the daily bake order
A top level menu item, the mobile view of the `TodaysBakesPage` is a scrollable list of cards of all the inventory items that are currently active, along with their total bake count for that particular day. "Chocolate Chip Cookies: 24", "Orange Scones: 15". Same color bar warnings can be used here, red if not enough for that quota, and black if zero items. Optional details could include freezer location. The `TotalBakeCount` is the sum of the scheduled bake quota and the `SpecialOrderCount` for that day.

### As a baker, I want to mark an item as pulled / complete
I pull the scheduled amount for each item and line them up for either preparation or set them as ready to bake in the racks. This effectively takes it out of inventory and deems it no longer usable. It's status can now only become sold or lost. 

Tapping a specific item card in the list will trigger a confirmation modal to mark the item as complete. Once the user confirms it, the transaction log is updated with the item and how many. 

### As a baker, I want to be able to hit the Undo Button and mark a DailyBake Item as not complete
Basically an undo button to unmark an item as complete. Should have a ConfirmationModal.

### As a baker, I want to be able to override the total count
Maybe I dropped a focaccia or burnt a sheet of cookies, I might need to add more to the baked/pulled count. Or possible there was less stock in the freezer than expected. When viewing the `ConfirmationModal` to mark an Item as Pulled, there is an increment counter to update the count. This might be something to flag in the user transaction logs to track who changes what, same for a manager upping a DailyBakeCount or any other override.

## As a baker, I want to Preview an upcoming day's bake order
Requires some kind of Weekly/Monthly Calendar view page to choose which day's order to view. 

No updates to counts allowed by a baker to a bake order.

## As a manager I want to add a special order to a Day's Bake Order
`Special Order` adds to the `ProjectedBakesLog` of bakes, and eventually the `TransactionLog` when the days order is marked complete. 

Might want to keep the `ProjectedBakesLog` entries in place to be able to track expected vs actual?

When viewing the Daily Order Page, there is a list of items and their counts. There could be a `+` button at the  bottom, which could use the same ChooserList of ActiveItems to this time add a SpecialOrder. A popup modal with the Item Name and count, this time defaulting to 1. Date, time and user is logged as well.  




# Batches
An `Item`'s `InventoryCount` is to be increased through the creation of a `Batch`. A `Batch` for a given item has the `ExpectedBatchCount`(s) of how many the recipe should make for an item, and the `ActualBatchCount` of how many to update the inventory by. 

## As a user, I log that I have created a Batch
If starting from the `InventoryListPage`, there will be a large `+` button, probably lower right, to indicate adding a batch to increase inventory. 

If starting from the `ItemViewPage`, there will be a button up top somewhere by the `ItemName` to `Add a Batch`, as well as the similar `+` button floating in the bottom right.

If starting from the `+`, an initial `ItemChooserModal` will appear listing all the items that are currently active. The user selects an inventory item.

If starting from ItemViewPage, or after selecting an Item from the `ItemChooserModal`, the User sees the `AddBatchModal` listing the `ItemName`, the `ExpectedBatchCount` within a number chooser field with the ability to input a new qty or use the up down arrows to increment the `ActualBatchCount`. Eventually, there might be `BatchNotes` to track issues. There are Save and Cancel buttons. Once Save is clicked, a `ConfirmationModal` appears just to make sure batch counts don't accidentally get added. This is logged in the `TransactionLog` as a batch with the itemid, actual count, date and time. 

Once a Batch has been saved to the transaction log, the current count for the item is updated, and the projected inventory counts calendar needs to be updated in order to have the chart accurately reflect the MinPar and other bakedown dates.
