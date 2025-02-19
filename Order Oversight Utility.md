- 1 [Overview](#Overview)
    - 1.1 [Key Benefits](#Key-Benefits)
    - 1.2 [Solution Type](#Solution-Type)
    - 1.3 [User Stories](#User-Stories)
- 2 [Success Metrics](#Success-Metrics)
- 3 [Design](#Design)
- 4 [Features and Functionality](#Features-and-Functionality)
- 5 [Technical Specifications](#Technical-Specifications%5BhardBreak%5D)
    - 5.1 [Object Definitions](#Object-Definitions)
    - 5.2 [Data Design](#Data-Design)
    - 5.3 [Scripts and Automations](#Scripts-and-Automations)
- 6 [Testing Process](#Testing-Process)
    - 6.1 [Unit Tests](#Unit-Tests)
    - 6.2 [Process TestsSample Test Script: Provia Quote Approval Workflow](#Process-Tests%5BhardBreak%5DSample-Test-Script%3A-Provia-Quote-Approval-Workflow)
- 7 [Time Estimate](#Time-Estimate)

## Overview

The Provia Quote Approval Workflow is a customized solution designed to streamline and automate the quote approval process for contract furniture dealers using NetSuite. This solution enables sales representatives to easily submit quotes for approval, route them to the appropriate approvers based on predefined criteria, and track the approval status throughout the process. By implementing this workflow, contract furniture dealers can ensure that quotes are reviewed and approved by the necessary stakeholders before being sent to clients, reducing the risk of errors, inconsistencies, and potential loss of revenue due to low margins.

## Key Benefits

- Enhanced control and visibility over the quote approval process
    
- Automated routing of quotes to the appropriate approvers based on predefined criteria
    
- Real-time tracking of approval status for all stakeholders
    
- Automated notifications and reminders to ensure timely approvals
    
- Improved collaboration between sales and accounting teams
    

## Solution Type

The Provia Quote Approval Workflow is classified as a Customization, as it involves creating custom fields, buttons, and workflows within the standard NetSuite environment to meet the specific requirements of the contract furniture industry.

## User Stories

As a sales manager, I want to approve quotes to ensure that only quotes with proper pricing and appropriate margins are sent to customers.

As an accounting or finance person, I want to verify that quotes are only sent to approved prospects or customers and that the margins on the quotes are acceptable before they are sent.

As a sales representative, I want to easily submit quotes for approval and track their status, so that I can efficiently manage my sales pipeline and keep my customers informed.

## Success Metrics

- Reduction or elimination of quotes being sent to customers with low margins or obvious errors
    
- Reduction in time taken to submit and approve quotes
    
- Increase in the percentage of quotes that are approved by both sales management and accounting
    
- Improved visibility and tracking of the quote approval process for all stakeholders
    
- Enhanced collaboration and communication between sales and accounting teams
    

## Design

==The email template for notifying the sales rep (and potentially the order team) upon quote approval is the main item that needs to be defined and created.==

==The Provia Quote Approval Workflow primarily relies on standard NetSuite functionality and UI/UX components, requiring no unique design considerations beyond the normal SuiteFlow capabilities.==

## ==Features== and Functionality

- Custom "Submit for Approval" button on the quote record to initiate the approval process
    
- Custom "Approval Status" field on the quote record to track the current status of the approval process, with the following status options:
    
    1. Pending Submission
        
    2. Submitted
        
    3. Initially Approved - Sales MGMT Approval
        
    4. Initially Rejected
        
    5. Accounting Approved
        
    6. Accounting Rejected
        
    7. Fully Approved
        
- Custom "Approver" field on the quote record to assign and track the current approver
    
- Automated assignment of approvers based on predefined criteria (e.g., project association, sales rep's supervisor)
    
- Automated email notifications to relevant stakeholders at each stage of the approval process:
    
    - Sales rep receives notifications for:
        
        - Submitted
            
        - Initially Approved - Sales MGMT Approval
            
        - Initially Rejected
            
        - Accounting Approved
            
        - Accounting Rejected
            
        - Fully Approved
            
    - Sales manager (supervisor) receives notifications for:
        
        - Submitted
            
    - Accounting team receives notifications for:
        
        - Initially Approved - Sales MGMT Approval
            
- Reminder portlets for approvers to view and take action on pending approvals
    
- Customizable workflow to manage the approval process, including routing, notifications, and status updates
    
- Saved searches to populate reminder portlets and track quotes pending approval
    
- Custom list to populate the "Approver" drop-down field
    
- Custom list to populate the "Approval Status" drop-down field
    
- Development of a SuiteFlow workflow to manage the entire quote approval process, including routing, notifications, and status updates
    
- "My Quotes Pending Approval" dashboard portlet for sales reps to track their submitted quotes
    

## Technical Specifications

- The Quote Approval Workflow will primarily rely on SuiteFlow workflows, but there is a discussion point to explore with Luke whether using SuiteScript instead could improve system performance.
    
- No existing NetSuite customizations have been identified that would require integration with the Quote Approval Workflow.
    
- Performance and scalability considerations for handling large volumes of quotes efficiently should be discussed with Luke.
    
- The solution proposes using the "Supervisor" field on the sales rep record and a specific role for approvers, rather than assigning specific individuals.
    
- There is an open discussion point to evaluate the option of allowing dealers to manage approvers through a workflow parameter or custom record, pending confirmation with Catherine.
    

## Object Definitions

## Data Design

## Scripts and Automations

## Testing Process

## Unit Tests

## Process Tests  
Sample Test Script: Provia Quote Approval Workflow

Objective: Validate the functionality, performance, and user experience of the Provia Quote Approval Workflow.

Prerequisites:

1. NetSuite environment with the Provia Quote Approval Workflow customization installed and configured
    
2. Test data:
    
    - Sales rep user account
        
    - Sales manager user account (supervisor of the sales rep)
        
    - Accounting team user account
        
    - Sample customer records
        
    - Sample project records (if applicable)
        
3. Access to email inbox for receiving notifications
    

Test Steps:

1. Log in to NetSuite as a sales rep user
    
2. Navigate to the quote record and create a new quote for a customer
    
3. Fill in the necessary quote details, including items, quantities, and prices
    
4. Click the "Submit for Approval" button on the quote record
    
5. Verify that the "Approval Status" field changes to "Submitted"
    
6. Check the email inbox associated with the sales rep user and confirm receipt of a submission notification
    
7. Log out of NetSuite and log in as the sales manager user (supervisor)
    
8. Navigate to the dashboard and locate the "Quotes Pending Approval" portlet
    
9. Verify that the submitted quote appears in the portlet
    
10. Click on the quote link in the portlet to open the quote record
    
11. Review the quote details and click the "Approve" button
    
12. Verify that the "Approval Status" field changes to "Initially Approved - Pending Accounting Approval"
    
13. Check the email inbox associated with the sales rep user and confirm receipt of an initial approval notification
    
14. Log out of NetSuite and log in as the accounting team user
    
15. Navigate to the dashboard and locate the "Quotes Pending Approval" portlet
    
16. Verify that the initially approved quote appears in the portlet
    
17. Click on the quote link in the portlet to open the quote record
    
18. Review the quote details and click the "Approve" button
    
19. Verify that the "Approval Status" field changes to "Fully Approved"
    
20. Check the email inbox associated with the sales rep user and confirm receipt of a final approval notification
    
21. Log in to NetSuite as the sales rep user and navigate to the "My Quotes Pending Approval" dashboard portlet
    
22. Verify that the fully approved quote no longer appears in the portlet
    

Expected Results:

1. The quote approval workflow follows the defined steps without any errors
    
2. Email notifications are sent to the appropriate users at each stage of the approval process
    
3. Dashboard portlets display accurate information for each user role
    
4. The "Approval Status" field updates correctly at each stage of the workflow
    
5. The "My Quotes Pending Approval" portlet reflects the current status of the sales rep's submitted quotes
    

Actual Results: [To be filled in during testing]

## ==Time Estimate==

|   |   |
|---|---|
||**Hours**|
|Development|16|
|NetSuite Setup|32|
|QA|12|
|**Total**|**60**|

Be the first to add a reaction