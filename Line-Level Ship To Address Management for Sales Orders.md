- 1 [Overview](#Overview)
- 2 [User Stories](#User-Stories)
- 3 [Success Metrics](#Success-Metrics)
- 4 [Solution Type: Utility](#Solution-Type%3A-Utility)
- 5 [Design](#Design)
    - 5.1 [UI/UX design:](#UI%2FUX-design%3A)
- 6 [Roles and Permissions:](#Roles-and-Permissions%3A)
- 7 [Features and Functionality](#Features-and-Functionality)
- 8 [Technical Considerations](#Technical-Considerations)
- 9 [Technical Specifications](#Technical-Specifications)
    - 9.1 [Object Definitions](#Object-Definitions)
    - 9.2 [Data Design](#Data-Design)
    - 9.3 [Scripts and Automations](#Scripts-and-Automations)
- 10 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 10.1 [Unit Tests](#Unit-Tests)
    - 10.2 [Process Tests](#Process-Tests)
    - 10.3 [Reporting and Analysis](#Reporting-and-Analysis)
    - 10.4 [Conclusion](#Conclusion)
- 11 [Time Estimate](#Time-Estimate)

## **Overview**

While there will be a main Ship To Address for the sales order – such as a warehouse address where the products are being received, stored temporarily, and staged for delivery and installation to the customer, there is also a need for a _**line level ship to address**_ where an item is being shipped to an alternate address on a Vendor Purchase Order.

Vendors require a single PO per ship to address.

The most common scenario for this _**line level ship to address**_ is when a COM (Customer’s Own Material) or COL (Customer’s Own Leather) is being purchased by the dealer and shipped to the sofa/chair manufacturer to be applied to the item before the assembled item is shipped to the dealer warehouse.

In the example for a COM line, the fabric is ordered from a fabric manufacturer and then shipped to a furniture manufacturer’s COM address with detailed purchase order instructions to complete the item to the customer’s specifications. Each COM fabric that is shipping to a different manufacturer would need to be on its own unique purchase order - there is a 1:1 relationship in contract furniture between PO# and Ship To Address. (For example, I may be ordering 3 different fabrics from Maharam - but if they are to be applied to chairs from Bernhardt, Nucraft, and Via - they need to be on 3 different POs).

There are other scenarios where a specific line will be shipped to a different address than the main order Ship To Address. The solution needs to be flexible enough for all considerations when a dealer needs to select a specific address for a line on an order: Customer Address, Vendor Address, or Location Address.

## User Stories

1. As a Sales Admin, I want to be able to select the correct vendor and vendor address for a line on a sales order. If the line item will be shipped to a customer or other address in my NetSuite account, I want to be able to select an address for those options as well.
    
2. As a Procurement person, I want to be able to easily identify the shipping address for each line item on a sales order when creating purchase orders, so that I can ensure the accuracy of our POs and streamline the ordering process.
    

## Success Metrics

1. Reduction in shipping errors: Track the percentage decrease in shipping errors related to incorrect shipping addresses on sales order line items after implementing the utility.
    
2. Time saved in order processing: Measure the average time saved per order by allowing users to easily select the correct shipping address for each line item, compared to the time taken before implementing the utility.
    
3. Improved order accuracy: Monitor the percentage increase in orders with accurate shipping addresses for all line items, leading to fewer customer complaints and returns.
    

## Solution Type: Utility

## Design

### UI/UX design:

1. Address Field on Sales Order Line: Add a new field called "Line Ship To Address" on each line item within the Sales Order Smart Table. This field will allow users to select the appropriate shipping address for that specific line item. If no address is selected at the line level, the default Ship To Address from the sales order will be automatically applied.
    
2. Address Selection Dropdown: When a user clicks on the "Line Ship To Address" field, a dropdown menu should appear, displaying the following options:  
    a. Customer Addresses: Display a list of all available customer addresses associated with the selected customer on the sales order.  
    b. Vendor Addresses: Display a list of all available vendor addresses based on the vendor selected for the line item.  
    c. Other Addresses: Allow users to select from a list of other predefined addresses in the NetSuite account, such as warehouse locations or staging areas.
    
3. Address Search and Filtering: Implement a search and filtering functionality within the address selection dropdown to help users quickly find and select the desired address, especially when dealing with a large number of addresses.
    
4. Address Validation: Include a validation mechanism to ensure that the selected address is complete and properly formatted before saving the changes to the line item.
    
5. PO Selection Utility Integration: When generating purchase orders using the PO Selection Utility, group line items based on their selected "Line Ship To Address" to create separate POs for each unique shipping address. Line items without a specified address will use the default Ship To Address from the sales order.
    
6. Visual Indicators: Use visual cues, such as icons or color-coding, to clearly differentiate line items with a line-level address within the Smart Table. This will help users quickly identify and manage line items where the shipping address differs from the default. Leave the "Line Ship To Address" field blank for lines using the default address to keep the Smart Table cleaner and easier to read.
    
7. Tooltips and Help Text: Provide tooltips and help text throughout the utility to guide users on how to use the "Line Ship To Address" field effectively and understand its impact on the PO Selection Utility. Clearly explain that leaving the field blank will result in the default Ship To Address being used for that line item.
    

## **Roles and Permissions:**

1. Orion - Salesperson/ Account Manager
    
    - Access Level: Edit
        
    - Permissions: Can view and edit the "Line Ship To Address" field on sales order line items for their assigned orders.
        
2. Orion - Sales Admin
    
    - Access Level: Edit
        
    - Permissions: Can view and edit the "Line Ship To Address" field on sales order line items for all orders.
        
3. Orion - Procurement
    
    - Access Level: Edit
        
    - Permissions: Can view and edit the "Line Ship To Address" field on sales order line items for all orders.
        

These three roles should have the necessary access to effectively use the Line-Level Ship To Address Management utility within their respective responsibilities.

Additionally, consider the following roles that may require view-only access to the "Line Ship To Address" field:

4. Orion - Sales Leadership
    
    - Access Level: View
        
    - Permissions: Can view the "Line Ship To Address" field on sales order line items for all orders, but cannot make changes.
        
5. Orion - Ops Manager
    
    - Access Level: View
        
    - Permissions: Can view the "Line Ship To Address" field on sales order line items for all orders, but cannot make changes.
        
6. Orion - Project Manager
    
    - Access Level: View
        
    - Permissions: Can view the "Line Ship To Address" field on sales order line items for their assigned projects, but cannot make changes.
        

These view-only permissions ensure that relevant stakeholders can access the line-level shipping address information without the ability to modify it.

## Features and Functionality

- Addition of a "Line Ship To Address" field on each line item within the Sales Order Smart Table
    
- Dropdown menu for selecting the appropriate shipping address for each line item, with options for Customer Addresses, Vendor Addresses, and Other Addresses
    
- Automatic application of the default Ship To Address from the sales order if no line-level address is specified
    
- Search and filtering functionality within the address selection dropdown for quick and easy address selection
    
- Validation mechanism to ensure the completeness and proper formatting of selected addresses
    
- Integration with the PO Selection Utility to group line items based on their selected "Line Ship To Address" and create separate POs for each unique shipping address
    
- Visual indicators, such as icons or color-coding, to clearly differentiate line items with a line-level address within the Smart Table
    
- Tooltips and help text to guide users on the usage and impact of the "Line Ship To Address" field
    
- Role-based access control, allowing Salespersons, Sales Admins, and Procurement users to edit the "Line Ship To Address" field, while providing view-only access to Sales Leadership, Ops Managers, and Project Managers
    

## Technical Considerations

Key technical points and constraints to consider:

1. This will have impact on the Purchase Order Creation utility. The Vendor PO must be segmented by Ship To Address - one PO per address only.
    
2. NetSuite Version Compatibility: Ensure that the utility is compatible with the version of NetSuite used by your organization. The utility should be developed and tested against the specific NetSuite release to avoid any compatibility issues.
    
3. Custom Field Creation: A new custom field, "Line Ship To Address," needs to be created and added to the Sales Order line item record. This field should be configured as a dropdown list, with the appropriate address options sourced from Customer, Vendor, and Other Address records.
    
4. Smart Table Integration: The "Line Ship To Address" field must be seamlessly integrated into the Sales Order Smart Table. Ensure that the field is properly displayed, editable, and functions as expected within the Smart Table interface.
    
5. Once a Vendor Purchase Order has been created, the line-level ship to address should not be editable, read only access will exist for all roles/permissions. If this address needs to be edited after purchase order creation and PO has NOT been communicated to the vendor - the PO would be deleted and then the address could be updated.
    
    1. Batch mode/bulk edits should also be considered to not allow editing to the line level ship to address.
        
6. Address Record Integration: The utility should establish connections with the existing Customer, Vendor, and Other Address records in NetSuite. It should be able to fetch and display the relevant addresses in the dropdown list based on the selected line item's context.
    
7. PO Selection Utility Integration: The Line-Level Ship To Address Management utility should interface with the PO Selection Utility to enable the grouping of line items based on their selected shipping addresses. Ensure that the necessary data is passed between the two utilities to facilitate accurate PO creation.
    
8. Performance Optimization: As the utility will be used within the Sales Order Smart Table, it is crucial to optimize its performance to avoid any slowdowns or delays in the user experience. Implement efficient data retrieval and caching mechanisms to minimize the impact on Smart Table load times.
    
9. Error Handling and Logging: Implement robust error handling and logging mechanisms to capture and report any issues or exceptions that may occur during the utility's operation. This will aid in troubleshooting and maintaining the utility's stability.
    
10. Security and Access Control: Ensure that the utility adheres to NetSuite's security best practices and implements appropriate role-based access control. Only authorized users should be able to view and modify the "Line Ship To Address" field based on their assigned permissions.
    

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

Test Script Title: Line-Level Ship To Address Management for Sales Orders Test Script

Test Objectives:

1. Verify the functionality and usability of the "Line Ship To Address" field on the Sales Order line items.
    
2. Ensure the accurate integration and data flow between the utility and the Sales Order Smart Table, PO Selection Utility, and relevant address records.
    

Test Environment:

- NetSuite Sandbox account with the Line-Level Ship To Address Management utility installed and configured.
    

Test Data:

- Sample Sales Orders with multiple line items.
    
- Customer, Vendor, and Other Address records for selection.
    

Test Steps:

1. Create a new Sales Order and add multiple line items.
    
2. For each line item, select a different shipping address using the "Line Ship To Address" dropdown field.
    
3. Save the Sales Order and verify that the selected addresses are correctly associated with their respective line items.
    
4. Use the PO Selection Utility to generate Purchase Orders based on the Sales Order.
    
5. Verify that the line items are grouped correctly based on their selected shipping addresses, and separate POs are created for each unique address.
    

Test Assertions:

1. The "Line Ship To Address" field is visible and editable on each Sales Order line item.
    
2. The dropdown list for the "Line Ship To Address" field contains the expected Customer, Vendor, and Other Address options.
    
3. The selected shipping addresses are correctly saved and associated with their respective line items.
    
4. The PO Selection Utility accurately groups line items based on their selected shipping addresses and creates separate POs for each unique address.
    
5. Users with the appropriate roles and permissions can view and edit the "Line Ship To Address" field, while unauthorized users cannot access or modify the field.
    

Test Metrics:

1. Defect Density: Track the number of defects found during testing relative to the utility's size and complexity.
    
2. User Acceptance: Measure the percentage of users who find the utility intuitive, efficient, and reliable during User Acceptance Testing (UAT).
    

Test Execution:

- Execute the test script in the NetSuite Sandbox environment.
    
- Record the actual results for each test step and compare them against the expected results.
    
- Document any discrepancies or issues encountered during the testing process.
    

Test Results:

- Compile the test results, including the actual outcomes, any defects or issues found, and their respective severities.
    
- Evaluate the overall quality and reliability of the Line-Level Ship To Address Management utility based on the test results.
    

Defect Reporting:

- Report any defects or issues found during testing to the development team.
    
- Categorize the defects based on their severity and impact on the utility's functionality and user experience.
    
- Track the defect resolution progress and retest the utility once the fixes are implemented.
    

Test Script Approval:

- Review the test script with the relevant stakeholders, including the development team, product owner, and quality assurance team.
    
- Obtain approval from all stakeholders before commencing the testing process.
    
- Ensure that the test script covers all the critical aspects of the Line-Level Ship To Address Management utility and aligns with the defined requirements and specifications.
    

## Unit Tests

## Process Tests

## **Reporting and Analysis**

## **Conclusion**

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development|0|
|NetSuite Setup|0|
|QA|0|
|**Total**|**0**|

Be the first to add a reaction