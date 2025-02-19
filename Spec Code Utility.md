- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
- 7 [Technical Considerations](#Technical-Considerations)
- 8 [Technical Specifications](#Technical-Specifications)
    - 8.1 [Object Definitions](#Object-Definitions)
    - 8.2 [Data Design](#Data-Design)
    - 8.3 [Scripts and Automations](#Scripts-and-Automations)
- 9 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 9.1 [Unit Tests](#Unit-Tests)
    - 9.2 [Process Tests](#Process-Tests)
- 10 [Time Estimate](#Time-Estimate)

## Overview

The Manufacturer Code and Catalog Mapping component within Provia aims to streamline the process of importing and managing product data from SIF files for contract furniture dealers. This solution allows users to map the Manufacturer Code (MG) and/or the Manufacturer Catalog Code (MC) in imported SIF files to the appropriate Vendor in NetSuite. By establishing these mappings, the component ensures that product information is accurately associated with the correct Vendor records, enhancing data integrity and facilitating efficient product management.

Key benefits of the Manufacturer Code and Catalog Mapping component include:

1. Improved data accuracy: By mapping MG and MC codes to the proper Vendor records, the component minimizes the risk of errors and inconsistencies in product data.
    
2. Enhanced efficiency: The user-friendly interface allows Dealers to easily view, add, edit, and remove mappings, saving time and effort in managing product information.
    
3. Streamlined product management: With accurate Vendor associations, contract furniture dealers can better organize and manage their product catalogs, leading to improved operational efficiency.
    

## Solution Type

·      Customization (standard NetSuite customization including point and click and simple scripts)

## User Stories

1. As an importer of a SIF file, I want the MG and MC codes in the SIF file to map to a Vendor in the NetSuite database, and to be informed when no Vendor can be identified, so that I can ensure accurate product data and take necessary actions to resolve any missing Vendor mappings.
    
2. As an Administrator, I want to be able to manage the SIF Codes/Vendor Mappings - to add additional, modify existing, and inactivate incorrect ones, so that I can maintain up-to-date and accurate mappings between SIF codes and Vendors.
    
3. As a Dealer, I want to be able to import my existing mappings from my old system, so that I can seamlessly transition to Provia without manually recreating all the mappings.
    

These user stories cover the key aspects of the utility, including a process for missing mappings during SIF file import, manual management of mappings by Administrators, and the ability to import existing mappings from a Dealer's old system.

**Roles and Permissions**

1. Provia - Executive Leadership: View access to all Manufacturer Code and Catalog Mapping data.
    
2. Provia - Marketing Specialist: No access to Manufacturer Code and Catalog Mapping data.
    
3. Provia - Sales Leadership: View access to all Manufacturer Code and Catalog Mapping data.
    
4. Provia - Salesperson/Account Manager: View access to Manufacturer Code and Catalog Mapping data.
    
5. Provia - Sales Support: Full access to all Manufacturer Code and Catalog Mapping data, including view, create, edit, and delete permissions.
    
6. Provia - Admin: Full access to all Manufacturer Code and Catalog Mapping data, including view, create, edit, and delete permissions.
    
7. Provia - Design Manager: View access to Manufacturer Code and Catalog Mapping data.
    
8. Provia - Designer: View access to Manufacturer Code and Catalog Mapping data.
    
9. Provia - Purchasing: Full access to all Manufacturer Code and Catalog Mapping data, including view, create, edit, and delete permissions.
    
10. Provia - Procurement: Full access to all Manufacturer Code and Catalog Mapping data, including view, create, edit, and delete permissions.
    
11. Provia - Ops Manager: No access to Manufacturer Code and Catalog Mapping data.
    
12. Provia - Project Manager: View access to Manufacturer Code and Catalog Mapping data.
    
13. Provia - Operations Admin/Support: No access to Manufacturer Code and Catalog Mapping data.
    
14. Provia - Inventory Manager: No access to Manufacturer Code and Catalog Mapping data.
    
15. Provia - Warehouse Manager: No access to Manufacturer Code and Catalog Mapping data.
    
16. Provia - Accounting Manager: No access to Manufacturer Code and Catalog Mapping data.
    
17. Provia - Warehouse: No access to Manufacturer Code and Catalog Mapping data.
    
18. Provia - Controller/CFO: View access to Manufacturer Code and Catalog Mapping data.
    
19. Provia - A/P Analyst: No access to Manufacturer Code and Catalog Mapping data.
    
20. Provia - A/R Analyst: No access to Manufacturer Code and Catalog Mapping data.
    
21. Provia - Human Resources/Payroll: No access to Manufacturer Code and Catalog Mapping data.
    
22. Provia - Employee Center: No access to Manufacturer Code and Catalog Mapping data.
    
23. Provia - Resource Manager: View access to Manufacturer Code and Catalog Mapping data.
    
24. Provia - Daily Administrator: Full access to all Manufacturer Code and Catalog Mapping data, including view, create, edit, and delete permissions.
    

## Success Metrics

- To have a missing vendor mapping be a rare occurrence.
    
- When it does occur, to have an easy and user-friendly resolution process.
    
- No user can unknowingly end up with the incorrect vendor.
    
- A user with appropriate permissions can manage the mappings easily.
    

## Design

[https://www.figma.com/file/OS6PMamkuZlueD56tHkxF1/Catalog-Code-Manager?type=design&node-id=0%3A1&mode=design&t=UyW5oUXNkmnPXQKZ-1](https://www.figma.com/file/OS6PMamkuZlueD56tHkxF1/Catalog-Code-Manager?type=design&node-id=0%3A1&mode=design&t=UyW5oUXNkmnPXQKZ-1)

This is largely an under the hood component, but UX/UI becomes important in three ways:

1. Alerting a user attempting to import a SIF file that a Vendor was not identified for one or more SIF lines due to a missing MG/MC mapping.
    
2. Providing a process for the user to correct this issue. This could mean allowing them to type and select the proper Vendor (if it exists in the database), or notifying the appropriate role that either a new Vendor is needed, or a new mapping is needed for an existing Vendor. One approach (which I like and Catalyst has today), is to display on-screen a section with list of MG/MC codes that did not map to a Vendor in the current SIF file, and for each let them specify which Vendor to use interactively with a vendor lookup/dropdown. We could then save this mapping on the back end if the user has permission, or just use their selected Vendor for the current import. Below example of this approach is from Catalyst's current system:
    

4. Another approach would be to use a TBD vendor for those lines, but this should still require alerting the user that they have an invalid vendor on one or more lines, which they will need to address manually after the import - a bit less clean in my view, as they could forget to, and later run into an issue when PO generation happens - as we should not allow them to generate a PO to the special "TBD" vendor.
    
5. For the Admin or other roles with the ability to create/edit Vendors, an interface showing all the mappings as they currently exist. They should be able to type in a code and see which Vendor it is mapped to, and also arrange by Vendor, showing all MC codes mapped to that Vendor. They should be able to easily add new mappings, or modify existing. This interface could be stand-alone tied to a menu item, or could be part of a larger "Provia Settings" area, if we plan to have something like that.
    

## Features and Functionality

1. A SIF file can come from a variety of sources. Sometimes there is an MC element, which stands for Manufacturer Catalog. Sometimes there is not, but there is an MG element, which is just the Manufacturer. Sometimes there are both.
    
2. A particular Manufacturer can only have one MG code (eg. "HMI" for Herman Miller), but can have many MC codes (e.g. "HST", "HAO", "HBE", etc - all Herman Miller -there are scores of them for HMI alone.)
    
3. The BOM Import process must have a way to allow the import to proceed if it is unable to match the SIF codes to a Vendor - either allow the user to select a Vendor, or use the TBD vendor (or both - even if we let them look for one, they may not find what they are looking for in the database.)
    
4. An Administrative (or other roles with Vendor permissions) section must be able to see the existing mappings, modify them, inactivate them, and add additional ones.
    

## Technical Considerations

We won't want to let them map the same code to multiple vendors, unless we need to support Jennifer M's findings of conflicts with Configura. _**Note**_: she is currently verifying if there IS still a problem with Configura using MC codes that map to vendors other than CAP/Project Spec map to.

## Technical Specifications

## Object Definitions

## Data Design

- customrecord_orion_cat_code (already in dev instance)
    

## Scripts and Automations

It appears the Dev instance already has a standardized list of Vendors and their Catalog/Mfg Codes. We will need to allow the dealers to bring in non-standard Vendors, and any Internal Vendors they have created, along with any Catalog/Mfg Codes they have created. We can do this with a script if we have access to a SQL dump of their Core data. I do not know if Core itself can produce such a report in their interface. I have access to our pilots' data, and to a fair number of other dealer's data.

In addition, we could consider pushing updates of the Standard list - when there are new ones, or catalog codes are added. There is a website we can scrape for this, and we could automate that. I recommend we add a field to the Vendor entity along the lines of "isStandard" - that will allow us to update the standard vendors we preloaded, without affecting any non-standard or internal vendors added by the dealer. We could also have a field for our own ID for Standard vendors, so that we dont need to depend on the auto-numbered internal IDs and have conflicts. This could probably be in the the vendor's external ID.

Our Standard list could also include the Solomon Coyle name and/or ID, so that in the Solomon Coyle report process we eliminate the current need for the dealer to map vendors.

## Testing and Quality Assurance

## Unit Tests

## Process Tests

Test Script Title: Provia SIF Code Mapping Utility Test Script

Test Objectives:

1. Verify the accuracy and completeness of the MG/MC code to Vendor mapping process.
    
2. Ensure the user interface is intuitive, responsive, and functions as expected.
    
3. Validate the error handling and notification system for missing or incorrect mappings.
    

Test Environment:

- Sandbox environment with sample SIF files and Vendor records.
    
- Production environment with real-world data and scenarios.
    

Test Data:

- Sample SIF files with a variety of MG and MC codes.
    
- Vendor records with varying levels of complexity and data completeness.
    
- Edge cases and scenarios to test error handling and notification system.
    

Test Steps:

1. Import sample SIF files and verify the accuracy of the automatic mapping process.
    
2. Manually add, edit, and remove mappings through the user interface and confirm the changes are reflected correctly.
    
3. Simulate missing or incorrect mappings and validate the error handling and notification system.
    

Test Assertions:

1. The automatic mapping process accurately maps MG and MC codes to the correct Vendor records.
    
2. The user interface allows for seamless management of mappings, including adding, editing, and removing.
    
3. The error handling and notification system promptly alerts users of any missing or incorrect mappings and guides them through the resolution process.
    

Test Metrics:

1. Percentage of MG and MC codes successfully mapped to Vendor records during SIF file import.
    
2. Time taken to resolve missing or incorrect mappings through the user interface.
    

Test Execution:

- Perform manual testing by following the test steps and recording the results.
    
- Utilize automated testing tools, such as NetSuite's SuiteScript and SuiteTalk APIs, to simulate user actions and validate outcomes.
    

Test Results:

- Document the actual results of each test step and compare them against the expected results.
    
- Identify any discrepancies or issues encountered during the testing process.
    

Defect Reporting:

- Create detailed defect reports for any issues identified during testing.
    
- Assign severity levels to each defect based on its impact on the utility's functionality and user experience.
    
- Collaborate with the development team to prioritize and resolve defects.
    

Test Script Approval:

- Review the test script with key stakeholders, including the project manager, development lead, and business analysts.
    
- Obtain approval from all stakeholders before proceeding with the testing process.
    
- Ensure that the test script covers all critical aspects of the utility and aligns with the project's goals and requirements.
    

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development||
|NetSuite Setup||
|QA||
|**Total**|**0**|

Be the first to add a reaction