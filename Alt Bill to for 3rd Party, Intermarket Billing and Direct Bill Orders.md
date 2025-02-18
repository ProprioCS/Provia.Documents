- 1 [Orion Alternative Billing Option for 3rd Party, Direct Business, and Intermarket Orders](#Orion-Alternative-Billing-Option-for-3rd-Party%2C-Direct-Business%2C-and-Intermarket-Orders)
- 2 [Technical Specifications](#Technical-Specifications)
    - 2.1 [Object Definitions](#Object-Definitions)
    - 2.2 [Data Design](#Data-Design)
    - 2.3 [Scripts and Automations](#Scripts-and-Automations)
- 3 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 3.1 [Unit Tests](#Unit-Tests)
    - 3.2 [Process Tests](#Process-Tests)
- 4 [Time Estimate](#Time-Estimate)
- 5 [Changes And Revisions](#Changes-And-Revisions)

## Orion Alternative Billing Option for 3rd Party, Direct Business, and Intermarket Orders

Overview:  
The Orion Alternative Billing Option is a flexible and unified solution designed to streamline the billing process for 3rd party, direct business, and intermarket orders within NetSuite. By introducing an "Alternate Bill To" field on Quote and Sales Order records, this solution allows dealers to accurately manage various billing scenarios while ensuring precise AR reporting and maintaining compliance with tax regulations. The key benefits of this solution include:

1. Simplified architecture that consolidates multiple billing scenarios into a single, easy-to-manage solution.
    
2. Accurate financial reporting by automatically updating the customer record on the invoice based on the "Alternate Bill To" field.
    
3. Flexibility to accommodate diverse billing arrangements and order types within a unified framework.
    
4. Customizable warnings or restrictions to enforce best practices and prevent errors based on dealer preferences.
    
5. Consistent tax calculations across sales orders and invoices through tax override functionality.
    

The Orion Alternative Billing Option empowers contract furniture dealers to efficiently handle complex billing requirements, reduce manual effort, and maintain a clear audit trail for all transactions.

Solution Title: Orion Alternative Billing Option

Solution Type: Utility

User Stories:

1. As a project coordinator, I need to set up my project with the appropriate customer on the quote and sales order, which also have the appropriate install address and customer contacts. However, we will be invoicing the general contractor, so I will mark the order type as 3rd Party Billing and identify the appropriate customer record in the "Alternate Bill To" field on the quote. When I go to save the quote, if I did not identify the "Alternate Bill To," I will get a warning from the system asking me if I want to fix it or move on. This will trigger me to fix my mistake, so I don't invoice the wrong customer. Once the invoice is generated, the customer on the invoice will be automatically changed to the GC that I identified in the "Alternate Bill To" field and the install address that was on the sales order, will be added to the GC’s customer record and used on the invoice (we need to test this and see how taxes are calculated)
    
2. As a project coordinator, I need to set up my project with the appropriate customer on the quote and sales order, which also have the appropriate install address and customer contacts. However, we will be invoicing another dealer since this is an intermarket order. An intermarket order is when another MillerKnoll dealer contracts us to install the product for one of their customers. This usually happens when their customer has multiple locations, including a location in my territory. So, I will mark the order type as Intermarket Incoming and identify the intermarket dealer (customer record) as the "Alternate Bill To." This will ensure that I invoice the intermarket dealer. Usually, I am only contracted to do the install, so the invoice will only have labor lines on it. It is possible in the future that I might do more work for this customer, but that is only with permission from the referring dealer.
    
3. As a project coordinator, I need to set up my project with the appropriate customer on the quote and sales order, which also have the appropriate install address and customer contacts. However, for the order type Direct Business, I will be billing MillerKnoll. MillerKnoll has a direct relationship with the customer, and the customer gets pricing directly from MillerKnoll. I will only be receiving a Contract Management Fee (CMF). MillerKnoll will be identified as the "Alternate Bill To" on the quote and the order. However, a few things will happen automatically that make my life easier as a project coordinator:
    
    - When any purchase order is created for items on a direct bill order that are not marked with 'Teaming Agreement' in the ==Invoicing instructions column==, the cost/rates on the PO are set to zero. This ensures that the product does not have a WIP impact when received.
        
    - When the invoice is generated, all items except those marked with teaming agreement will have a discount item applied to it called Direct Business Adjustment. This will make sure we impact COGS correctly.
        
    - Once a PO line is received, it will be billed as normal but the cost will be zero. We will bill instead of close so the quantities on the bill are correct for the three way matching process.
        
    - Items on the invoice marked teaming agreement will have the appropriate sell as they will be reimbursed by MillerKnoll. There will be POs and Vendor Bills for these items to the appropriate vendors. These items will not have the COGS discount applied to it.
        
    - It is important to note that as a project coordinator, I will only set up one quote/sales order per direct business "Alternate Bill To." In other words, all lines on an order will be invoiced to one manufacturer. If there needs to be someone else invoiced, then a separate quote/sales order will have to be created.
        
    - We will be using NetSuite's 'Other Relationship' feature to allow for a vendor (MillerKnoll) to also be a customer so I can invoice them properly.
        

All this should happen automatically as long as I identify the order type as Direct Business and set MillerKnoll as the "Alternate Bill To," and see the appropriate lines on the order a Teaming Agreement. Any other lines that don't have a value in that field are assumed to be direct business.

Success Metrics:

1. Reduction in billing errors: Track the decrease in billing errors related to incorrect customer assignments compared to the previous process.
    
2. Increased accuracy of "Alternate Bill To" assignments: Monitor the percentage of orders with correctly assigned "Alternate Bill To" values.
    
3. Time savings in the billing process: Measure the average time saved per order in the billing process compared to the previous approach.
    
4. User satisfaction: Conduct surveys to gauge user satisfaction with the Orion Alternative Billing Option.
    
5. Faster order processing: Track the average time from order creation to invoicing after adopting the Orion Alternative Billing Option.
    

Design (UI/UX overview):  
The design for the Orion Alternative Billing Option will primarily rely on native NetSuite functionality, ensuring a seamless and familiar user experience. However, a custom component will be introduced to enhance the selection of the "Alternate Bill To" contact associated with the "Alternate Bill To" customer record.

Key design elements:

1. Native NetSuite UI: Leverage standard NetSuite interfaces for Quote and Sales Order forms to maintain consistency and minimize user learning curve.
    
2. Custom "Alternate Bill To" field: Introduce a new field on the Quote and Sales Order forms to capture the "Alternate Bill To" customer record. This field will be prominently displayed and easily accessible to users.
    
3. "Alternate Bill To" contact selector: Develop a custom component that allows users to select the appropriate contact associated with the "Alternate Bill To" customer record. This component will be intuitive and user-friendly, enabling quick and accurate selection of contacts.
    
4. Contextual help and guidance: Provide inline help text and tooltips to guide users on how to use the "Alternate Bill To" field and contact selector effectively.
    
5. Error handling and validation: Implement clear error messages and validation rules to prevent users from submitting incomplete or incorrect information related to the "Alternate Bill To" field and contact selector.
    

Roles and Permissions:

Edit Access:

- Orion - Admin
    
- Orion - Sales Support
    
- Orion - Ops Manager
    
- Orion - Project Manager
    
- Orion - Operations Admin/ Support
    
- Orion - Accounting Manager
    
- Orion - Controller/CFO
    
- Orion - A/P Analyst
    
- Orion - A/R Analyst
    
- Orion - Daily Administrator
    

View Access:

- Orion – Executive leadership
    
- Orion – Marketing Specialist
    
- Orion - Sales Leadership
    
- Orion – Sales
    
- Orion - Salesperson/ Account Manager
    
- Orion - Sales
    
- Orion - Design Manager
    
- Orion - Designer
    
- Orion - Purchasing
    
- Orion - Procurement
    
- Orion - Inventory Manager
    
- Orion - Warehouse Manager
    
- Orion - Warehouse
    
- Orion - Human Resources/ Payroll
    
- Orion - Employee Center
    
- Orion - Resource Manager
    

Features and Functionality:

1. "Alternate Bill To" field on Quote and Sales Order forms
    
    - Allows users to select an alternate customer record for billing purposes
        
    - Triggers custom warnings or restrictions if left blank, based on dealer-specific settings
        
2. Custom "Alternate Bill To Contact" contact selector
    
    - Enables users to choose the appropriate contact associated with the "Alternate Bill To" customer record
        
    - Provides a user-friendly interface for quick and accurate contact selection
        
3. Automated invoice generation
    
    - Updates the customer record on the invoice based on the "Alternate Bill To" field
        
    - Ensures accurate billing and AR reporting
        
4. ==Order type-specific automation and functionality==
    
    - ==3rd Party Billing:==
        
        - ==Validates the presence of the "Alternate Bill To" field and displays warnings if missing==
            
        - ==Updates the invoice customer to the selected "Alternate Bill To" customer (e.g., General Contractor)==
            
    - ==Intermarket Incoming:==
        
        - ==Sets the intermarket dealer as the "Alternate Bill To" customer==
            
    - ==Direct Business:==
        
        - ==user Sets MillerKnoll as the "Alternate Bill To" customer==
            
        - ==User sets order type and identifies teaming agreement lines==
            
        - ====User adjusts cost/rates on purchase orders to zero for non-teaming agreement items====
            
        - ==User applies appropriate discounts and fees on the invoice for non-teaming agreement items to ensure correct COGS impact. This amount is calculated by subtracting each non teaming agreement lines cost from sell and then totaling==
            
        - ==Maintains accurate pricing and billing for teaming agreement items==
            
        - ==best practice is the creation of separate quotes/sales orders for each manufacturer involved in the project==
            
5. Integration with NetSuite's "Other Relationship" feature
    
    - Allows vendors (e.g., MillerKnoll) to be set up as customers for accurate invoicing
        
6. Customizable warnings and restrictions
    
    - Enables dealers to set preferences for warnings or hard stops when the "Alternate Bill To" field is not populated for applicable order types
        
    - Prevents users from proceeding without addressing billing-related issues
        
7. ==Tax override functionality==
    
    - ==Ensures that the tax calculated on the sales order is reflected on the invoice, regardless of the tax platform being used (SuiteTax or Avalara)==
        
    - ==Disables tax recalculation or overrides it to match the sales order tax for consistent tax calculations across transactions==
        
8. Technical Considerations:
    

1. Workflow or scripting for banner warning when no "Alternate Bill To" is selected for the three order types (3rd Party Billing, Intermarket Incoming, and Direct Business) on create only
    
    - Develop a workflow or script that checks for the presence of the "Alternate Bill To" field when the order type is set to one of the three specified values
        
    - Display a warning message to the user if the "Alternate Bill To" field is left blank, prompting them to either select a value or proceed without one
        
    - Allow dealers to configure whether the warning is a hard stop or a soft warning during implementation
        
2. Customization of NetSuite's "Other Relationship" feature
    
    - Configure the "Other Relationship" feature to allow vendors to be set up as customers for direct business scenarios
        
    - Modify the user interface to make this feature easily accessible and user-friendly for dealers
        
    - Provide clear instructions and training materials to ensure proper usage of this feature
        
3. Performance optimization
    
    - Analyze the impact of the Orion Alternative Billing Option on system performance, especially for dealers with high transaction volumes
        
    - Implement necessary optimizations, such as indexing, caching, or batch processing, to maintain optimal performance
        
    - Monitor performance regularly and make adjustments as needed to ensure a smooth user experience
        
4. Security and access control
    
    - Review and update role-based access controls to ensure that only authorized users can access and modify the "Alternate Bill To" field and related functionality
        
    - Implement necessary security measures, such as data encryption and audit trails, to protect sensitive billing information
        
    - Regularly review and update security settings to maintain compliance with industry standards and best practices
        
5. SuiteScript 2.1
    
    - Develop the necessary customizations and automations using SuiteScript 2.1
        
    - Leverage the features and capabilities of SuiteScript 2.1 to ensure efficient and effective customization of the NetSuite platform
        
    - Follow best practices for script development, including modular design, error handling, and performance optimization
        

Testing and Quality Assurance:  
Test Script Title: "Orion Alternative Billing Option Test Script"

Test Objectives:

1. Validate the functionality of the "Alternate Bill To" field and contact selector on Quote and Sales Order forms
    
2. Ensure accurate invoice generation based on the "Alternate Bill To" value for each order type
    
3. Verify the effectiveness of customizable warnings and restrictions when the "Alternate Bill To" field is left blank
    
4. Test the tax override functionality to ensure consistent tax calculations across sales orders and invoices
    
5. Validate the integration with the BOM import process for automatic population of the "Alternate Bill To" field based on order type
    
6. Verify the accuracy of cost adjustments and vendor bill creation for specific billing arrangements
    

Test Environment:

- Sandbox environment with representative data for 3rd Party Billing, Intermarket Incoming, and Direct Business order types
    
- Production environment for final user acceptance testing (UAT)
    

Test Data:

- Sample quotes and sales orders for each order type (3rd Party Billing, Intermarket Incoming, and Direct Business)
    
- Customer and contact records representing various billing scenarios
    
- Product and service items with appropriate pricing and configurations
    
- BOM files for testing the integration with the BOM import process
    
- Tax settings and configurations for testing the tax override functionality
    

Test Steps:

1. Create a quote or sales order for each order type (3rd Party Billing, Intermarket Incoming, and Direct Business)
    
2. Populate the "Alternate Bill To" field with a valid customer record and select an associated contact using the custom contact selector
    
3. Generate an invoice from the quote or sales order and verify that the invoice customer matches the "Alternate Bill To" value
    
4. Repeat steps 1-3 for each order type, testing various billing scenarios and edge cases
    
5. Attempt to save a quote or sales order without populating the "Alternate Bill To" field for each order type and verify that the appropriate warning or restriction is triggered based on dealer-specific settings
    
6. Test the tax override functionality by comparing the tax calculations on the sales order and invoice for each order type
    
7. Import BOM files for each order type and verify that the "Alternate Bill To" field is automatically populated based on the order type
    
8. Validate the accuracy of cost adjustments and vendor bill creation for specific billing arrangements, as applicable
    

Test Assertions:

1. The "Alternate Bill To" field and contact selector are available and functional on Quote and Sales Order forms for all order types
    
2. Invoices generated from quotes or sales orders accurately reflect the customer specified in the "Alternate Bill To" field
    
3. Customizable warnings or restrictions are triggered when the "Alternate Bill To" field is left blank for applicable order types, based on dealer-specific settings
    
4. Order type-specific automation and functionality, such as adjusting cost/rates or applying discounts, are executed correctly based on the "Alternate Bill To" value and other relevant criteria
    
5. Integration with NetSuite's "Other Relationship" feature allows vendors to be set up as customers for direct business scenarios
    
6. Tax calculations on invoices match the tax calculations on the corresponding sales orders, ensuring consistency and accuracy
    
7. The "Alternate Bill To" field is automatically populated based on the order type during the BOM import process
    
8. Cost adjustments and vendor bill creation are handled accurately for specific billing arrangements, as needed
    

Test Metrics:

1. Percentage of test cases passed for each order type and billing scenario
    
2. Time taken to complete the invoicing process for each order type with the Orion Alternative Billing Option compared to the previous process
    

Test Execution:

- Execute the test script in the sandbox environment, documenting any issues or deviations from expected results  
    -​​​​​​​​​​​​​​​​
    

## Technical Specifications

## Object Definitions

## Data Design

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