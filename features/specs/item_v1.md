# Item v1

## Description
A bakery item is the base unit of our inventroy control features. Initial feature is just maintaining a name and count, with a form to create a new item. 


## Roles
- Admin
- Manager
- Baker

## Routes

### Mobile App
- /inventory, list of cards, each an item
- Modal `CreateItemForm` 

### Web
- /inventory, list of cards, each an item
- Modal `CreateItemForm` 

### API
GET  /inventory/items, returns a list of active items and their current counts
GET /inventory/create, returns the `CreateItemForm`
POST /inventory/item, sends the item to the db for saving


## Web Components
InventoryEmptyVIew
- "No active items in inventory. Click to add an item."
- CreateItemButton
- ListToggleInactiveItems
CreateItemForm
- item name
- current inventory incrementer, default is 0
- SaveItem Button
- Cancel Button

InventoryListView
- InventoryItemCard
  -- ItemName
  -- ItemCount
  -- ItemInventoryStatus: above par, at par, min par, nextday, zero

## DB Schemas Used

### Item
- id, PK, incrementing
- name, varchar, unique
- active, bool, default true

```sql
-- Product catalog
CREATE TABLE items (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL,
	active BOOLEAN DEFAULT TRUE
);
```

## Actions
### First visit, empty list
Admin/Manager first visit, they won't have any items in the list. So they see the text "No active items in inventory". There is a button to add an item, and somewhere on the page a toggle to view both inactive and active items, can either disable the button or show the empty list with the text and button to add item.

### Create Item
The create item button should only be available to admin and manager roles. Once the create item button is clicked, it will go to a modal with the CreateItemForm in it. 

The `CreateItemForm` Form should have `ItemName` and `ItemInitialCount`, default is zero.
Button to `SaveItem`, which POSTS item, db writes it to item and writes the count in the ItemActionStore as the initial inventory count.

User is redirected to the `InventoryPage` after successful creation.

#### OPTIONAL Save and Add Another Button in Modal

### As a baker, I want to be able to view a page showing my CurrentInventory, so that I don't have to open any freezer doors.

Mobile View is a `scrolling list of mini-cards` with `Name` and `InventoryCount` of each `Item`. There would be a color-coded `InventoryStatusBar`, maybe even can choose different styles of left, bottom, or whole card. Green would indicate there was at least `ParMinimum` count of items in stock. Orange would indicate less than `ParMinimum` items were in stock, but not completely out yet. Red would indicate there weren't enough for the next day's `bake quota`. Darkred/Black indicates zero items in stock. Might even fit in the date that stock will run out, for planning purposes.

### Inactive Items
By default the `InventoryPage` will not show inactive items, this can be toggled with a switch somewhere. Once all items are displayed, the desired item can be selected/clicked/tapped and open it's `ItemDetailPage`.

On the `ItemDetailPage`, there will be a toggle button to mark the Item as `inactive`, which will remove it from most query results. A consideration is only allowing managers and admins to view inactive items. The same button will toggle the item back to `active`. A confirmation modal should be used to remind user to set a weekly schedule.

### As a baker, I want to see the InventoryPage for an Item
Clicking/tapping an `item card` takes the user to a `item view page`. It lists `Name`, `InventoryCount`. 











