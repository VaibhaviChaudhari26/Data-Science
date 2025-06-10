# Objects for Online Shopping App

Problem Statement: Design and develop custom Application (Online Shopping) using Salesforce Cloud.

---

## Objects

1. Online Product
2. Product Category
3. Customer Details
4. Order Details 

---

## Fields and Relations

### Online Product

1. Fields:
    - Product Name (Text)
    - Description (Long Text)
    - Price (Currency)
    - Stock Quantity (Number)
    - Product Category (Picklist)
2. Relationships:
    - Related to Product Category (Many-to-One)

### Product Category

1. Fields:
    - Category Name (Text/Picklist)
2. Relationships:
    - Related to Online Product (One-to-Many)

### Customer Details

1. Fields:
    - Name (Text)
    - Email (Email)
    - Phone Number (Phone)
    - Address (Text Area)
2. Relationships:
    - Related to Orders Details (One-to-Many)

### Order Details

1. Fields:
    - Order Number (Auto-Number)
    - Order Date (Date/Time)
    - Total Amount (Currency)
    - Status (Picklist: Pending, Shipped, Delivered, Cancelled)
2. Relationships:
    - Related to Customer Details (Many-to-One)

---
