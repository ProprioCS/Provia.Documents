- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
    - 5.1 [Core Components:](#Core-Components%3A)
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

## Overview

The Orion Commission Module revolutionizes commission management for contract furniture dealers by introducing a project-centric approach that aligns with modern project management practices. Moving beyond traditional line-by-line calculations, this module provides a comprehensive commission framework that automatically calculates commissions based on project-level gross profit, incorporating both actual and estimated data throughout the project lifecycle.

The module features an intelligent calculation engine that automatically triggers commission calculations based on configurable events and performs true-ups as projects progress. Its flexible commission plan architecture supports a hierarchical rule system that accommodates complex commission scenarios while preventing manipulation through strategic order splitting.

The module introduces a relative-to calculation framework that determines commission amounts based on the proportion of total project sell represented by each triggering document, while always using the project's overall GP for rate determination. This approach ensures fair commission distribution throughout the project lifecycle while preventing manipulation through strategic order splitting.

## Solution Type

Module – This is an extensive functionality module that includes:

- Commission calculation framework
    
- Integration with project management
    
- Complex business rules engine
    
- Automated workflows
    
- Trigger-based commission scheduling
    

## User Stories

1. "As a salesperson, I want to see my projected and approved commissions for each project in real-time so I can track my earnings and focus my efforts effectively."
    
2. "As a sales manager, I want to review and approve commission calculations before payment processing so I can ensure accuracy and handle any special circumstances."
    
3. "As a controller, I want the system to automatically calculate true-ups and clawbacks based on project changes and payment status so I can maintain accurate commission records without manual intervention."
    
4. "As a sales operations manager, I want to configure different commission plans with varying rates, thresholds, and rules so I can implement complex compensation structures across different divisions and scenarios."
    
5. "As a project manager, I want to mark specific lines or transactions as non-commissionable so I can properly handle warranty work, internal costs, and other special cases that shouldn't affect commission calculations."
    
6. "As an accounting manager, I want the system to calculate commissions based on the project's sales team structure and automatically handle splits between primary and secondary sales representatives so I can ensure fair compensation distribution."
    
7. "As a CFO, I want visibility into commission calculations at both the master project and sub-project levels so I can analyze commission expenses across different business units and project types."
    
8. "As a sales operations manager, I want to configure multiple commission calculation triggers per plan so I can automate initial payments and true-ups at different project stages."
    
9. "As a controller, I want the system to automatically handle negative GP scenarios with appropriate clawbacks so I can maintain accurate commission payments."
    
10. "As an administrator, I want to prevent overlapping commission plans while allowing multiple plans across different locations/subsidiaries."
    
11. "As a commission administrator, I need to specify priorities for commission plans to handle cases where multiple plans could apply to ensure the correct plan is selected automatically."
    
12. "As a commission administrator, I want commission plans to be copied and timestamped when applied to projects so that subsequent changes to the original commission plan don't affect existing projects."
    
13. "As a commission administrator, I need flexible expiration date options for commission plans to support both indefinite and time-bound commission structures."
    
14. "As a commission administrator, I need to control which lines affect commission GP calculations to properly handle special cases and non-commissionable items."
    

## Success Metrics

- Reduction in commission calculation time (comparing automated project-based calculations vs. manual/line-based methods)
    
- Accuracy of commission calculations (measured by reduction in manual adjustments and corrections)
    
- Time saved in commission reconciliation process (particularly for complex projects with multiple sales team members)
    
- Adoption rate among sales teams (measured by percentage of projects using automated commission calculations vs. manual tracking)
    
- Reduction in commission-related disputes (tracking frequency and resolution time of commission discrepancies)
    
- Accuracy of automated trigger processing
    
- Reduction in commission plan configuration time
    
- System performance under configured calculation frequency
    

## Design

### Core Components:

1. Commission Plan Record
    
    - Plan configuration and rules
        
    - Effective dates (with overlap prevention)
        
    - Location/subsidiary assignment
        
    - Rate card data (JSON)
        
    - Trigger configurations
        
    - Priority ranking
        
    - Project plan flag (indicates if plan is a static project copy)
        
    - Original plan reference (for project copies)
        
    - Book date reference (from first sales order)
        
2. Commission Trigger Record
    
    - Event type (deposit, invoice, payment, etc.)
        
    - Calculation type (initial, true-up)
        
    - Sequence number
        
    - ==Conditions/rules==
        
3. Commission Payment Record
    
    - Calculation results
        
    - Status tracking
        
    - Project reference
        
    - Trigger reference
        
    - Audit history
        
4. Commission Schedule Configuration
    
    - Schedule type (Initial/Recalculate/One Time)
        
    - Relative to field (Project Total/Invoiced/Cash Received)
        
    - Percentage calculation rules
        
    - Trigger definitions
        

## Roles and Permissions

Full Access (Configure, Approve, View All):

- Orion - Executive Leadership
    
- Orion - Controller/CFO
    
- Orion - Accounting Manager
    
- Orion - Daily Administrator
    

Approval & View Access:

- Orion - Sales Leadership (Approve team commissions, view all)
    
- Orion - Ops Manager (View all, approve project-related)
    
- Orion - A/P Analyst (Process payments, view all)
    
- Orion - A/R Analyst (Process payments, view all)
    
- Orion - Human Resources/Payroll (Process payments, view all)
    

View Own + Project Access:

- Orion - Salesperson/Account Manager (View own commissions)
    
- Orion - Project Manager (View project commissions)
    
- Orion - Sales Support (View related commissions)
    
- Orion - Operations Admin/Support (View project-related)
    
- Orion - Resource Manager (View team-related)
    

View Only Access:

- Orion - Procurement
    
- Orion - Purchasing
    
- Orion - Marketing Specialist
    

No Access Required:

- Orion - Design Manager
    
- Orion - Designer
    
- Orion - Inventory Manager
    
- Orion - Warehouse Manager
    
- Orion - Warehouse
    
- Orion - Employee Center
    

## Features and Functionality

Automations:

- Automatic commission calculation based on configurable events (invoice creation, payment receipt)
    
- Scheduled commission recalculations (every 15 minutes)
    
- Project-level GP calculations combining actual and estimated data
    
- True-up calculations when project status changes
    
- Clawback calculations for write-offs and corrections
    
- Commission splits based on sales team structure
    
- Integration with project hierarchy
    
- Commission plan priority-based selection
    
- Project-specific commission plan snapshot creation
    
- Relative-to calculations based on project total sell
    
- Non-commissionable line exclusion from calculations
    

User Actions:

- Create/modify commission plans with effective dates
    
- Configure rate cards and calculation rules
    
- Assign sales teams and contribution percentages
    
- Mark items/transactions as non-commissionable
    
- Review pending commission calculations
    
- Approve/reject commission payments
    
- Generate commission reports
    
- Override calculations with proper permissions
    
- Manage project relationships for commission purposes
    
- Set commission plan priorities
    
- Mark lines/transactions as non-commissionable
    
- Configure relative-to calculation basis
    
- Review and select from applicable commission plans
    

## Technical Considerations

1. Architecture Requirements
    
    - Custom parent-child relationship field for project hierarchy
        
    - JSON blob storage for rate card data instead of separate records
        
    - Scheduled MapReduce script for commission calculations
        
    - Custom commission calculation events/triggers
        
    - Commission plan snapshot storage and referencing system
        
    
    - Priority field and resolution logic implementation
        
    
    - Relative-to calculation framework
        
    
    - Non-commissionable flag implementation at line and body levels
        
2. Key Constraints
    
    - Must maintain performance with 15-minute calculation intervals
        
    - Need to handle multiple commission calculations per project
        
    - Complex GP calculations combining actuals and estimates
        
    - Commission records must maintain audit trail for changes
        
    - Project sales team restrictions (one team per project)
        
    - Must support manual priority assignment in V1 (automated in V2)
        
    
    - Need to handle multiple relative-to calculation bases
        
    
    - Must maintain relationship between original and project-specific commission plans
        
    
    - Need to validate priority conflicts across multiple plans
        
3. Integration Points
    
    - Project management system
        
    - Invoice processing
        
    - Payment processing
        
    - Vendor bill processing
        
    - Time tracking impact on costs
        
    - Invoice processing (for relative-to calculations)
        
    
    - Payment processing (for relative-to calculations)
        
    
    - Project management system (for commission plan snapshots)
        

## Technical Specifications

## Object Definitions

1. Commission Plan
    
    - Plan configuration and rules
        
    - Effective dates (with overlap prevention)
        
    - Rate card data (JSON)
        
    - Assignment criteria
        
    - Trigger configurations
        
    - Book date reference
        
2. Commission Trigger
    
    - Event type definitions
        
    - Calculation type (initial/true-up)
        
    - Sequence settings
        
    - Condition rules
        
3. Commission Payment
    
    - Calculation results
        
    - Status tracking
        
    - Audit history
        
    - Project reference
        
    - Trigger reference
        
4. Project (Enhanced)
    
    - Book Date (sourced from first sales order)
        
    - Commission Plan Reference
        
    - Commission Status
        
    - Forecasted Commission Amount
        
    - Actual Commission Amount
        

## Data Design

1. Core Objects:
    
    - Commission Plan
        
    - Commission Trigger
        
    - Commission Payment
        
    - Project (enhanced)
        
    - Transaction customizations
        
2. Relationships:
    
    - Project hierarchy (parent/child)
        
    - Sales team assignments
        
    - Commission plan assignments
        
    - Trigger sequences
        
    - Location/subsidiary assignments
        

## Scripts and Automations

1. Scheduled Scripts
    
    - Commission calculation (configurable intervals)
        
    - True-up processing
        
    - Status updates
        
    - Overlap prevention validation
        
2. User Event Scripts
    
    - Project updates
        
    - Transaction processing
        
    - Commission plan changes
        
    - Book date assignment
        
    - Trigger event processing
        
3. Client Scripts
    
    - UI validations
        
    - Dynamic field updates
        
    - User experience enhancements
        
    - Rate card calculations
        
    - GP validation rules
        

## Testing and Quality Assurance

## Unit Tests

1. Commission Calculations
    
    - Basic GP calculations
        
    - Split calculations
        
    - True-up scenarios
        
    - Clawback processing
        
    - Negative GP handling
        
    - Rate card calculations
        
    - Trigger sequencing validation
        
2. Project Integration
    
    - Hierarchy updates
        
    - Sales team validation
        
    - Status changes
        
    - Book date assignment
        
    - Commission plan application
        

## Process Tests

1. End-to-End Workflows
    
    - Commission plan creation/updates
        
    - Calculation triggers
        
    - Approval process
        
    - Payment processing
        
    - Overlap prevention
        
    - Multiple location handling
        
2. Integration Testing
    
    - Project management integration
        
    - Transaction processing
        
    - Payment processing
        
    - Trigger event processing
        

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

|   |   |   |   |   |
|---|---|---|---|---|
|**Version**|**Date**|**Author**|**Type**|**Description**|

|   |   |   |   |   |
|---|---|---|---|---|
|**Version**|**Date**|**Author**|**Type**|**Description**|
|1.0|2024-11-13|@John Dasharion|Initial|Initial version of solution design|
|1.1|2024-11-13|@John Dasharion|Changed|Enhanced commission module design with trigger-based scheduling, negative GP handling, and plan overlap prevention. Added detailed specifications for commission triggers and expanded testing scenarios. Added new user stories and success metrics for automated processing.<br><br>---<br><br>This change was made after a solution design meeting was had on Nov 11, 2024.<br><br>Fathom Recording of Solution Design meeting: [https://fathom.video/share/xremRZYVa8JTHTs9LitszCf6UvbGwLr-](https://fathom.video/share/xremRZYVa8JTHTs9LitszCf6UvbGwLr-)<br><br>Here are key Changes/Decisions from the Discussion:<br><br>1. Commission Plan Structure:<br>    <br>    1. Move to using a trigger record system for commission calculation timing<br>        <br>    2. Commission plans should be project-based rather than transaction-based<br>        <br>    3. Need to prevent overlapping commission plans<br>        <br>    4. Should be able to have multiple commission plans at separate locations/subsidiaries<br>        <br>2. Commission Calculation:<br>    <br>    1. Commission calculation should be based on the project's book date (date of first sales order)<br>        <br>    2. System should support both initial calculations and recalculations/true-ups<br>        <br>    3. Need validation to prevent gaps in GP percentage ranges<br>        <br>    4. Should handle negative GP scenarios with clawbacks<br>        <br>3. Technical Implementation:<br>    <br>    1. Commission rate tables should be stored as JSON<br>        <br>    2. Need to implement a scheduled script with configurable frequency (determined during implementation)<br>        <br>    3. Need field-level permissions for project field editing|
|1.2|Jan 17, 2025|@John Dasharion|Changed / Added|- Added relative-to calculation framework explanation<br>    <br><br>- Added 4 new user stories for commission admin requirements<br>    <br><br>- Updated Commission Plan Record to include priority and snapshot functionality<br>    <br><br>- Added Commission Schedule Configuration to core components<br>    <br><br>- Added new automation features for priority selection and plan snapshots<br>    <br><br>- Updated technical considerations for new requirements|

Be the first to add a reaction