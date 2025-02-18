## Overview

The Orion Invoice Schedule solution is a sophisticated utility designed to streamline and automate the invoicing process for contract furniture dealers within the NetSuite environment. This component allows users to create invoice schedule templates, apply them to transactions, and manage invoice events and triggers. By setting up these schedules in advance, the system can automatically prompt relevant users to generate invoices at the appropriate times and for the correct amounts.

This solution addresses the common challenge of managing complex, multi-phase projects with varying payment terms. It ensures timely and accurate invoicing, reducing manual errors and improving cash flow management. The Invoice Schedule utility integrates seamlessly with other Orion modules, providing a cohesive financial management experience within NetSuite.

## Solution Type

Utility

## User Stories

1. As a Project Manager, I want to create an invoice schedule template for large-scale office furniture installation projects, so that I can ensure consistent billing across multiple projects with similar phases.
    
2. As a Sales Representative, I want to apply an invoice schedule template to a quote and modify it if necessary, so that I can quickly set up accurate billing schedules for my clients.
    
3. As an Accounting Manager, I want to set up custom invoice triggers based on specific project criteria, so that I can automate invoice generation for unique business scenarios.
    
4. As a Financial Analyst, I want to view and analyze invoice schedules across multiple projects, so that I can forecast cash flow and identify billing patterns.
    

## Success Metrics

1. Reduction in average days sales outstanding (DSO)
    
2. Increase in percentage of invoices sent on time according to schedule
    
3. Decrease in time spent manually creating and tracking invoice schedules
    
4. Improvement in client satisfaction ratings related to billing processes
    
5. Increase in the number of projects using standardized invoice schedule templates
    

## Design (UI/UX Overview)

The Orion Invoice Schedule Utility features a custom React application embedded within NetSuite, providing a seamless and intuitive user interface. Key design elements include:

1. Template Configuration Interface: A dynamic, user-friendly React component allowing users to create and modify invoice schedule templates.
    
2. Transaction-level Schedule Management: React components embedded in Quote and Sales Order records for applying templates and managing invoice events.
    
3. Invoice Schedule Template Field: A body field named "Invoice Schedule Template" on both Quote and Sales Order records, allowing users to select and apply a template.
    
4. Trigger Configuration Interface: A NetSuite native interface for setting up and managing invoice triggers.
    
5. Custom Record Integration: The utility stores template, event, and trigger data in custom NetSuite records, ensuring robust data management and easier integration with other NetSuite functionalities.
    
6. New Line Addition: The option to add a new invoice event is placed at the bottom of the table for a more intuitive user experience.
    
7. Non-Editable Completed Events: Invoice events with assigned transaction numbers are displayed as non-editable and non-deletable.
    

## Custom Records

1. Invoice Schedule Template
    
    - Implemented as a React component
        
    - Stores the base template for invoice schedules
        
2. Invoice Schedule Events
    
    - Implemented as a React component
        
    - Stores specific events related to invoicing
        
    - Fields include:
        
        - Invoice Type (list: Deposit, Product Invoice, Pro Forma Invoice, Final Invoice, Request for Deposit)
            
        - Value (percentage)
            
        - Trigger Type (list: Date, Days Open (Order), Days Open (Project), Event)
            
        - Trigger (varies based on Trigger Type) Make this a List/Record for Invoice Triggers
            
        - Terms (sourced from native NetSuite list)
            
        - Comments (free-form text)
            
        - Invoice Ready (checkbox)
            
        - Transaction Number (text, stores associated transaction number)
            
        - Transaction Amount (currency)
            
        - Quote Number (hidden from UI)
            
        - Sales Order Number (hidden from UI)
            
        - Project Number (hidden from UI)
            
3. Invoice Triggers
    
    - Standard NetSuite custom record
        
    - Fields:
        
        - Name: Text field for the trigger name
            
        - Saved Search: Field to select a saved search for the query
            
        - Custom SuiteQL: Text area field for users to input custom SuiteQL queries
            
4. Event Trigger Sub-Record
    
    - Fields:
        
        - Title
            
        - Query (based on saved searches)
            

## Roles and Permissions

Create and Edit Access for Templates and Triggers:

- Orion - Sales Leadership
    
- Orion - Sales
    
- Orion - Salesperson/ Account Manager
    
- Orion - Sales Support
    
- Orion - Ops Manager
    
- Orion - Project Manager
    
- Orion - Operations Admin/ Support
    

Apply Templates and Modify Events on Transactions:

- All roles with Create and Edit Access
    
- Orion - Accounting Manager
    
- Orion - Controller/CFO
    
- Orion - A/R Analyst
    

View-Only Access:

- All other Orion roles
    

## Features and Functionality

1. Template Creation and Management
    
    - Create reusable invoice schedule templates
        
    - Set specific percentages or amounts for each invoice in the template
        
    - Assign invoice types (e.g., deposit, progress, final) to each line item
        
2. Transaction-level Schedule Management
    
    - Apply templates to Quote and Sales Order records using the "Invoice Schedule Template" body field
        
    - Automatically populate invoice events based on the selected template
        
    - Modify invoice events on individual transactions without affecting the original template
        
    - View and edit existing invoice schedules
        
    - New invoice events are added to the bottom of the list
        
3. Invoice Trigger System
    
    - Create custom trigger types using saved searches or SuiteQL queries
        
    - Automatically detect when trigger conditions are met
        
    - Automatically check the "Invoice Ready" checkbox when trigger conditions are met
        
    - Automatically uncheck the "Invoice Ready" checkbox when a transaction number is assigned
        
    - Generate automated reminders for invoices ready to be sent
        
4. Reporting and Analytics
    
    - Provide a clear visual representation of invoice schedules in the custom React UI
        
    - Implement a dashboard for viewing and managing invoice schedules across multiple projects
        
5. Integration with Existing Processes
    
    - Seamless integration with quote and sales order processes
        
    - Ensure consistency between invoice schedule and actual order details
        
    - Invoice Schedule appears as a sub-list on the accounting tab of Quote and Sales Order records
        

## Technical Considerations

1. Custom React application development within NetSuite environment
    
2. Creation and management of three distinct custom NetSuite records
    
3. Integration with existing NetSuite quote and sales order records
    
4. Implementation of SuiteQL for defining and executing trigger type queries
    
5. Development of a custom reminder dashboard using NetSuite saved searches
    
6. Ensuring data consistency between templates, transaction-level modifications, and NetSuite records
    
7. Performance optimization for handling large numbers of invoice schedules
    
8. Security considerations for accessing and modifying invoice schedule data
    

## JSON Sample

`{ "invoicingSchedule": [ { "invoiceType": { "id": 1, "value": "Deposit on Product" }, "value": 50, "triggerType": { "id": 1, "value": "Event" }, "trigger": { "id": 1, "value": "Upon Quote Approval" }, "terms": "Due on Receipt" }, { "invoiceType": { "id": 2, "value": "Proforma Invoice" }, "value": 20, "triggerType": { "id": 2, "value": "Date" }, "trigger": { "id": 2, "value": "03/04/2025" }, "terms": "15" }, { "invoiceType": { "id": 2, "value": "Proforma Invoice" }, "value": 20, "triggerType": { "id": 3, "value": "Days Open (Order, Project)" }, "trigger": { "id": 3, "value": "30" }, "terms": "Due on Receipt" }, { "invoiceType": { "id": 3, "value": "Final Invoice" }, "value": 10, "triggerType": { "id": 1, "value": "Event" }, "trigger": { "id": 4, "value": "Work Orders Complete" }, "terms": "30 Days" } ] } // Lists from NS lists "listOptions": { "invoiceTypes": [ {"id": 1, "value": "Deposit on Product"}, {"id": 2, "value": "Proforma Invoice"}, {"id": 3, "value": "Final Invoice"} ], "triggerTypes": [ {"id": 1, "value": "Event"}, {"id": 2, "value": "Date"}, {"id": 3, "value": "Days Open (Order, Project)"} ] }`

## Testing and Quality Assurance

1. Verify accurate creation and management of invoice schedule templates
    
2. Test application of templates to quotes and sales orders
    
3. Ensure proper functioning of trigger types and automated notifications
    
4. Validate the integration with existing quote and sales order processes
    
5. Test performance with a large number of schedules and complex trigger conditions
    
6. Verify correct behavior of automatic checkbox updates for "Invoice Ready"
    
7. Test the non-editable and non-deletable functionality for completed invoice events
    

## Implementation Phases

1. Phase 1: Core functionality
    
    - Develop custom records and React components
        
    - Implement basic template creation and application
        
2. Phase 2: Advanced features
    
    - Develop trigger system
        
    - Create reporting and analytics dashboard
        
3. Phase 3: Integration and optimization
    
    - Integrate with existing NetSuite processes
        
    - Perform performance optimizations
        
4. Phase 4: Testing and deployment
    
    - Conduct thorough testing
        
    - Deploy to production and provide user training
        
5. Phase 5: UI Refinement
    
    - Review and refine UI based on user feedback and testing
        
    - Implement any necessary adjustments to improve user experience
        

## Future Considerations

1. Integration with pro forma invoice solution
    
2. Enhanced analytics and forecasting capabilities
    
3. Mobile app for on-the-go schedule management
    

## Change Log

- Updated UI/UX overview to include new line placement and completed event display
    
- Modified Invoice Schedule Events custom record structure
    
- Updated Invoice Trigger functionality to include automatic checkbox updates
    
- Expanded Trigger Type options and added Event Trigger sub-record details
    
- Clarified integration with existing NetSuite records
    
- Added information on custom field creation for Invoice Schedule Events record
    
- Included new phase for UI refinement in Implementation Phases
    

## Meeting Transcripts

Be the first to add a reaction