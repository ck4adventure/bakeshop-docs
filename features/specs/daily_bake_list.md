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