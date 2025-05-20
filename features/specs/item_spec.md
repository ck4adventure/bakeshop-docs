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
POST /inventory/item


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

## Actions
### First visit, empty list
Admin/Manager first visit, they won't have any items in the list. So they see the text "No active items in inventory". There is a button to add an item, and somewhere on the page a toggle to view both inactive and active items, which in this case will still be the empty list with the text and button to add item.

### Create Item
The create item button should only be available to admin and manager roles. Once the create item button is clicked, it will go to a modal with the CreateItemForm in it. 

The `CreateItemForm` Form should have `ItemName` and `ItemInitialCount`, default is zero.

Button to `SaveItem`.

### View Inventory List
With at least one Item, `InventoryCardList` has one `InventoryCard` in it. The user sees the `ItemName` and `ItemCount`.


### Inactive Items
On the Item View Page, there will be a button to mark the Item as `inactive`, which will remove it from most query results. A consideration is only allowing managers and admins to view inactive items.






