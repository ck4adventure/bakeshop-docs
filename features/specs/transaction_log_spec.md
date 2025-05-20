# Transaction Log (Backend Only)
Rather than have items keep track of their current inventory count in the items table via direct count updates, I want to explore where the best place is.

chatgpt suggested the inventory count as `InventoryCount = sum of all batches − sum of all pulls`. At first glance performing that query over and over wouldn't be very smart, so I asked chatgpt to explain some more about how best practice inventory management can work. I was given the `Event Sourcing` pattern, which does indeed make sense. The [Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/) has a wonderful detailed breakdown of how the design pattern works. 

To summarize, there are a defined set of possible events for inventory items such as creating a batch or baking a daily quota. Each event is recorded in an Event Store (what I would call a transaction log), along with any relevant information, such as the quantity. This becomes the authoritative source of the inventory level. One way to store the count would be through a `matierialized view`, which would perform a query operation to inform the current count for each item, which is called a `refresh`. The other popular option is to create a full table to store the current count, with `triggers` or an  to update the appropriate item when events are recorded to the transaction log. When a query comes through to get the current counts, it references the view/table rather than the event store directly. Having an event store makes the inventory count auditable, since there is a record of every change. It is more accurate, since reads and writes are separate, and the calculated count can be rebuilt. It allows for analytics and debugging, and it more scalable. 

## DB Tables for Event Store
### Transaction Log
- id, incrementing, PK
- timestampstz of event
- type of transaction: batch | dailybake | adjustment | initial
- transaction qty: -8, +100, etcn
- userID who performed the action
- function and trigger to update the product inventory table on insert

### Product Inventory Table

- item_id as PK, enforces unique intrinsically
- item_quantity, nonzero number
- timestamptz


## User Stories
### Item Creation
An initial entry is made to the transaction log when an Item is created. This starts the count, default is 0.

### Batch Creation
An entry is made everytime a new batch is submitted.
/inventory/batch
/transaction/batch