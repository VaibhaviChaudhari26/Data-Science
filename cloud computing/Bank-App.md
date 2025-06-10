# Bank Application using Apex

Problem Statement: Create Bank application in SalesForce.com using Apex programming Language.

- [Method 1 (Create Visual App)](#method-1)
- [Method 2 (Execution Window)](#method-2)
- [Video Instructions](https://git.kska.io/sppu-te-comp-content/CloudComputing/src/branch/main/Practical/Assignment-3/Bank-App-Demo.mp4)

---

## Method 1

1. In the Developer Console, after creating a new `Apex Class` with the name `CreateBankCustomer`, paste the below code:

> [!IMPORTANT]
> Remove all the existing stuff from the file before pasting.

```java
public class CreateBankCustomer {
    public String customerName { get; set; }
    public String contactNumber { get; set; }
    public String customerSegment { get; set; }
    public String accountNumber { get; set; }
    public String accountType { get; set; }

    public List<SelectOption> segmentOptions { get; set; }
    public List<SelectOption> accountTypeOptions { get; set; }

    public CreateBankCustomer(ApexPages.StandardController controller) {
        segmentOptions = new List<SelectOption>();
        segmentOptions.add(new SelectOption('', '- None -'));
        segmentOptions.add(new SelectOption('Retail Banking', 'Retail Banking'));
        segmentOptions.add(new SelectOption('Corporate Banking', 'Corporate Banking'));
        segmentOptions.add(new SelectOption('Private Banking', 'Private Banking'));
        segmentOptions.add(new SelectOption('Investment Banking', 'Investment Banking'));

        accountTypeOptions = new List<SelectOption>();
        accountTypeOptions.add(new SelectOption('', '- None -'));
        accountTypeOptions.add(new SelectOption('Savings', 'Savings'));
        accountTypeOptions.add(new SelectOption('Current', 'Current'));
    }

    public PageReference createCustomer() {
        System.debug('Creating new bank customer');
        if (!String.isEmpty(customerName)) {
            Account customer = new Account(
                Name = customerName,
                Phone = contactNumber,
                Industry = customerSegment,
                AccountNumber = accountNumber,
                Type = accountType
            );
            insert customer;
            PageReference pg = new PageReference('/' + customer.Id);
            pg.setRedirect(true);
            return pg;
        } else {
            ApexPages.addMessage(new ApexPages.Message(ApexPages.Severity.ERROR, 'Please enter Customer Name'));
        }
        return null;
    }

    public PageReference cancelCreation() {
        return new PageReference('/' + Schema.SObjectType.Account.getKeyPrefix() + '/o');
    }
}
```

2. In top-left corner, click on `File` followed by `Save` to save this file.

3. In top-left corner, click on `File`, then `New -> Visualforce Page` and create a new Apex Page titled `CreateBankCustomer`. Then, paste the following code:

> [!IMPORTANT]
> Remove all the existing stuff from the file before pasting.

```xml
<apex:page standardController="Account" extensions="CreateBankCustomer">
    <apex:form>
        <apex:pageMessages />
        <apex:pageBlock title="Create Bank Customer">
            <apex:pageBlockSection columns="1">
                <apex:inputText value="{!customerName}" label="Customer Name"/>
                <apex:inputText value="{!contactNumber}" label="Contact Number"/>
                <apex:inputText value="{!accountNumber}" label="Account Number"/>
                <apex:selectList value="{!accountType}" size="1" label="Account Type">
                    <apex:selectOptions value="{!accountTypeOptions}" />
                </apex:selectList>
                <apex:selectList value="{!customerSegment}" size="1" label="Customer Segment">
                    <apex:selectOptions value="{!segmentOptions}"/>
                </apex:selectList>
            </apex:pageBlockSection>
            <apex:pageBlockButtons >
                <apex:commandButton value="Create" action="{!createCustomer}" />
                <apex:commandButton value="Cancel" action="{!cancelCreation}" />
            </apex:pageBlockButtons>
        </apex:pageBlock>
    </apex:form>
</apex:page>
```

4. In top-left corner, click on `File` followed by `Save` to save this file.


5. In top-left corner, right above the line numbers, click on `Preview` button. A new browser tab will open. Enter the required details and click on `Create` to create a new user.

> [!TIP]
> Visit `Accounts` section from App Launcher to view the changes.

---

## Method 2

1. In the Developer Console, after creating a new `Apex Class` with the name `User`, paste the below code:

> [!IMPORTANT]
> Remove all the existing stuff from the file before pasting.

```java
public class User {
public static void createAccount(String accName, String accType) {
Account newAcc = new Account();
newAcc.Name = accName;
newAcc.Type = accType; // Use the standard Type field

    try {
        insert newAcc;
        System.debug('Account created with id: ' + newAcc.Id);
    } catch (DmlException e) {
        System.debug('Error creating Account: ' + e.getMessage());
    }
}

 public static void deleteAccount(Id accId) {
    // Check if the account ID is valid
    if (accId == null) {
        System.debug('Account Id cannot be null');
        return;
    }
    
    try {
        // Perform the delete operation
        delete [SELECT Id FROM Account WHERE Id = :accId LIMIT 1];
        System.debug('Account with ID: ' + accId + ' has been deleted.');
    } catch (DmlException e) {
        System.debug('Error deleting Account: ' + e.getMessage());
    } catch (QueryException e) {
        System.debug('Error finding Account: ' + e.getMessage());
    }
}

}
```

2. In top-left corner, click on `File` followed by `Save` to save this file.

3. Press `Ctrl+E` to open execute anonymous window.

4. Paste the below content and hit `Execute`.

```java
User.createAccount('Test Account', 'Savings);
User.deleteAccount('#specified_Id');

// Id can be checked in URL when clicked on any account created in Accounts Page
```

> [!TIP]
> Visit `Accounts` section from App Launcher to view the changes.

> [!NOTE]
> For account deletion, you have to do it directly from the `Accounts` section in App Launcher.

---
