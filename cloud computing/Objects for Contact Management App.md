# Objects for Contact Management App

Problem Statement: Design and develop custom Application (Contact Management) using Salesforce Cloud.

---

## Objects

1. Contact Information
2. Interaction History
3. Company Details

---

## Fields and Relations

### Contact Information

1. Fields:
    - Name (Text)
    - Email (Email)
    - Phone (Phone)
    - Address (Text Area)
    - Date of Birth (Date)
    - Company (Text)
2. Relationships:
    - Contact Information to Interaction History: One-to-Many (One contact can have multiple interactions)
    - Contact Information to Company Details: Many-to-One (Multiple contacts can belong to one company)

### Interaction History

1. Fields:
    - Interaction Date (Date/Time)
    - Interaction Type (Picklist: Call, Email, Meeting, Other)
    - Notes (Long Text Area)
    - Follow-up Date (Date)
2. Relationships:
    - Lookup Relationship to Contact Information (Each interaction is related to a specific contact)

### Company Details

1. Fields:
    - Company Name (Text)
    - Industry (Picklist: Technology, Finance, Healthcare, etc.)
2. Relationships:
    - Lookup Relationship to Contact Information (A company can have multiple contacts)

---
