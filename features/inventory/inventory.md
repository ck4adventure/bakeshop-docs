# Inventory

### As a baker, I want to be able to view a page showing my CurrentInventory, so that I don't have to open any freezer doors.

Mobile View is a `scrolling list of mini-cards` with `Name` and `InventoryCount` of each `Item`. There would be a color-coded `InventoryStatusBar`, maybe even can choose different styles of left, bottom, or whole card. Green would indicate there was at least `ParMinimum` count of items in stock. Orange would indicate less than `ParMinimum` items were in stock, but not completely out yet. Red would indicate there weren't enough for the next day's `bake quota`. Darkred/Black indicates zero items in stock. Might even fit in the date that stock will run out, for planning purposes.

### As a baker, I want to see the InventoryPage for an Item
Clicking/tapping an `item card` takes the user to a `item view page`. It lists `Name`, `InventoryCount` and it's corresponding `InventoryStatusBar` and shows the `RefillByDate`, which is the last date a `Batch` can be made in order to have enough for the next day's `BakeQuota`. In order to know about `BakeQuotas`, the `Item` has a weekly `QuotaSchedule` where each `DayOfWeek` has the number of items to be baked for that day, called the `BakeQuota`. This displays as a slim card with abbreviated day names: Mon, Tue, Wed, Thu, Fri, Sat, Sun, and their counts below such as 0 0 12 15 12 18 15. There is an edit button to the right of the bar to open a modal with controls for each of the days of the week, submit updates all the fields at once. 

A `BakeCalendar` can be built on query to project out the daily bakes, paying special attention to finding the `ParMinimumDate` and `ZeroItemsDate`. Could eventually use the calendar for other things, such as reminders.

Below all that would be a `BakedownChart` showing the expected `InventoryCount` for each day, again visually highlighting when the stock count reaches the `ParMinimum`, `DailyBakeQuota`, `ZeroItems`, etc.