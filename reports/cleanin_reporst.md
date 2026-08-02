## Orders Dataset

- No duplicate rows.
- All order_id values are unique.
- Date columns converted to datetime.
- Missing timestamps are mostly associated with canceled, unavailable, processing, and shipped orders.
- Missing timestamps were retained because they represent valid business scenarios.
- 166 records had carrier timestamps earlier than purchase timestamps.
- Most differences were under one hour.
- Two records showed unusually large differences (4 days and 171 days) and were flagged as potential data quality anomalies.


## Products Dataset

- No duplicate rows.
- All product_id values are unique.
- Data types are appropriate.
- 610 products have missing category and descriptive information.
- Investigation confirmed that these products were sold.
- These rows will be retained because removing them would exclude valid sales records.
- Missing categories will be treated as "Unknown" during category-based analysis if needed.


## Customers Dataset

- No duplicate rows found.
- No missing values detected.
- All `customer_id` values are unique.
- `customer_unique_id` contains repeated values.

### Investigation

The repeated `customer_unique_id` values represent returning customers. Each purchase generates a new `customer_id` while retaining the same `customer_unique_id`, indicating that the same customer has placed multiple orders.

### Cleaning Decision

- No rows were removed.
- No values were imputed.
- The repeated `customer_unique_id` values are expected and correctly represent repeat customers.
- The dataset is considered clean and ready for analysis.


## Order Items Dataset

- No duplicate rows found.
- No missing values detected.
- `order_id` values are repeated as expected because one order can contain multiple products.
- `product_id` values are repeated as expected because the same product can be purchased in multiple orders.
- `order_item_id` is not globally unique. It uniquely identifies the position of an item within a specific order and restarts for each new order.
- Date columns were converted to the appropriate datetime datatype (if applicable).

### Cleaning Decision

- No rows were removed.
- No values were imputed.
- Repeated `order_id`, `product_id`, and `order_item_id` values are expected and represent the structure of order-item relationships.
- The dataset is considered clean and ready for merging.