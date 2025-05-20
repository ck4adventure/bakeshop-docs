# Special Orders
Under consideration is setting up a special orders table to track each amount as it comes in. 

###
```sql
CREATE TABLE special_orders (
  id SERIAL PRIMARY KEY,
  product_id INTEGER NOT NULL REFERENCES products(id) ON DELETE CASCADE,
  quantity INTEGER NOT NULL CHECK (quantity > 0),
  bake_date DATE NOT NULL,
  customer_name TEXT,
  notes TEXT
);
```