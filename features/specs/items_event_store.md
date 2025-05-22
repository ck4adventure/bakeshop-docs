# Item Event Store aka Transaction Log (Backend Only)

## Design Pattern Overview
Rather than have items keep track of their current inventory count in the items table via direct count updates, I want to explore where the best place is.

chatgpt suggested the inventory count as `InventoryCount = sum of all batches − sum of all pulls`. At first glance performing that query over and over wouldn't be very smart, so I asked chatgpt to explain some more about how best practice inventory management can work. I was given the `Event Sourcing` pattern, which does indeed make sense. The [Azure Architecture Center](https://learn.microsoft.com/en-us/azure/architecture/) has a wonderful detailed breakdown of how the design pattern works. 

To summarize, there are a defined set of possible events for inventory items such as creating a batch or baking a daily quota. Each event is recorded in an Event Store (what I would call a transaction log), along with any relevant information, such as the quantity. This becomes the authoritative source of the inventory level. One way to store the count would be through a `matierialized view`, which would perform a query operation to inform the current count for each item, which is called a `refresh`. The other popular option is to create a full table to store the current count, with `triggers` or an  to update the appropriate item when events are recorded to the transaction log. When a query comes through to get the current counts, it references the view/table rather than the event store directly. Having an event store makes the inventory count auditable, since there is a record of every change. It is more accurate, since reads and writes are separate, and the calculated count can be rebuilt. It allows for analytics and debugging, and it more scalable.

## Description
This one will be called `ItemEventStore` and will be used for all bakery products created by bakers.

## Types of Events
initial -> must be non-neg (>0), set on item creation. If zero at item creation manager can set an override or create through a batch.



## DB Tables for Event Store
### Transaction Log
```sql
CREATE TABLE item_event_store (
  id SERIAL PRIMARY KEY,
  item_id REFERENCES items(id),
  quantity_change INTEGER NOT NULL,
  reason TEXT CHECK (reason IN ('batch', 'bakeoff', 'special_order', 'adjustment', 'initial')),
  created_at TIMESTAMPTZ DEFAULT now()
)
```

### Product Inventory Table
```sql
CREATE TABLE item_inventory (
  item_id INTEGER PRIMARY KEY REFERENCES items(id),
  quantity INTEGER NOT NULL
	timestamps
);
```