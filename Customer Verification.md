- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
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

The Customer Approval Workflow is designed to facilitate the process of submitting new customers, including leads and prospects, for approval by the accounting team before engaging in business with them. This solution ensures that dealer policies and sound accounting practices are followed, minimizing financial risks and enhancing the overall customer management process.

The workflow allows the Salesperson or Sales Admin to submit a request to the Accounting team to review and approve a potential customer. The Accounting person will review the request and fill in essential details such as the required Deposit percentage and Credit Limit. The solution also incorporates a review process for customers who have been inactive for a specified period (12-24 months, as determined by the dealer during implementation), automatically setting their status to "Pending Approval" or "Pending Review."

Key benefits include:

1. Improved financial control by ensuring that all new customers are vetted and approved by the Accounting team before engaging in business
    
2. Increased efficiency through automated workflows and clear communication channels between Sales and Accounting teams
    
3. Enhanced risk management by regularly reviewing and updating customer approval status based on predefined inactivity periods
    

## Solution Type

·       Customizations – standard netsuite customization including point and click and simple scripts

## User Stories

- As a Salesperson, I want to easily submit new customers for approval so that I can start doing business with them as quickly as possible while ensuring compliance with dealer policies.
    
- As an Accounting Manager, I want to efficiently review and approve new customers, setting appropriate deposit percentages and credit limits, to minimize financial risk and maintain sound accounting practices.
    
- As an Account Coordinator, I want to know when a Customer has been approved by accounting so I can place the order in a timely manner.
    

## Success Metrics

- Reduction in time spent on manual customer approval processes
    
- Increase in the percentage of new customers with properly set deposit requirements and credit limits
    
- Decrease in the number of orders placed for customers without proper approval by X%
    

## Design

1. Clear and intuitive interface for Salespeople and Sales Admins to submit new customers for approval
    
    - Saved search for Salespeople and Sales Admins to view pending approval requests and their status
        
    - Reminder notifications for Salespeople and Sales Admins to follow up on pending approval requests
        
2. Streamlined view for Accounting team members to review, approve, and set deposit percentages and credit limits for new customers
    
    - Saved search for Accounting team members to view pending approval requests and their details
        
    - Reminder notifications for Accounting team members to process pending approval requests within a specified timeframe
        
3. Automated notifications and status updates for relevant stakeholders (e.g., Salespeople, Account Coordinators) throughout the approval process
    
    - Email notifications to Salespeople and Account Coordinators when a customer is approved or rejected
        
    - Saved search for Account Coordinators to view approved customers and their corresponding deposit percentages and credit limits
        
    - Reminder notifications for Account Coordinators to place orders for approved customers
        
4. Customizable dashboard for each role to display relevant information and metrics related to the Customer Approval Workflow
    
    - Dashboard for Salespeople and Sales Admins displaying pending approval requests, average approval time, and approval rate
        
    - Dashboard for Accounting team members displaying pending approval requests, average processing time, and approval/rejection rates
        
    - Dashboard for Account Coordinators displaying approved customers, average time to place an order, and order volume for new customers
        

## Roles and Permissions

- Orion - Sales Leadership: View access to all customer approval requests and dashboards
    
- Orion - Salesperson/Account Manager: Submit new customer approval requests, view their own requests, and receive notifications
    
- Orion - Sales Admin: Submit new customer approval requests, view all requests from their team, and receive notifications
    
- Orion - Accounting Manager: Review and approve/reject customer approval requests, set deposit percentages and credit limits, view all requests and dashboards
    
- Orion - A/R Analyst: Review and approve/reject customer approval requests, set deposit percentages and credit limits, view all requests
    
- Orion - Account Coordinator: View approved customers, receive notifications, and access saved searches for approved customers
    

## Features and Functionality

1. New customer approval request submission process - status field, button, etc for Salespeople and Sales Admins to submit or indicate that a new customer is ready for accounting review for approval 
    

Statuses 

Pending Submission 

Submitted 

Pending Approval 

Revisions Requested 

Approved 

Denied 

2. Automated notification to Accounting team members upon new request submission
    
3. Review and approval/rejection process for Accounting team members
    
4. Customizable deposit percentage and credit limit fields for Accounting team members
    
5. Automated notifications to Salespeople, Sales Admins, and Account Coordinators upon approval/rejection
    
6. Automated status updates throughout the approval process
    
    - Pending Submission
        
    - Pending Approval: Default status for new customer approval requests
        
    - Approved: Status for customers approved by the Accounting team
        
    - Denied
        
    - Pending Review: Status for customers who have been dormant for 12-24 months (customizable timeframe) and require a new review before placing an order
        
    - Credit Hold: Standard NetSuite functionality for customers who have exceeded their credit limit or have become in bad standing due to lack of payment or fraudulent payments
        
7. Customizable saved searches for each role to view relevant requests and customer data
    
8. Automated reminders for pending approval requests and order placement
    
9. Customizable dashboards for each role displaying key metrics and information
    
10. Automated customer status change to "Pending Approval" or "Pending Review" after a specified period of inactivity (12-24 months)
    

## Technical Considerations

- NetSuite Workflow: The Customer Approval Workflow will be built using the standard NetSuite Workflow functionality, which allows for customizable approval processes and automated actions.
    
- Custom Fields: Additional custom fields may need to be created on the Customer record to store information such as approval status, deposit percentage, and credit limit.
    
- Script Development: Custom scripts may be required to handle specific actions or data validation, such as updating the customer status based on inactivity or integrating with the Credit Hold functionality.
    
- Access Controls: Proper access controls and permissions must be set up for each user role to ensure data security and prevent unauthorized actions.
    
- Notifications and Reminders: NetSuite's built-in email notification system will be used to send automated notifications and reminders to relevant users throughout the approval process.
    
- Performance Optimization: To ensure optimal performance, the workflow should be designed efficiently, avoiding unnecessary triggers or actions that could slow down the system.
    
- Customization and Configuration: The Customer Approval Workflow should be designed with flexibility in mind, allowing for easy customization and configuration to accommodate different dealer requirements.
    

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

Test Script Title: Orion Customer Approval Workflow Test Script

Test Objectives:

1. Validate the end-to-end functionality of the Customer Approval Workflow
    
2. Ensure proper access controls and permissions for each user role
    
3. Verify the accuracy of automated notifications, reminders, and status updates
    

Test Environment:

- NetSuite Sandbox account with the Customer Approval Workflow customization installed and configured
    

Test Data:

- Test customer records with various approval statuses and inactivity periods
    
- Test user accounts for each role (Salesperson, Sales Admin, Accounting Manager, A/R Analyst, Account Test Steps:
    
    1. Submit a new customer approval request as a Salesperson and verify the automated notification to the Accounting team
        
    2. Review and approve the customer request as an Accounting Manager, setting the appropriate deposit percentage and credit limit
        
    3. Verify the automated notifications to the Salesperson and Account Coordinator upon approval
        
    4. Test the automated status change to "Pending Review" for a customer with 12-24 months of inactivity
        
    5. Attempt to place an order for a customer on Credit Hold and verify that the system prevents the actionCoordinator)
        

Test Assertions:

1. The Customer Approval Workflow accurately routes approval requests to the appropriate users
    
2. Automated notifications and reminders are sent to the correct recipients at the right times
    
3. User access controls and permissions are enforced throughout the workflow
    
4. Customer statuses are updated accurately based on approval actions and inactivity periods
    
5. Integration with the Credit Hold functionality works as expected
    

Test Metrics:

1. Pass/fail rate for each test case
    
2. Time taken to complete each test step
    
3. Number of defects identified during testing
    

Test Execution:

- Execute the test script in the NetSuite Sandbox environment
    
- Record the results of each test step and any observed issues or defects
    

Test Results:

- Compare the actual results with the expected results for each test step
    
- Document any discrepancies or defects found during testing
    

Defect Reporting:

- Report all defects found during testing, including a description, severity level, and reproduction steps
    
- Severity levels: Critical, High, Medium, Low
    

Test Script Approval:

- Test script to be reviewed and approved by the NetSuite Solution Architect and the client's project stakeholders
    
- Approval criteria: All test objectives are met, and the Customer Approval Workflow functions as intended
    

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