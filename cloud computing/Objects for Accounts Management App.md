# Objects for Accounts Management App

Problem Statement: Design and develop custom Application (Accounts Management) using Salesforce Cloud.

---

## Objects

1. Account Details
2. Contact Details
3. Activity Information
4. Case Information

---

## Fields and Relations

### Account Details

1. Fields:
    - Account Name (Text)
    - Account Type (Picklist: Customer, Partner, Vendor, etc.)
    - Industry (Picklist: Technology, Finance, Healthcare, etc.)
    - Phone (Phone)
    - Address (Address)
2. Relationships:
		Account Details to Contact Details: One-to-Many (One Account can have multiple Contacts)
		Account Details to Activity Information: One-to-Many (One Account can have multiple Activities)
    Account Details to Case Information: One-to-Many (One Account can have multiple Cases)

### Contact Details

1. Fields:
    - Name (Text)
    - Email (Email)
    - Phone (Phone)
    - Job Title (Text)
    - Account (Lookup to Account)
2. Relationships:
    - Contact Details to Activity Information: One-to-Many (One Contact can have multiple Activities)
    - Contact Details to Case Information: One-to-Many (One Contact can have multiple Cases)

### Activity Information

1. Fields:
    - Subject (Text)
    - Account (Lookup to Account)
    - Contact (Lookup to Contact)
    - Activity Type (Picklist: Call, Meeting, Email, Task)
    - Due Date (Date)
    - Status (Picklist: Not Started, In Progress, Completed)
    - Notes (Long Text Area)

### Case Information

1. Fields:
    - Case Number (Auto Number)
    - Account (Lookup to Account)
    - Contact (Lookup to Contact)
    - Status (Picklist: New, In Progress, Escalated, Closed)
    - Priority (Picklist: Low, Medium, High)
    - Description (Long Text Area)
    - Created Date (Date/Time)
    - Last Modified Date (Date/Time)

---
