- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
    - 5.1 [Design Requests Kanban Board](#Design-Requests-Kanban-Board)
- 6 [Roles and Permissions](#Roles-and-Permissions)
- 7 [Features and Functionality](#Features-and-Functionality)
- 8 [Technical Considerations](#Technical-Considerations)
- 9 [Technical Specifications](#Technical-Specifications)
    - 9.1 [Object Definitions](#Object-Definitions)
    - 9.2 [Data Design](#Data-Design)
    - 9.3 [Scripts and Automations](#Scripts-and-Automations)
- 10 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 10.1 [Unit Tests](#Unit-Tests)
    - 10.2 [Process Tests](#Process-Tests)
- 11 [Time Estimate](#Time-Estimate)
- 12 [Changes And Revisions](#Changes-And-Revisions)
- 13 [Solution Design - Change Log](#Solution-Design---Change-Log)

## Overview

The NetSuite Kanban Board is a React-based, visual, card-based solution that allows users to efficiently manage and track any NetSuite record throughout its lifecycle. It provides a centralized platform for teams to collaborate, assign tasks, and monitor progress of their workflows. The Kanban Board seamlessly integrates with NetSuite records through saved searches and can display multiple record types (such as Projects, Opportunities, Tasks, Cases, Design Requests, Sales Orders, or any custom record type) in a single view.

The solution will be implemented as a SuiteLet and can be applied to any NetSuite record type with proper view definition. This flexibility allows organizations to visualize and manage various workflows through a unified interface while maintaining data consistency and accuracy.

This is another company that is doing this well, using saved searches to feed the data: [![](https://suitecorner.com/wp-content/uploads/2022/05/favicon_suitecorner.svg)Kanban Board for any NetSuite Process - suitecorner](https://suitecorner.com/en/kanban-board-for-any-netsuite-process/)

## Solution Type

Module

## User Stories

1. As a Manager, I want to review records assigned to my team, assign them to team members, and monitor workload and capacity across different record types.
    
2. As a Team Member, I want to view and filter records assigned to me, update their status, and record important information, regardless of record type.
    
3. As a Process Owner, I want to configure Kanban views that combine different record types to give me a complete view of my business processes.
    
4. As a user, I want to be able to search and filter across all cards to quickly find relevant items and update them.
    

## Success Metrics

1. The Kanban board will provide configurable metrics such as:
    
    - Average time records spend in each status/column
        
    - Average processing time from assignment to completion
        
    - Percentage of records completed within target timelines
        
    - Workload distribution across team members
        
    - Volume of records processed per time period
        
    - Custom metrics based on record type-specific fields
        
2. The Kanban board will present all record types in a consistent, user-friendly card format
    

## Design

The interface will follow the look and feel of the existing tool, found here:

[https://dhtmlx.com/docs/products/dhtmlxKanban/](https://dhtmlx.com/docs/products/dhtmlxKanban/)

Cards will use Provia view records with type "card" and utilize JSON cell definitions for layout, supporting different card areas (header, title, body) and formula functionality matching smart table capabilities. The layout and displayed fields will be configurable based on record type.

## Design Requests Kanban Board

The Kanban board for design requests needs the following fields:

1. Sales Rep (from entity record if no Transaction is linked, else Primary from Opp or Transaction)
    
2. Project # (will be needed once Project record is fully functional)
    
3. Transaction link - if transaction exists, should be linked to the Design Request; if Design Request was created from Opp or Transaction, should auto-fill
    
4. Order Name - (needs to be sorted on transactions as some use [title] and SO uses our custom field) - but the Order Name should show on the cards
    
5. Hyperlink to the full Design Request record to access all information and enable responses/interaction with fields.
    

## Roles and Permissions

1. Administrator: Ability to configure Kanban views, define card layouts, and set up record type mappings.
    
2. Manager: Full access to view, create, edit, and move cards between columns, assign team members, and manage workflows within their permission scope.
    
3. Team Member: Access to view, edit, and move cards assigned to them, update status, add comments, and attach files based on their NetSuite permissions.
    

## Features and Functionality

Features - each card will contain sections for:

- Configurable display fields based on record type (e.g., Due Date, Customer, Name, Transaction #, Record #, Created by, Updated by, Assigned to)
    
- Version/revision tracking - ability to track version changes per record - will be used in metrics and to drive coaching or change in behavior, identification of increased costs, etc. Can be achieved by a field and a date/timestamp
    
- Notifications when assigned to individuals
    
- Notifications when status changed
    
- Notifications for version/revision adjustments (to relevant parties)
    
- Widgets for additional data visualization
    
- KPIs displayed above the card view, like this demo:
    

Widgets: [https://snippet.dhtmlx.com/5pfab4yg?text=kanban](https://snippet.dhtmlx.com/5pfab4yg?text=kanban)

User Actions:

- Create and submit new records with required information
    
- Update and edit record details (based on permissions)
    
- Assign records to team members (Manager)
    
- Move cards between columns to update status
    
- Add comments and attach files to records
    
- Filter and search for specific records based on criteria
    
- View detailed information about each record by clicking on the card
    
- Cards organized into columns representing different statuses, which can be configured during implementation
    

Automations:

- Automatic status updates based on linked records
    
- Move completed or cancelled items to non-active status
    
- Clear "double check" field when a revision is selected
    
- Date stamp for "double check" to ensure it is recent
    
- Link records to related NetSuite records for seamless information transition
    

Additional Features:

- Configurable process stages
    
- Expanded and configurable fields for deliverables, billable and non-billable services, ancillary products
    
- Enhanced board views with filters for location, division, and assignee
    
- Workload views for team leads
    
- RFP handling capability with win/loss status tracking
    
- Reporting capabilities to extract Kanban Board data from NetSuite
    

## Technical Considerations

1. _Relationship between displayed records and other NetSuite records_
    
2. Links to Requirements record/engine (from Joe Keller)
    
3. Status updates and saved searches
    
4. Time entry integration - visual bar percent to completion for actual to quoted hours
    
5. Data integrity and synchronization
    
6. Performance and scalability
    
7. Security and access controls
    

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

**Testing and Quality Assurance** Test Script Title: Kanban Board Functionality and Integration Test Script

Test Objectives:

1. Verify the functionality and user experience of the Kanban Board
    
2. Validate the integration and data flow between the Kanban Board and related NetSuite records
    
3. Assess the performance, scalability, and security of the Kanban Board
    

Test Environment: Sandbox and Production

Test Data: Representative records that closely mimic real-world scenarios, covering various types, related records, user roles and actions, edge cases, and integration scenarios.

Test Steps:

1. Create a new record
    
2. Assign and update a record
    
3. Collaborate on a record
    
4. Test integration with related records
    
5. Verify reporting and analytics
    

Test Assertions:

1. Role-based access control
    
2. Data security and privacy
    
3. Filter and search functionality
    
4. Workflow and status transitions
    
5. Performance and scalability
    

Test Metrics:

1. User Acceptance
    
2. Defect Density
    
3. Performance Metrics
    

Test Execution: Provide instructions on test environment setup, test script execution, defect reporting, communication, and collaboration. Utilize test management tools, defect tracking tools, test automation tools, and performance testing tools.

Defect Reporting: Follow a standardized process for reporting defects, including clear descriptions, severity levels, priority levels, screenshots/attachments, and defect tracking using a designated tool.

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

## Changes And Revisions

Be sure to Tag Dev (Luke) any time a new change is made. Format will be

## Solution Design - Change Log

|Version|Date|Author|Type|Description|
|---|---|---|---|---|

|   |   |   |   |   |
|---|---|---|---|---|
|Version|Date|Author|Type|Description|
|1.2|Nov 13, 2024|@John Dasharion|Changed|- Restructured solution design to support generic record types instead of design-specific implementation<br>    <br>- Updated implementation approach to use React and SuiteLet architecture<br>    <br>- Added support for multiple record types in single board view<br>    <br>- Added flexible data source integration through saved searches<br>    <br>- Updated roles and permissions to be record-type agnostic<br>    <br>- Revised success metrics to be configurable per record type<br>    <br>- Initial solution design for Design Request Kanban Board|
|1.3|2024-11-22|@John Dasharion|Added|Added required fields that were called out in [OQA-466](https://suitecentric.atlassian.net/browse/OQA-466 "https://suitecentric.atlassian.net/browse/OQA-466")|

Be the first to add a reaction