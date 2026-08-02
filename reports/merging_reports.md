# Merge Report

## Merge 1: Customers + Orders

**Merge Key:** `customer_id`

**Join Type:** Inner Join

### Purpose

Combine customer information with order records so that each order includes customer details such as location and unique customer identifier.

### Result

| Dataset | Shape |
|---------|------:|
| Orders | (99,441, 8) |
| Customers | (99,441, 5) |
| Merged Dataset | (99,441, 12) |

### Observation

- No rows were lost during the merge.
- Every order has a matching customer record.
- Customer information (city, state, unique customer identifier) is now available for each order.



## Merge 2: Customer Orders + Order Items

**Merge Key:** `order_id`

**Join Type:** Inner Join

### Purpose

Attach purchased product information to each customer order.

### Result

| Dataset | Shape |
|---------|------:|
| Customer Orders | (99,441, 12) |
| Order Items | (112,650, 7) |
| Merged Dataset | (112,650, 18) |

### Observation

- The number of rows increased because one order can contain multiple purchased items.
- The number of unique orders decreased from **99,441** to **98,666**.
- Investigation showed that **775 orders** had no matching records in the `order_items` dataset and were therefore excluded by the inner join.
- Most excluded orders belonged to the following statuses:
  - **Unavailable:** 603
  - **Canceled:** 164
  - **Created:** 5
  - **Invoiced:** 2
  - **Shipped:** 1
- These excluded orders do not represent completed purchases, making the inner join appropriate for sales analysis.



## Merge 3: Customer Orders + Order Items + Products

**Merge Key:** `product_id`

**Join Type:** Inner Join

### Purpose

Attach product information to each purchased item, creating a complete analytical dataset.

### Result

| Dataset | Shape |
|---------|------:|
| Customer Orders + Order Items | (112,650, 18) |
| Products | (32,951, 9) |
| Final Dataset | (112,650, 26) |

### Observation

- No rows were lost during the final merge.
- Every purchased item has a matching product record.
- Products with missing category information were retained because they represent valid sales.
- The final dataset is ready for business analysis.