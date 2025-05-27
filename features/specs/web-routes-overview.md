# Top Level Pages

## Inventory
/inventory
- show list of current items
- gets items current count
- evtl will compare count against a minimum par

## Batches
/inventory/batches
- view page for all the recently created batches
- a created batch is written to the ItemEventStore which triggers count updates

## Weekly Production Schedule
/production/week/51
- shows chart of all the items currently with a schedule
- show current WeekOf
- prolly some kind of button to view daily bakeoff lists
- was gonna do a basic count update but might want to keep weekly entries

## Daily Production List
/production/day/2025-05-12
- needs a mechanism to create bakeoff lists for the upcoming week, but only once
- adding in special order counts where exist
- bakeoff marked complete, all items added to the item even store, which triggers count update for each item as well
- prolly want a view page for recent history and upcoming
- bakeoff list per baker, some unassigned, that way any things to be accomplished by a single person, like me, can be differentiated from items that get pulled from stock to pack special orders. Or the barista's get accounts to make fulfilling the special orders

## Special Orders
/production/orders
- view page for all the entered special orders
- special orders filter into the bakeoff list as well

