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

This solution is designed to streamline the quoting process for contract furniture dealers by using Generic Items and Service Items until line level detail is required to proceed with the order. This solution allows for flexibility in configuring the items to meet individual dealer needs while still providing a standardized baseline.

A dealer will leverage Netsuite’s Division segmentation to provide the additional detailed reporting that dealers require to track items by Division. This allows a smaller subset of Generic and Service Items than in their old DBOS systems that did not have Division segmentation per transaction.

## Solution Type

Configurations  -NetSuite features to be enabled, configured or installed

## User Stories

1. A NetSuite consultant will be able to demonstrate and explain the baseline set of Generic and Service Items.
    
2. A NetSuite techno-functional consultant will be able to easily install the baseline set of Generic and Service Items.
    
3. The dealer will be able to review and select Generic and Service Items.
    
4. The dealer NetSuite admin will be able to make changes to the baseline Generic and Service Items.
    

## Success Metrics

Outline how we know this solution meets our goals.

## Design

UI/UX for the solution. Link to supporting documents

## Roles and Permissions

1. NetSuite Consultant
    
    - Permissions: View and demonstrate the baseline set of Generic and Service Items
        
2. NetSuite Techno-Functional Consultant
    
    - Permissions: Install, configure, and customize the baseline set of Generic and Service Items
        
3. Dealer
    
    - Permissions: Review and select Generic and Service Items during the quoting process
        
4. Dealer NetSuite Admin
    
    - Permissions: View, modify, and manage the baseline Generic and Service Items
        

As you mentioned, the Generic and Service Items will be transparent to most other roles, so they won't require specific permissions related to this functionality.

## Features and Functionality

1. Generic Items (Products):
    
    - HM Furniture
        
    - Knoll Furniture
        
    - MK Affiliated Furniture (Geiger, Maharam, etc.)
        
    - Other Furniture
        
    - Architectural Products Primary (Walls, Falkbuilt)
        
    - Architectural Products Other
        
    - Flooring Products
        
    - AV Products
        
        @Marcus Dallacqua **Not 100% sure that we need this much delineation in the Generic Items - I don’t totally understand why we can’t use Vendor (or query link to Vendor Category) to provide the info the dealer needs as opposed to creating separate Generic Items for HM and Knoll and Other… and then I also feel fuzzy about how Division can be used instead of creating Walls, Flooring, AV as generic items…??? What if it’s Generic Item = Product and the rest is query-able with the other data held in NetSuite?
        
2. The functional consultant will work with the dealer to determine the relevant Service Items to include things such as:
    
    - Delivery
        
    - Design - Contract
        
    - Design - Internal
        
    - Direct Bill Fee (CMF)
        
    - Discount (Loyalty Program, On the Fly Special Discount)
        
    - Disposal/Dump Charges
        
    - Drayage
        
    - Electrician Services
        
    - Freight
        
    - Fuel Surcharge
        
    - IFF Fee
        
    - Installation - Internal
        
    - Installation - External/Subcontractor
        
    - Kickback/Management Fee
        
    - Move Services - Project Management
        
    - Move Services Labor
        
    - Project Management - Contract
        
    - Project Management - Internal
        
    - Storage Charge
        
    - Tariff
        
    - Technical Services
        
    - Travel
        
    - Truck Charges
        
    - Warranty Labor
        
    
    [Dealer CORE OPCs Reference for Generic and Service Items.xlsx](https://suitecentric-my.sharepoint.com/:x:/g/personal/marcus_dallacqua_suitecentric_onmicrosoft_com/EbeFGwSBFi9CmCXjMX01YvEBC9Y6qVO7xIwtBfr9NAUVtw?e=9Kbmqj "https://suitecentric-my.sharepoint.com/:x:/g/personal/marcus_dallacqua_suitecentric_onmicrosoft_com/EbeFGwSBFi9CmCXjMX01YvEBC9Y6qVO7xIwtBfr9NAUVtw?e=9Kbmqj")
    
    Additional Functionality:
    
    - NetSuite will leverage Division segmentation to provide detailed reporting that dealers require to track items by Division.
        
    - Division segmentation allows for a smaller subset of Generic and Service Items compared to old DBOS systems that did not have Division segmentation per transaction.
        

## Technical Considerations

- The BOM importer, MFG, and Catalog codes have a dependency on the Generic Items. The relationship between the Generic Items and lines imported with the BOM importer must be clearly defined and verified during the NetSuite implementation.
    
- Guidelines for Service Item import via the BOM importer must be clearly documented and included in training materials provided to the dealer.
    
- The Generic and Service Items will have a relationship to the Project Intel module, which needs to be considered in terms of how they are displayed or interact with Project Intel.
    
- Service Items may have a default rate associated with them.
    
- Service Items may have default vendors, or the dealer may need to select the vendor during the quoting process.
    
- These additional technical considerations highlight the importance of:
    
    - Defining the relationship between Generic and Service Items and the Project Intel module.
        
    - Determining whether Service Items will have default rates and how they will be managed.
        
    - Establishing a process for associating vendors with Service Items, either through default settings or dealer selection.
        

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

Test Objectives:

1. Validate the functionality of Generic and Service Items in the quoting process.
    
2. Ensure the BOM importer correctly associates imported lines with the appropriate Generic Items.
    
3. Verify that Division segmentation provides the expected level of detailed reporting.
    

Test Environment:

- Testing will be conducted in a sandbox environment that mirrors the production environment.
    

Test Data:

- Test data will include a representative sample of quotes, generic items, service items, and BOM import files.
    

Test Steps:

1. Create a new quote using the predefined Generic and Service Items.
    
2. Import a BOM file and verify the association of imported lines with the appropriate Generic Items.
    
3. Generate reports using Division segmentation and validate the level of detail provided.
    

Test Assertions:

1. The quote is created successfully with the correct Generic and Service Items.
    
2. The BOM import process accurately associates imported lines with the corresponding Generic Items.
    
3. Division segmentation reports provide the expected level of detail for tracking items by Division.
    

Test Metrics:

1. Percentage of quotes created without errors.
    
2. Accuracy rate of BOM import line associations.
    
3. User satisfaction rating for Division segmentation reporting.
    

Test Execution:

- Testing will be executed by the designated QA team using the specified test data and following the documented test steps.
    

Test Results:

- Test results will be recorded and compared against the expected outcomes defined in the test assertions.
    

Defect Reporting:

- Defects will be reported using the standard defect tracking system, with severity levels assigned based on the impact on the quoting process.
    

Test Script Approval:

- The test script will be reviewed and approved by the project stakeholders, including the NetSuite consultant, techno-functional consultant, and dealer representatives.
    

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