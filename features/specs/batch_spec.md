# Batches

## Description
Batches are the execution of a specific recipe to create a real quantity of items. For example, a batch of chocolate chip cookies may make 96 cookies. 

## Roles
Admin
Manager
Baker

## Routes
POST /inventory type=batch

## Web Components
CreateBatchModal
- item name
- number incrementer field
- save / cancel buttons

## User Stories
### As a baker/manager/admin, I log that I have created a Batch
If starting from the `InventoryListPage`, there will be a large `+` button, probably lower right, to indicate adding a batch to increase inventory. 

If starting from the `ItemViewPage`, there will be a button up top somewhere by the `ItemName` to `Add a Batch`, as well as the similar `+` button floating in the bottom right.

If starting from the `+`, an initial `ItemChooserModal` will appear listing all the items that are currently active. The user selects an inventory item.

If starting from ItemViewPage, or after selecting an Item from the `ItemChooserModal`, the User sees the `AddBatchModal` listing the `ItemName`, the `ExpectedBatchCount` within a number chooser field with the ability to input a new qty or use the up down arrows to increment the `ActualBatchCount`. Eventually, there might be `BatchNotes` to track issues. There are Save and Cancel buttons. Once Save is clicked, a `ConfirmationModal` appears just to make sure batch counts don't accidentally get added. This is logged in the `TransactionLog` as a batch with the itemid, actual count, date and time. 

Once a Batch has been saved to the transaction log, the current count for the item is updated, and the projected inventory counts calendar needs to be updated in order to have the chart accurately reflect the MinPar and other bakedown dates.