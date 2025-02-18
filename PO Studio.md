- 1 [Overview](#Overview)
- 2 [Technical Specifications](#Technical-Specifications)
    - 2.1 [Object Definitions](#Object-Definitions)
    - 2.2 [Data Design](#Data-Design)
    - 2.3 [Scripts and Automations](#Scripts-and-Automations)
- 3 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 3.1 [Unit Tests](#Unit-Tests)
    - 3.2 [Process Tests](#Process-Tests)
- 4 [Time Estimate](#Time-Estimate)
- 5 [Changes And Revisions](#Changes-And-Revisions)

## **Overview**

The PO Generation utility is a NetSuite customization designed to streamline the process of creating purchase orders from selected lines in a sales order smart table. This utility allows users to quickly generate a new purchase order for a specific vendor by selecting the appropriate lines from the sales order and clicking on a dedicated icon in the multi-line edit bar. The selected lines will be automatically transferred to the new purchase order, reducing manual data entry and minimizing the risk of errors. By simplifying the creation of purchase orders, this customization aims to save time, improve accuracy, and enhance overall productivity for contract furniture dealers.

**Solution Title** PO Generation

**Solution Type** Utility

**User Stories**

1. As a project coordinator, I want to create a PO for a vendor. To do this, I filter the smart table for the appropriate lines, select them all, and hit the generate PO button.
    
2. As a project manager, I need to quickly generate purchase orders for specific vendors based on the items in a project. By using the PO Generation utility, I can easily filter the smart table, select the relevant lines, and create a PO with just a few clicks.
    
3. As a customer support representative, I often need to process replacement orders for customers. With the PO Generation utility, I can efficiently locate the needed items in the smart table, select them, and generate a PO to fulfill the replacement request.
    

**Success Metrics**

1. Accuracy: 100% of the selected lines from the smart table are successfully transferred to the newly created purchase order, ensuring no lines are missed or accidentally included.
    
2. Vendor Matching: The generated purchase order consistently associates with the correct vendor based on the selected lines, without any instances of mismatched vendors.
    
3. User Satisfaction: Users report a positive experience with the PO Generation utility, citing ease of use and time savings compared to manual PO creation.
    

**Design (UI/UX overview)**

- A new icon will be added to the multi-edit bar associated with the right panel in the NetSuite smart table interface.
    
- The icon will be grayed out by default and will only become active when the following conditions are met:
    
    - The user is in view mode on the sales order.
        
    - The user has selected lines that belong to the same vendor.
        
- If the user clicks on the grayed-out icon, a pop-up message will appear, indicating the reason for the icon being inactive:
    
    - If the user is not in view mode, the message will prompt them to switch to view mode.
        
    - If the selected lines have multiple vendors, the message will inform the user that they can only generate a PO for a vendor at a time.
        
- When the icon is active and clicked, it will trigger the generation of a new purchase order for the selected vendor, with the selected lines pre-populated and ready for editing.
    

**Roles and Permissions** The PO Generation utility will leverage NetSuite's existing role-based access control system. The permissions to access and use this utility will be determined by the user's assigned NetSuite role and their corresponding permissions for creating and editing purchase orders. No additional role-specific permissions need to be configured for the Orion user roles listed. The developer will need to ensure that the utility respects the user's existing NetSuite role permissions and only allows access to users with the appropriate permissions.

**Features and Functionality**

- Automatic header information transfer:
    
    - When the user initiates the PO Generation utility, the system will create a new purchase order and automatically populate the header information based on the corresponding sales order.
        
    - The newly created purchase order will open in edit mode, allowing the user to make any necessary adjustments.
        
- Line item transfer:
    
    - The selected lines from the sales order smart table will be transferred to the purchase order's item sublist.
        
    - The smart table on the purchase order transaction will be adapted to display relevant information for purchase orders, with a different default quick view and a list of quick views specific to purchase orders.
        
    - The smart table on the purchase order will still include data such as sell price and gross profit, which are not natively available in NetSuite for purchase orders.
        
- Summary item creation:
    
    - The system will create summary items in the purchase order's item sublist based on the smart table's JSON data.
        
    - The summary lines on the purchase order will be similar to the summary lines on the sales order, but will exclude the sell price, as NetSuite does not support this natively on purchase orders.
        
    - The sell price will still be available in the smart table on the purchase order, but not in the defaulted view.
        
- User actions:
    
    - After the purchase order is generated and populated with the selected lines and summary items, the user will review and make any necessary edits.
        
    - The user will need to manually save the purchase order once they have completed any additional modifications.
        

**Testing and Quality Assurance** _Test Script Title:_ PO Generation Test Script

_Test Objectives:_

1. Verify that the PO Generation utility correctly transfers the selected line items from the sales order to the new purchase order.
    
2. Ensure that the generated purchase order opens in edit mode with the selected lines populated in the PO smart table.
    
3. Confirm that upon saving the purchase order, the summary lines are accurately written to the transaction.
    

_Test Environment:_

- The testing will be conducted in either the designated SDN (Software Development Network) account or the SuiteCentric dev account, at the discretion of the developer.
    

_Test Data:_

- A sales order with multiple line items associated with different vendors.
    
- Specific line items on the sales order that will be selected for PO generation.
    

_Test Steps:_

1. Navigate to a sales order in view mode.
    
2. Set the desired view and filter the line items.
    
3. Select the appropriate line items associated with a vendor.
    
4. Click on the "Generate PO" icon in the multi-edit bar.
    
5. Verify that the user is redirected to a new purchase order in edit mode.
    
6. Confirm that the selected lines from the sales order are populated in the PO smart table.
    
7. Save the purchase order.
    
8. Verify that the summary lines are accurately written to the transaction.
    

_Test Assertions:_

1. The correct line items from the sales order are transferred to the new purchase order, ensuring that no lines are missing or incorrectly included.
    
2. The summary lines on the purchase order are correctly created, accurately reflecting the data from the transferred line items.
    
3. The dollar amounts in the summary lines match the expected values based on the selected line items from the sales order.
    

_Test Execution:_

- The testing will be conducted manually by following the defined Test Steps.
    
- The tester will use the appropriate NetSuite environment (SDN account or SuiteCentric dev account) to execute the test cases.
    
- The tester will document any discrepancies between the actual results and the expected results.
    

_Defect Reporting:_

- Any defects or issues encountered during testing should be reported as bugs in JIRA.
    
- The tester will create detailed bug reports, including steps to reproduce the issue, expected behavior, and actual behavior.
    
- The bug reports should include relevant screenshots or videos to help developers understand and reproduce the issue.
    

_Test Script Approval:_

- The Test Script will be reviewed and approved by the designated project stakeholders.
    
- Reviewers will ensure that the Test Script covers all the necessary test cases and aligns with the requirements of the PO Generation utility.
    
- Any feedback or suggestions from reviewers will be incorporated into the Test Script before final approval.
    

## Technical Specifications

## Object Definitions

## Data Design

[https://www.figma.com/design/9uSk06aKTHmgerBNDOBNSE/PO-Generators?node-id=25%3A946&t=RU7TvWediy1urn1Q-1](https://www.figma.com/design/9uSk06aKTHmgerBNDOBNSE/PO-Generators?node-id=25%3A946&t=RU7TvWediy1urn1Q-1)

## Scripts and Automations

## Testing and Quality Assurance

1. Validate functionality and usability
    
2. Ensure accuracy and reliability
    
3. Verify proper handling of PO deletion scenarios
    

Test Environment:

- NetSuite Sandbox environment
    

Test Data:

- Representative sample of sales orders, vendors, custom fields
    

Test Steps:

1. Navigate to Smart Table and locate PO Break feature
    
2. Apply filters to select order lines
    
3. Tag selected order lines for future PO generation
    
4. Initiate PO generation process using the wizard
    
5. Delete generated POs and verify updates and notifications
    

Test Assertions:

1. PO Break feature is easily accessible
    
2. Filtering and tagging functionalities work as expected
    
3. PO generation process creates accurate POs
    
4. Deleting a generated PO updates linked sales order lines and sends notifications
    
5. Audit trail captures all relevant details
    

Test Metrics:

1. Percentage of test cases passed
    
2. Time taken to generate POs compared to manual process
    
3. User satisfaction rating
    

Test Execution:

- Execute test script in NetSuite Sandbox environment
    
- Record results and observations
    

Test Results:

- Document actual results and compare against expected results
    
- Identify discrepancies or issues
    
- Provide summary of test results
    

Defect Reporting:

- Record defects in a defect tracking system
    
- Classify defects based on severity levels
    
- Assign defects to development team for resolution
    

Test Script Approval:

- Review test script with stakeholders
    
- Obtain approval before proceeding with testing
    
- Ensure test script covers all critical aspects and aligns with requirements
    

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