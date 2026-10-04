Microsoft Dynamics CRM

This repository contains my learning notes, examples, and practical work related to Microsoft Dynamics CRM / Dynamics 365.

I created this repository to document the concepts and development techniques I learned during my IT Applications Internship, with a focus on Microsoft Dynamics CRM customization, development, business processes, and software development practices.

---

About Microsoft Dynamics CRM

Microsoft Dynamics CRM is a Customer Relationship Management platform used to manage and organize customer-related business processes such as:

* Customers and contacts
* Sales processes
* Marketing activities
* Customer service
* Activities and communication
* Business processes and workflows
* Business data and relationships

Dynamics CRM provides a customizable platform where developers can extend the system using C#, JavaScript, CRM SDK, Web API, FetchXML, and other tools.

---

CRM Business Areas

CRM systems support different areas of a business.

Sales

CRM helps organizations manage the sales process, from potential customers to completed deals.

Marketing

CRM can be used to manage marketing activities, campaigns, customer engagement, and related processes.

Customer Service

CRM supports customer service operations such as managing cases, customer requests, activities, and support interactions.

---

Sales Cycle

The Sales Cycle represents the stages a potential customer goes through during the sales process.

A simplified sales cycle can be represented as:

Lead
  ↓
Qualification
  ↓
Opportunity
  ↓
Proposal / Quote
  ↓
Order
  ↓
Customer

CRM helps organizations track and manage these stages and maintain customer-related information throughout the process.

---

CRM Environments

CRM development and customizations can be managed across different environments.

Development
      ↓
Staging
      ↓
Production

Development

Used for developing and testing customizations before they are released.

Staging

Used to validate and test changes before moving them to the live environment.

Production

The live environment where the CRM system is used by the organization.

Separating environments helps reduce the risk of introducing untested changes into the production system.

---

CRM Customization

Dynamics CRM can be customized to meet specific business requirements.

Customization can include:

* Entities
* Fields
* Forms
* Views
* Relationships
* Business Rules
* Workflows
* Dialogs
* JavaScript
* Plugins
* Solutions

The goal is to use built-in CRM configuration whenever possible and introduce custom development when more advanced behavior is required.

---

Core CRM Concepts

Entities

An Entity represents a type of business data inside CRM.

Examples:

* Account
* Contact
* Lead
* Opportunity
* Case
* Activity

Entities contain:

* Fields — store data
* Forms — allow users to view and edit records
* Views — display lists of records
* Relationships — connect entities together

Custom Entities

Dynamics CRM also allows creating custom entities based on business requirements.

For example:

Customer
   |
   ├── Orders
   ├── Appointments
   └── Support Cases

---

Fields

Fields are used to store information inside CRM entities.

Common field types include:

* Text
* Number
* Currency
* Date and Time
* Boolean
* Lookup
* Option Set

Fields can be configured according to the requirements of the business process.

---

Relationships

Entities can be connected using relationships.

Common relationship types include:

One-to-Many

One record can have many related records.

Account
   |
   ├── Contact
   ├── Contact
   └── Contact

Many-to-Many

Multiple records can be related to multiple records.

Students  <---->  Courses

Relationships are important for organizing CRM data and retrieving related records.

---

Forms

Forms provide the user interface for creating and editing CRM records.

Forms can be customized by:

* Adding or removing fields
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

Views

Views are used to display collections of CRM records.

A view can define:

* Which columns are displayed
* Filtering conditions
* Sorting
* Related data

Views help users quickly find and work with relevant CRM records.

---

Business Rules

Business Rules allow business logic to be implemented without writing code in many situations.

They can be used to:

* Set field values
* Show or hide fields
* Make fields required
* Enable or disable fields
* Display validation messages

Business Rules are useful for implementing simple business requirements directly inside CRM.

---

Business Process Management

Business Process Management (BPM) focuses on designing, managing, and improving business processes.

During the internship, I gained exposure to BPM tools and portals used to work with business processes.

BPM Portals

The BPM tools included:

* Process Admin
* Inspector
* Portal
* Designer

These tools provide different capabilities for managing, inspecting, designing, and working with business processes.

---

Workflows

Workflows automate business processes and repetitive tasks.

For example:

New Customer Created
        ↓
Create Follow-up Task
        ↓
Assign Task to Sales Representative
        ↓
Notify the User

Workflows can help reduce manual work and automate repetitive business processes.

---

Dialogs

Dialogs provide guided and interactive processes that can help users complete predefined business tasks.

They can be used to:

* Guide users through a sequence of steps
* Ask users for information
* Collect required data
* Support predefined business processes

---

Plugins

A Plugin is a custom piece of C# code that executes when a specific event occurs in Dynamics CRM.

Plugins are useful when the required business logic is more complex than what can be achieved using configuration or workflows.

A plugin can be registered for events such as:

* Create
* Update
* Delete
* Retrieve
* RetrieveMultiple

Plugin Pipeline

A simplified CRM plugin execution flow is:

Request
   ↓
Pre-Validation
   ↓
Pre-Operation
   ↓
Main Operation
   ↓
Post-Operation

The execution stage determines when the custom logic runs.

---

C# Plugin Example

A simple plugin can access the CRM execution context and organization service.

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

The plugin can use CRM services to:

* Read records
* Create records
* Update records
* Delete records
* Retrieve related records

---

Development Tools

CRM development can involve several development and administration tools.

Visual Studio and .NET Framework

Visual Studio can be used to develop custom CRM functionality, especially C# plugins and other .NET-based components.

The internship included working with:

* Visual Studio
* .NET Framework
* C# development
* CRM development projects

---

JavaScript Customization

JavaScript can be used to customize the behavior of CRM forms on the client side.

It can be used for:

* Form validation
* Showing or hiding fields
* Setting field values
* Making fields required
* Responding to form events
* Controlling the user experience

Example:

function onLoad(executionContext) {
    const formContext = executionContext.getFormContext();

    const field = formContext.getAttribute("telephone1");

    if (field && !field.getValue()) {
        console.log("Phone number is empty.");
    }
}

JavaScript is commonly connected to form events such as:

OnLoad
OnChange
OnSave

---

XrmToolBox

XrmToolBox is a collection of tools that can be used to assist with Dynamics CRM administration, customization, development, and troubleshooting.

It provides utilities that can make common CRM development and administration tasks easier.

---

FetchXML

FetchXML is a query language used by Dynamics CRM to retrieve data.

Example:

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

FetchXML can be used to:

* Retrieve records
* Filter data
* Sort results
* Join related entities
* Build more complex CRM queries

---

OData / Web API

Dynamics 365 provides a Web API that can be accessed using OData.

It allows applications to communicate with CRM data using HTTP requests.

Common operations include:

GET     → Retrieve data
POST    → Create data
PATCH   → Update data
DELETE  → Delete data

Example:

GET /api/data/v9.0/accounts

This allows external applications and integrations to interact with Dynamics 365.

---

Dynamics CRM SDK

The Dynamics CRM SDK provides APIs and tools that allow developers to extend and interact with CRM.

Using the SDK, developers can work with CRM data programmatically.

For example:

Entity account = new Entity("account");

account["name"] = "Example Account";

service.Create(account);

The SDK is especially useful when developing C# plugins and custom CRM functionality.

---

Solutions

Solutions are used to package and move CRM customizations between environments.

A solution can contain components such as:

* Entities
* Fields
* Forms
* Views
* Workflows
* Plugins
* JavaScript web resources
* Other customizations

Creating a Solution

A typical customization process can be represented as:

Create Solution
      ↓
Create Entity
      ↓
Add Fields
      ↓
Configure Forms / Views
      ↓
Add Custom Logic
      ↓
Test
      ↓
Deploy

A common deployment flow is:

Development
     ↓
Solution
     ↓
Staging / Testing
     ↓
Production

Solutions help organize CRM customizations and make deployment between environments easier.

---

Security

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

User
  ↓
Security Role
  ↓
Privileges
  ↓
Create / Read / Write / Delete

---

Support and Ticket Management

Technical support and issue management are important parts of IT operations.

During the internship, I worked with ManageEngine as a support and ticket management tool.

A typical support workflow can be represented as:

Issue Reported
      ↓
Ticket Created
      ↓
Issue Analysis
      ↓
Troubleshooting
      ↓
Resolution
      ↓
Ticket Closure

Ticket management involves:

* Creating tickets
* Recording reported issues
* Tracking ticket status
* Analyzing technical problems
* Following issues through resolution
* Closing resolved tickets

---

Software Development Life Cycle

The Software Development Life Cycle (SDLC) describes the different stages involved in developing and maintaining software.

A simplified lifecycle is:

Requirements
     ↓
Analysis
     ↓
Design
     ↓
Development
     ↓
Testing
     ↓
Deployment
     ↓
Maintenance

SDLC Stages

Requirements

Understanding the business requirements and what the system needs to achieve.

Analysis

Analyzing the requirements and determining how they can be implemented.

Design

Planning the system structure, components, and overall solution.

Development

Implementing the required functionality.

Testing

Verifying that the software works correctly and meets the requirements.

Deployment

Releasing the software to the target environment.

Maintenance

Fixing issues and improving the system after deployment.

---

SDLC Models

Waterfall

Waterfall is a sequential development methodology where each phase is completed before moving to the next.

Requirements
     ↓
Design
     ↓
Development
     ↓
Testing
     ↓
Deployment

It is suitable for projects where requirements are relatively stable and well-defined.

---

Agile

Agile is an iterative development methodology where software is developed and delivered through smaller cycles.

Plan
 ↓
Develop
 ↓
Test
 ↓
Review
 ↓
Improve
 ↺

Agile allows teams to adapt to changing requirements and continuously improve the product.

---

Waterfall vs Agile

Waterfall| Agile
Sequential approach| Iterative approach
Requirements are usually defined early| Requirements can evolve
Testing mainly follows development| Testing occurs continuously
Changes can be more difficult later| Changes can be incorporated more easily
Delivery is usually at the end| Frequent incremental delivery

---

Software Testing

Software Testing is the process of verifying that software works as expected, meets its requirements, and behaves correctly under different conditions.

Testing helps identify:

* Functional issues
* Incorrect behavior
* Integration problems
* Unexpected errors
* Requirements that are not correctly implemented

Different types of testing can be applied at different levels of a software system.

---

Unit Testing

Unit Testing focuses on testing the smallest testable parts of an application, such as individual methods, functions, or classes.

The goal is to verify that each unit behaves correctly in isolation.

A unit test typically follows the Arrange – Act – Assert (AAA) pattern:

// Arrange
var calculator = new Calculator();

// Act
var result = calculator.Add(2, 3);

// Assert
Assert.Equal(5, result);

Unit tests are usually:

* Small and focused
* Fast to execute
* Independent
* Repeatable
* Used to detect problems early

---

Integration Testing

Integration Testing verifies that different components or modules work correctly together.

For example:

API
 ↓
Service
 ↓
Repository
 ↓
Database

Integration testing checks whether these components communicate and work together as expected.

---

Functional Testing

Functional Testing verifies that the software's features behave according to the specified requirements.

For example:

Login
 ↓
Enter valid credentials
 ↓
Submit
 ↓
User is authenticated

It focuses on what the system does rather than how the internal code works.

---

System Testing

System Testing tests the complete application as a whole.

It verifies that the different components of the system work together and that the complete system satisfies its requirements.

For example:

User
 ↓
Application
 ↓
Backend
 ↓
Database
 ↓
Expected Result

---

Regression Testing

Regression Testing ensures that new changes or fixes have not broken existing functionality.

For example:

New Feature / Bug Fix
        ↓
Run Existing Tests
        ↓
Verify Existing Features

Regression testing is especially important when modifying an existing system.

---

Acceptance Testing

Acceptance Testing verifies whether the system meets the business requirements and is ready to be accepted by the customer or end users.

It focuses on whether the software solves the intended business problem.

---

Testing Levels

The different testing levels can be viewed as:

Unit Testing
      ↓
Integration Testing
      ↓
System Testing
      ↓
Acceptance Testing

Testing is an important part of the SDLC because it helps improve software quality, detect defects early, and ensure that the final system meets both technical and business requirements.

---

CRM Development Approach

When implementing a CRM requirement, I think about it in layers:

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
Testing
        ↓
Deployment using Solutions
        ↓
Production

The goal is to use configuration whenever possible and introduce custom code when the business requirement needs more advanced behavior.

---

Topics Covered

Topic| Description
CRM Foundations| CRM concepts and business areas
Sales Cycle| Understanding the CRM sales process
CRM Environments| Development, Staging, and Production
CRM Customization| Configuring and extending CRM
Entities| CRM data structures
Custom Entities| Creating business-specific data models
Fields| Storing and configuring CRM data
Relationships| Connecting CRM entities
Forms| Customizing record forms
Views| Displaying and filtering records
Business Rules| Implementing simple business logic
BPM Tools| Business Process Management tools
BPM Portals| Process Admin, Inspector, Portal, and Designer
Workflows| Automating business processes
Dialogs| Guiding users through business processes
Plugins| Server-side C# customization
C#| Developing CRM business logic
JavaScript| Client-side form customization
Visual Studio| CRM development environment
.NET Framework| Framework used for CRM development
XrmToolBox| CRM development and administration utilities
FetchXML| Querying CRM data
OData / Web API| Accessing CRM through APIs
CRM SDK| Programmatic CRM development
Solutions| Packaging and deploying customizations
Security| Users, roles, privileges, and access
ManageEngine| Support and ticket management
Ticket Management| Tracking and resolving technical issues
SDLC| Software development lifecycle
Waterfall| Sequential development methodology
Agile| Iterative development methodology
Software Testing| Verifying software quality and requirements
Unit Testing| Testing individual methods, functions, or classes
Integration Testing| Testing interactions between application components
Functional Testing| Verifying features against their requirements
System Testing| Testing the complete application as a whole
Regression Testing| Ensuring existing functionality still works after changes
Acceptance Testing| Verifying that the system meets business requirements

---

Learning Outcomes

Through this internship, I developed a foundation in:

- Microsoft Dynamics CRM / Dynamics 365
- CRM customization and configuration
- CRM business processes
- C# and JavaScript
- CRM Plugins
- Workflows and Dialogs
- Business Process Management
- CRM data querying
- XrmToolBox
- CRM SDK and Web API
- CRM Solutions and deployment
- Role-based security
- Technical support and ticket management
- Software Development Life Cycle
- Waterfall and Agile methodologies
- Software Testing
- Unit, Integration, Functional, System, Regression, and Acceptance Testing
