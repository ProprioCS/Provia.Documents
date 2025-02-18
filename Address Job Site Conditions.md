- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
- 7 [Technical Considerations](#Technical-Considerations)
- 8 [Technical Specifications](#Technical-Specifications)
    - 8.1 [Object Definitions](#Object-Definitions)
    - 8.2 [Data Design](#Data-Design)
    - 8.3 [Scripts and Automations](#Scripts-and-Automations)
- 9 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 9.1 [Unit Tests](#Unit-Tests)
    - 9.2 [Process Tests](#Process-Tests)
- 10 [Time Estimate](#Time-Estimate)

## Overview

The Customer Site Conditions component within Orion aims to streamline the process of capturing and utilizing site-specific information for contract furniture dealers. This solution allows users to save and store the unique conditions and attributes of each customer site, so that Operations can provide an accurate Labor Quote, and also prepare for the Installation. By centralizing this information, the component eliminates the need for repetitive data entry and ensures consistency across various aspects of the project lifecycle.

Key benefits of the Customer Site Conditions component include:

1. Improved efficiency: Users can quickly access and auto-populate saved site conditions on appropriate interfaces throughout the Orion solution, reducing manual effort and saving time.
    
2. Enhanced accuracy: Centralizing site-specific information minimizes the risk of errors and inconsistencies that may arise from manual data entry.
    
3. Better collaboration: By providing a single source of truth for customer site conditions, the component facilitates seamless communication and collaboration among different teams and stakeholders.
    

## Solution Type

·       Customizations – standard netsuite customization including point and click and simple scripts

## User Stories

**User Stories**

1. As a Lead Installer, I want to observe and record the specific conditions of a Customer Site while I am there, so that I can accurately capture and share the site information with the rest of the team.
    
2. As the Scheduler, I want to review the site conditions for a job as I determine how many resources to assign, as well as which resources.
    
3. As a Project Manager, I want to easily access and review the stored Customer Site conditions, so that I can make informed decisions and ensure project success.
    
4. As a Salesperson, I want to record Customer Site conditions without having to visit the site, so that I can efficiently capture important information and streamline the sales process.
    
5. As a Quoter, I want to have visibility to saved Customer Site conditions while quoting a job for that site, so that I can provide accurate and competitive quotes based on the specific site requirements.
    

## Success Metrics

1. Reduction in time spent manually entering and searching for site condition information, measured by tracking user activity and soliciting feedback.
    
2. Increase in the accuracy and completeness of site condition data, assessed by regular audits and comparisons to actual site visits.
    
3. Improvement in collaboration and communication among team members, evaluated through surveys and feedback sessions.
    
4. Increased sales efficiency, measured by tracking the time from opportunity creation to close and the number of site visits required per sale.
    

## Design

The Customer Site Conditions customization will feature a user-friendly interface that allows users to easily input, view, and manage site condition information. The main components of the UI will include:

1. We will use the Requirements feature to display the dealer’s Site Condition options on a Customer Address.
    
2. The specific values for this Customer Site will be saved to the customrecord_orion_requirement_values record, by the addressbook ID. No other custom record will be needed, unless needed for a Site Note, Site Photos, or Documents.
    
3. In addition to the Customer Address, Site Conditions will be visible when within a Quote, Order, Labor Quote or Work Order when they have been saved for the Customer Address.
    

The UX will focus on simplicity, efficiency, and ease of use, ensuring that users can quickly access and update site condition information as needed.

1. **Roles and Permissions**
    
    1. Orion - Executive Leadership: View access to all Customer Site Conditions data.
        
    2. Orion - Marketing Specialist: No access to Customer Site Conditions data.
        
    3. Orion - Sales Leadership: View access to all Customer Site Conditions data.
        
    4. Orion - Salesperson/Account Manager: View and create access to Customer Site Conditions data for their assigned accounts.
        
    5. Orion - Sales Support: View and create access to all Customer Site Conditions data.
        
    6. Orion - Admin: Full access to all Customer Site Conditions data, including view, create, edit, and delete permissions.
        
    7. Orion - Design Manager: View access to all Customer Site Conditions data.
        
    8. Orion - Designer: View access to all Customer Site Conditions data.
        
    9. Orion - Purchasing: View access to all Customer Site Conditions data.
        
    10. Orion - Procurement: View access to all Customer Site Conditions data.
        
    11. Orion - Ops Manager: View, create, and edit access to all Customer Site Conditions data.
        
    12. Orion - Project Manager: View, create, and edit access to Customer Site Conditions data for their assigned projects.
        
    13. Orion - Operations Admin/Support: View, create, and edit access to all Customer Site Conditions data.
        
    14. Orion - Inventory Manager: View access to all Customer Site Conditions data.
        
    15. Orion - Warehouse Manager: View access to all Customer Site Conditions data.
        
    16. Orion - Accounting Manager: No access to Customer Site Conditions data.
        
    17. Orion - Warehouse: View access to all Customer Site Conditions data.
        
    18. Orion - Controller/CFO: No access to Customer Site Conditions data.
        
    19. Orion - A/P Analyst: No access to Customer Site Conditions data.
        
    20. Orion - A/R Analyst: No access to Customer Site Conditions data.
        
    21. Orion - Human Resources/Payroll: No access to Customer Site Conditions data.
        
    22. Orion - Employee Center: No access to Customer Site Conditions data.
        
    23. Orion - Resource Manager: View access to all Customer Site Conditions data.
        
    24. Orion - Daily Administrator: View access to all Customer Site Conditions data.
        

## Features and Functionality

**Features and Functionality** The Customer Site Conditions customization will include the following key features and functionalities:

- Create, view, edit, and delete Customer Site Conditions records based on user permissions.
    
- Customize the Customer Addresses interface to allow getting to any saved site condition records - as well as to enter new ones.
    
- Integration with NetSuite's standard permission system to control access based on user roles.
    
- Ability to attach photos, documents, and notes to site condition records for enhanced context and collaboration.
    

## Technical Considerations

Site Conditions are simply a special case of Requirements, which apply to a Customer Site. Reference the Requirements Feature solution design for more detail.

When creating a Labor Quote or Work Order, any saved Site Conditions for the selected Installation Address will automatically be inherited by the requirements displayed on the LQ or WO.

## Technical Specifications

## Object Definitions

## Data Design

For the most part, Site Conditions do not need their own record, as the requirement_values record can store them.

However, we need to discuss if we also want to be able to store a Site Note by Customer address (maybe just a custom field?), and also if we want them to be able to attach files to a Customer address - and if that can be done without a custom record.

## Scripts and Automations

The Requirements scripts (runtime and admin) provide most of the functionality needed. We will have to customize the Customer Address area of the Customer form, and have user event scripts to load and save the data.

## Testing and Quality Assurance

Test Script Title: Customer Site Conditions Test Script

Test Objectives:

1. Verify that users can save, store, and access customer site conditions effectively within the Orion solution.
    
2. Ensure that the centralized site condition information is accurately populated and utilized across various interfaces and aspects of the project lifecycle.
    
3. Validate that the component improves efficiency, accuracy, and collaboration among different teams and stakeholders.
    

## Unit Tests

## Process Tests

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development||
|NetSuite Setup||
|QA||
|**Total**|**0**|

Be the first to add a reaction