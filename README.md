# Microsoft Dynamics CRM

This repository contains my learning notes, examples, and practical work related to **Microsoft Dynamics CRM / Dynamics 365**.

I created this repository to document the concepts and development techniques I learned during my **IT Applications Internship**, with a focus on **Microsoft Dynamics CRM customization and development**.

---

##  About Microsoft Dynamics CRM

**Microsoft Dynamics CRM** is a Customer Relationship Management platform used to manage and organize customer-related business processes such as:

* Customers and contacts
* Sales processes
* Customer service
* Activities and communication
* Business processes and workflows
* Business data and relationships

Dynamics CRM provides a customizable platform where developers can extend the system using **C#, JavaScript, CRM SDK, Web API, FetchXML, and other tools**.

---

#  Core CRM Concepts

##  Entities

An **Entity** represents a type of business data inside CRM.

Examples:

* Account
* Contact
* Lead
* Opportunity
* Case
* Activity

Entities contain:

* **Fields** — store data
* **Forms** — allow users to view and edit records
* **Views** — display lists of records
* **Relationships** — connect entities together

### Custom Entities

Dynamics CRM also allows creating custom entities based on the business requirements.

For example:

```text
Customer
   |
   ├── Orders
   ├── Appointments
   └── Support Cases
```

---

#  Relationships

Entities can be connected using relationships.

Common relationship types include:

### One-to-Many

One record can have many related records.

```text
Account
   |
   ├── Contact
   ├── Contact
   └── Contact
```

### Many-to-Many

Multiple records can be related to multiple records.

```text
Students  <---->  Courses
```

Relationships are important for organizing CRM data and retrieving related records.

---

#  Forms

Forms provide the user interface for creating and editing CRM records.

Forms can be customized by:

* Adding/removing fields
* Organizing sections and tabs
* Making fields required
* Controlling field visibility
* Adding JavaScript logic
* Responding to form events

Common form events include:

* OnLoad
* OnChange
* OnSave

---

#  Views

Views are used to display collections of CRM records.

A view can define:

* Which columns are displayed
* Filtering conditions
* Sorting
* Related data

---

#  Business Rules

**Business Rules** allow business logic to be implemented without writing code in many situations.

They can be used to:

* Set field values
* Show or hide fields
* Make fields required
* Enable or disable fields
* Display validation messages

They are useful for implementing simple business requirements directly inside CRM.

---

#  Workflows

Workflows automate business processes.

For example:

```text
New Customer Created
        ↓
Create Follow-up Task
        ↓
Assign Task to Sales Representative
        ↓
Notify the User
```

Workflows can help reduce manual work and automate repetitive business processes.

---

#  Plugins

A **Plugin** is a custom piece of C# code that executes when a specific event occurs in Dynamics CRM.

Plugins are useful when the required business logic is more complex than what can be achieved using configuration or workflows.

A plugin can be registered for events such as:

* Create
* Update
* Delete
* Retrieve
* RetrieveMultiple

### Plugin Pipeline

A simplified CRM plugin execution flow is:

```text
Request
   ↓
Pre-Validation
   ↓
Pre-Operation
   ↓
Main Operation
   ↓
Post-Operation
```

The execution stage determines when the custom logic runs.

---

#  C# Plugin Example

A simple plugin can access the CRM execution context and organization service.

```csharp
public class CustomerPlugin : IPlugin
{
    public void Execute(IServiceProvider serviceProvider)
    {
        var context =
            (IPluginExecutionContext)serviceProvider
            .GetService(typeof(IPluginExecutionContext));

        var serviceFactory =
            (IOrganizationServiceFactory)serviceProvider
            .GetService(typeof(IOrganizationServiceFactory));

        var service =
            serviceFactory.CreateOrganizationService(context.UserId);

        // Custom business logic
    }
}
```

The plugin can use the CRM services to:

* Read records
* Create records
* Update records
* Delete records
* Retrieve related records

---

#  JavaScript Customization

JavaScript can be used to customize the behavior of CRM forms on the client side.

It can be used for:

* Form validation
* Showing/hiding fields
* Setting field values
* Making fields required
* Responding to form events
* Controlling the user experience

Example:

```javascript
function onLoad(executionContext) {
    const formContext = executionContext.getFormContext();

    const field = formContext.getAttribute("telephone1");

    if (field && !field.getValue()) {
        console.log("Phone number is empty.");
    }
}
```

JavaScript is commonly connected to form events such as:

```text
OnLoad
OnChange
OnSave
```

---

#  FetchXML

**FetchXML** is a query language used by Dynamics CRM to retrieve data.

Example:

```xml
<fetch>
    <entity name="account">
        <attribute name="name" />
        <attribute name="telephone1" />
        <filter>
            <condition
                attribute="statecode"
                operator="eq"
                value="0" />
        </filter>
    </entity>
</fetch>
```

FetchXML can be used to:

* Retrieve records
* Filter data
* Sort results
* Join related entities
* Build more complex CRM queries

---

#  OData / Web API

Dynamics 365 provides a Web API that can be accessed using **OData**.

It allows applications to communicate with CRM data using HTTP requests.

Common operations include:

```text
GET     → Retrieve data
POST    → Create data
PATCH   → Update data
DELETE  → Delete data
```

Example:

```http
GET /api/data/v9.0/accounts
```

This allows external applications and integrations to interact with Dynamics 365.

---

#  Dynamics CRM SDK

The **Dynamics CRM SDK** provides APIs and tools that allow developers to extend and interact with CRM.

Using the SDK, developers can work with CRM data programmatically.

For example:

```csharp
Entity account = new Entity("account");

account["name"] = "Example Account";

service.Create(account);
```

The SDK is especially useful when developing **C# plugins and custom CRM functionality**.

---

#  Solutions

**Solutions** are used to package and move CRM customizations between environments.

A solution can contain components such as:

* Entities
* Fields
* Forms
* Views
* Workflows
* Plugins
* JavaScript web resources
* Other customizations

A common deployment flow is:

```text
Development
     ↓
Solution
     ↓
Testing
     ↓
Production
```

Solutions help organize CRM customizations and make deployment between environments easier.

---

#  Security

Dynamics CRM provides role-based security.

Security can be controlled using:

* Users
* Teams
* Security Roles
* Business Units
* Privileges
* Access Levels

Permissions determine what users can do with CRM records.

For example:

```text
User
  ↓
Security Role
  ↓
Privileges
  ↓
Create / Read / Write / Delete
```

---

#  CRM Development Approach

When implementing a CRM requirement, I think about it in layers:

```text
Business Requirement
        ↓
CRM Configuration
        ↓
Business Rules / Workflows
        ↓
JavaScript
        ↓
Plugins / C#
        ↓
Data Queries
        ↓
Deployment using Solutions
```

The goal is to use configuration whenever possible and introduce custom code when the business requirement needs more advanced behavior.

---

#  Topics Covered

| Topic           | Description                            |
| --------------- | -------------------------------------- |
| Entities        | CRM data structures                    |
| Custom Entities | Creating business-specific data models |
| Relationships   | Connecting CRM entities                |
| Forms           | Customizing record forms               |
| Views           | Displaying and filtering records       |
| Business Rules  | Implementing simple business logic     |
| Workflows       | Automating business processes          |
| Plugins         | Server-side C# customization           |
| JavaScript      | Client-side form customization         |
| FetchXML        | Querying CRM data                      |
| OData           | Accessing CRM through Web API          |
| CRM SDK         | Programmatic CRM development           |
| Solutions       | Packaging and deploying customizations |
| Security Roles  | Managing user permissions              |




