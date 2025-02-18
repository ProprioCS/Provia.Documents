- 1 [Technical Specifications](#Technical-Specifications)
    - 1.1 [Object Definitionsn](#Object-Definitionsn)
        - 1.1.1 [Orion Project - custom record](#Orion-Project---custom-record)
        - 1.1.2 [Data Design](#Data-Design)
    - 1.2 [Scripts and Automations](#Scripts-and-Automations)
- 2 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 2.1 [Unit Tests](#Unit-Tests)
    - 2.2 [Process Tests](#Process-Tests)
- 3 [Time Estimate](#Time-Estimate)
- 4 [Changes And Revisions](#Changes-And-Revisions)

**Solution Overview:**  
The NetSuite Project Management Module for Contract Furniture Dealers is a comprehensive solution designed to enhance visibility, reporting, and navigation capabilities for projects while supporting project management functionalities and accurate commission calculations. The Project record serves as the central hub, featuring a smart table design with key performance indicator (KPI) cards at the top for quick insights. The left navigation panel offers filters and views for easy data access, while the right pane displays related records such as tasks, emails, and files associated with the project.

This module enables dealers to efficiently manage projects, track costs, and ensure accurate commission recognition. It provides a unified view of all project-related communications, time entries, and item-level costing details, facilitating better decision-making and financial control.

**Solution Title: NetSuite Project Management Module for Contract Furniture Dealers**

Solution Type: **Module**

User Stories:

1. As a project manager, I want to view all project-related communications, tasks, and files in one place, so that I can easily navigate and manage project activities.
    
2. As a sales manager, I want to accurately track project costs and margin erosion, so that I can ensure proper commission calculations and financial reporting.
    
3. As an executive, I want to access key project metrics and KPIs through a dashboard, so that I can quickly assess project health and make informed decisions.
    

Success Metrics:

1. Reduction in time spent navigating between project-related records and transactions
    
2. Increase in accuracy of commission calculations and financial reporting
    
3. Improved project management efficiency and resource allocation
    
4. Enhanced visibility into project health and performance
    
5. Reduction in manual effort required for project cost tracking and reconciliation
    

Design:  
[Project Record](https://www.figma.com/file/aSkJbiIS2ACXRuhCTbql4X/Project-Record?type=design&node-id=1%3A1318&mode=design&t=lfFIFOL8Ke60eKoa-1)

![Screenshot 2024-06-10 130930.png](blob:https://suitecentric.atlassian.net/b2e8242e-140d-4f82-b73e-7f717989894d#media-blob-url=true&id=8876475f-d9f5-4f22-a299-3b141dff27f2&collection=contentId-2260041732&contextId=2260041732&width=473&height=196&alt=Screenshot%202024-06-10%20130930.png)

- The Project record will feature an admin-style screen layout with a smart table design. KPI cards at the top will display key project metrics.
    
- FUTURE: The left navigation panel will provide filters and quick views to easily access different subsets of data.
    
- The main table will display project transactions with the ability to add/remove columns and filter data. Clicking on a transaction will open a right pane with additional details and related records like tasks and emails. View options will include communication records, time entries, and detailed item-level cost breakdowns.
    
- Creation of new related records like tasks will be supported
    
- The project navigation module will be a subset of this record and will show up on the related record tab of other transaction types, tying all related transactions together
    

Roles and Permissions:

- Orion – Executive leadership: View only access to project KPIs, dashboards, and reports
    
- Orion - Sales Leadership: View access to all project data, edit access to update forecasts and targets
    
- Orion – Salesperson/Account Manager: View/edit access to own projects, view access to team projects
    
- Orion - Sales Support: View access to all project data to assist sales team
    
- Orion - Design Manager: View/edit access to all project data to manage design resources and timelines
    
- Orion - Designer: View/edit access to own assigned tasks and time entries
    
- Orion - Purchasing: View access to all project data, edit access for item procurement
    
- Orion - Procurement: View access to item data, edit access to create purchase orders
    
- Orion - Ops Manager: View/edit access to all project data to manage resources and timelines
    
- Orion - Project Manager: Full access to assigned projects to manage end-to-end delivery
    
- Orion - Inventory Manager: View access to all project data, edit access to update inventory allocations
    
- Orion - Warehouse Manager: View access to project data, manage receiving and fulfillment
    
- Orion - Accounting Manager: Full view access to all project financial data for reporting
    
- Orion - Controller/CFO: Full view/edit access to all project financial data
    

Features and Functionality:

- Auto Create a Project for every Opportunity on save of the Opp
    
- Project can have parent child relationships
    
- KPI cards displaying key project metrics like revenue, costs, margin, billing
    
- Left navigation for quick filters and views by transaction type, vendor, customer, status
    
- Smart table displaying project transactions with inline editing of key fields
    
- Right pane to view/edit related records like tasks, emails, notes associated with a transaction
    
- Communication view displaying all project-related messages and activities
    
- Time entry view with daily and weekly totals by employee, ability to enter and approve time
    
- Item detail view breaking down estimated vs actual costs and quantities across transactions
    
- Automated project and task creation from sales order approval
    
- Alerts for at-risk items like delayed shipments, change orders, or cost overruns
    
- Reports for project health, cost breakdown, resource utilization, AP/AR aging, and more
    
- Interactive Gantt chart for project schedule visualization (future enhancement)
    
- Project status will be displayed in a similar method that a sales order would show status seen in the screenshot in this doc
    
- ==Components==
    
    - Primary Section
        
        - Project Name
            
        - Number
            
        - Customer
            
        - Genesis Sales Order
            
    - KPI Cards
        
        - Based on Saved searches (adminable)
            
        - WIP Balance
            
        - Accrued AP Balance
            
        - Inventory Asset Balance
            
        - Cash Balance
            
        - Gross Profit $
            
        - Gross Profit %
            
        - Commissionable Gross Profit $
            
        - Commissionable Gross Profit %
            
        - Backlock GP$
            
        - Backlog GP%
            
        - Margin Erosion $
            
        - Margin Erosion %
            
        - Overhead Fee$
            
        - Overhead Fee %
            
    - Smart Table
        
        - Views
            
            - Transactions
                
                - Time Entries
                    
                - Projects
                    
            - Registers
                
                - WIP Register
                    
                - IRNB Register
                    
                - Item Audit
                    
                - Cash Register
                    
            
            - Discrepancies
                
                - Punch
                    
                - Ack Discrepancies
                    
                - Cost Verification Discrepancies
                    
            - Tasks - Across all transactions, showing trans#
                
                - Editable
                    
                - Add New, assigns directly to project record
                    
            - Communications
                
                - Emails
                    
                - Phone Calls
                    
                - User Notes
                    
            - Calendar view of events ![Question Mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/atlassian/productivityEmojis/question-64px.png)
                
            - Files (across transactions)
                
        - Reports (Summary Views)
            
            - Transactions Totals
                
                - Sales Orders
                    
                - Purchase Orders
                    
                - Vendor Bills
                    
                - Item Receipts
                    
                - Customer Invoices
                    
                - Adjustments
                    
            - Vendor Summary
                
            - Budget vs Actual
                
        - Agreement Types
            

|   |   |   |
|---|---|---|
|**Progress Invoicing**|**Action**|**Formula**|
|Invoice Generated|Commisison Calculated and Commission Payment Record Created|GP of lines on Invoice|
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
|Project Reopened|||
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
||||
|**Progress Invoice Payments**|||
|Invoice Lines are Paid|Commisison Calculated and Commission Payment Record Created|GP of lines on Invoice|
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
|Project Reopened|||
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
||||
|**Order Invoiced in Full**|||
|All lines invoiced|Commisison Calculated and Commission Payment Record Created|Project GP  - all actual sell and estimated and actual costs|
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
|Project Reopened|||
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
||||
|**Paid Order**|||
|All Invoices Paid|Commisison Calculated and Commission Payment Record Created|Project GP  - all actual sell and estimated and actual costs|
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|
|Project Reopened|||
|Project Complete|Commisison Calculated and Commission Payment Record Created|Project GP - all actual sell and costs less paid commission|

Technical Considerations:

- The project record will be a custom record named Orion Project
    
- Use SuiteScript to automate project creation at the time of Quote or Opp - this should be configurable
    
- Develop saved searches to power KPI cards, reports, and dashboard charts - SuiteQL?
    
- Ensure project architecture can scale to handle up to 2500 line items per project
    
- Use standard NetSuite permissions and roles to control record-level access
    
- Consider performance impact of detail item cost view with high transaction volumes
    
- Each status will refer to a number of criteria, and Marcus created a query field to the project status record so we can write the queries right there for each status, making it adminable during onboarding and also later by the customer
    

Testing and Quality Assurance:

- Test Script Title: NetSuite Project Management Module Test Script
    
- Test Objectives:
    
    1. Validate that project records are automatically created from approved sales orders
        
    2. Confirm that actual costs are accurately aggregated and allocated to projects
        
    3. Verify that project KPIs, reports and detail views match source transactions
        
- Test Environment: Sandbox with demo data migrated from legacy systems
    
- Test Data: Sample project records with sales orders, purchase orders, items across product categories, multiple cost and billing types
    
- Test Steps:
    
    1. Create test sales orders in various statuses and verify project records created
        
    2. Receive inventory against purchase orders and confirm costs roll up to project
        
    3. Apply vendor bill to purchase order and validate project costs and margin update
        
    4. Enter time entries for tasks and verify correct hours are logged to project
        
    5. Generate and review project KPI cards, detail views, and financial reports
        
- Test Assertions:
    
    1. Project is automatically created when sales order reaches approved status
        
    2. All actual costs are accurately captured on project record
        
    3. Time entries are included in project cost and resource reporting
        
    4. Costs are properly allocated to projects via purchase orders and item receipts
        
    5. Project reports and views reconcile to source transactions
        
- Test Metrics:
    
    1. Number of project records created vs number of approved sales orders
        
    2. Project costs reported vs total costs from item-level detail
        
    3. Resource hours logged to project vs total hours entered on related time cards
        
- Test Execution:
    
    1. Manually create projects and source transactions per test case
        
    2. Validate project creation and cost aggregation using saved searches
        
    3. Compare project reports to transaction detail using SuiteAnalytics Workbook
        
- Test Results: Document expected and actual values for each test assertion
    
- Defect Reporting: Log defects in Jira, categorize by severity (Critical, High, Medium, Low)
    
- Test Script Approval: Review with project team, key stakeholders prior to acceptance testing
    

In summary, the NetSuite Project Management module enables contract furniture dealers to streamline project delivery, improve financial visibility, and drive more accurate commissions. The unified interface allows quick access to all project-related data, while the smart table and KPI cards provide actionable insights. Automated cost aggregation and allocation ensures "one version of the truth," while flexible reporting and permissions support the needs of different dealer roles.

Key technical considerations include optimizing the data architecture for performance at scale, leveraging native NetSuite customization and scripting capabilities wherever possible, and thorough testing of all project tracking and financial roll-up logic. A phased implementation approach is recommended, gradually exposing features to pilot groups and incorporating user feedback.

With this module in place, contract furniture dealers can manage projects more efficiently, improve cross-functional collaboration, and make proactive data-driven decisions. This supports key business goals around margin improvement, customer satisfaction, and overall operational excellence.

## Technical Specifications

## Object Definitionsn

### Orion Project - custom record

### Data Design

## Scripts and Automations

## Testing and Quality Assurance

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

1. Change 1
    
    1. Details
        
2. Change 2
    
    1. Details
        

Be the first to add a reaction