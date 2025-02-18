- 1 [Overview](#Overview)
    - 1.1 [Scope](#Scope)
- 2 [Success Metrics](#Success-Metrics)
- 3 [User Roles and Permissions](#User-Roles-and-Permissions)
- 4 [Design](#Design)
- 5 [Features and Functionality](#Features-and-Functionality)
    - 5.1 [File Import and Management](#File-Import-and-Management)
    - 5.2 [Data Validation and Error Handling](#Data-Validation-and-Error-Handling)
    - 5.3 [Transaction and Item Management](#Transaction-and-Item-Management)
    - 5.4 [Fuzzy Lookups and Customization](#Fuzzy-Lookups-and-Customization)
    - 5.5 [Financial Calculations and Rounding](#Financial-Calculations-and-Rounding)
    - 5.6 [File Export](#File-Export)
- 6 [Technical Specifications](#Technical-Specifications)
- 7 [Architecture](#Architecture)
    - 7.1 [Dependencies](#Dependencies)
        - 7.1.1 [SIF to JSON](#SIF-to-JSON)
        - 7.1.2 [Line Item Display](#Line-Item-Display)
    - 7.2 [Configuration JSON](#Configuration-JSON)
    - 7.3 [Objects](#Objects)
        - 7.3.1 [BoM File Import](#BoM-File-Import)
            - 7.3.1.1 [Fields](#Fields)
        - 7.3.2 [BoM Error](#BoM-Error)
            - 7.3.2.1 [Fields](#Fields.1)
        - 7.3.3 [BoM Lines](#BoM-Lines)
    - 7.4 [Scripts](#Scripts)

## Overview

The BOM Import Tool is a native NetSuite solution designed to streamline the process of importing Bills of Materials (BOMs) into NetSuite for contract furniture dealers. This tool allows users to drag and drop a file containing item information directly ==onto a quote, sales order, or purchase order transaction record within NetSuite==. Upon import, the tool automatically populates the sublist with the relevant item data from the file.

The primary purpose of the BOM Import Tool is to bridge the gap between the design and specification process, which often occurs outside of NetSuite, and the order processing workflow within NetSuite. By enabling users to seamlessly import BOMs, this tool eliminates the need for manual data entry and reduces the risk of errors. Key benefits include increased efficiency, improved accuracy, and faster order processing times, ultimately leading to enhanced customer satisfaction and business growth for contract furniture dealers.

## Scope

Module

## Success Metrics

1. Import Speed: The Orion BOM Import Tool should be able to import files within seconds, ensuring high performance and minimal wait times for users.
    
2. Line Item Capacity: The tool should be capable of importing up to 2,000 line items per file, accommodating the needs of large-scale projects and complex BOMs.
    
3. Accurate Tax Calculations: The imported line items should have correct tax calculations applied without slowing down the import process, ensuring both accuracy and efficiency.
    
4. Data Integrity: The imported data should maintain its integrity, with all information accurately transferred from the source file to the corresponding NetSuite records.
    
5. Error Handling and Reporting: The Orion BOM Import Tool should provide comprehensive error handling and generate exception reports, allowing users to validate the imported data and quickly identify and resolve any discrepancies.
    
    1. what items did not get imported
        
    2. reports that allow the user to easily compare the number of lines in the sif with the # that were imported
        
    3. TBD vendor reporting so the user can address it. this can be an issue with the catalog code
        

These success metrics focus on performance, capacity, accuracy, data integrity, and user-friendly error handling, all of which are critical factors for the adoption and satisfaction of the Orion BOM Import Tool among contract furniture dealers.

## **User Roles and Permissions**

1. Orion - Sales Leadership: This role may need to access the tool for reviewing and analyzing sales quotes and orders.
    
2. Orion - Salesperson/Account Manager: Salespersons and account managers will use the tool to import BOMs and create quotes for their customers.
    
3. Orion - Sales/Admin/Sales Support: These roles will likely assist in preparing and managing sales quotes and orders using the imported BOM data.
    
4. Orion - Design Manager: Design managers may need to access the tool to review and approve BOMs before they are imported into NetSuite.
    
5. Orion - Designer: Designers will use the tool to import their designs and specifications into NetSuite for further processing.
    
6. Orion - Purchasing: The purchasing team may need to access the tool to review and process purchase orders based on the imported BOM data.
    
7. Orion - Ops Manager: Operations managers will oversee the use of the tool and ensure smooth integration with other operational processes.
    
8. Orion - Project Manager: Project managers will heavily rely on the tool to import BOMs and manage project-related quotes and orders.
    
9. Orion - Operations Admin/Support: These roles will provide support and assistance to users of the BOM Import Tool.
    

All these roles should have create permissions to allow them to import BOMs and generate the necessary transactions in NetSuite.

## Design

The user interface for the Orion BOM Import Tool has been designed by [Chris Trumble](https://suitecentric.atlassian.net/wiki/spaces/~71202011cf731166ad4f8ba2db412596ad166e "https://suitecentric.atlassian.net/wiki/spaces/~71202011cf731166ad4f8ba2db412596ad166e") and is available in Figma. The development team can access the design in Confluence.

Key UI/UX elements:

- Clean and intuitive user interface that allows users to easily navigate and interact with the tool.
    
- Drag and drop functionality, enabling users to import files by simply dragging them from their computer and dropping them onto the designated area within the tool.
    
- Browse option, allowing users to manually select files from their computer using a traditional file explorer interface.
    
- Support for adding multiple files simultaneously and arranging their import order by dragging and dropping within the tool.
    
- Placeholder for the upcoming Orion color scheme and branding, which will be incorporated into the design to ensure consistency with the overall Orion ecosystem.
    

The development team should refer to the Figma design for detailed specifications, visual elements, and user flow. The design may need to be updated once the Orion color scheme and branding guidelines are finalized.

## Features and Functionality

## **File Import and Management**

1. Support for importing SIF, PMX, XML, and CSV file types.
    
2. Ability to drag and drop files from a computer into quote, sales order, and purchase order transaction records.
    
3. Option for users to browse and select files from their computer.
    
4. Support for adding multiple files and arranging their import order by dragging and dropping.
    
5. Automatic conversion of imported files into JSON format.
    
6. Support for image import (pmx file type and maybe others) and the viewing of images in the line item data
    
7. ==Ability to append, prepend, or overwrite lines with new file imports==
    

## **Data Validation and Error Handling**

1. Real-time data validation to identify errors during import, particularly for CSV files prone to errors due to commas.
    
2. Requirement for users to resolve any identified errors before proceeding with the import.
    
3. Clear messaging to users about processing status, estimated processing time, progress, completion, errors, unimported items, and any vendors not found based on catalog codes.
    

## **Transaction and Item Management**

1. Creation of generic items on transactions with line item information, unique transaction line IDs, and lot numbers.
    
2. Selection of appropriate generic items based on product type:
    
    1. Lot Number inventory items for products
        
    2. Service items for Labor
        
    3. Non-Inventory items for Freight and Shipping
        
3. Unique naming convention for transaction line IDs and lot numbers, preferably including the project number or quote number for easy reference.
    
4. Access to catalog code records during import to identify the appropriate vendor for each item on the transaction.
    
5. Automatic calculation of financial fields (e.g., sell and cost prices) based on available information in the file, such as list price and discount.
    
6. Support for appending, prepending, or overwriting existing transaction data with imported data.
    

## **Fuzzy Lookups and Customization**

1. Fuzzy lookups on non-product items to identify and match existing items in NetSuite.
    
2. Ability for dealers to add their own common misspellings to a list of lookups to improve item recognition and prevent the creation of duplicate items.
    

## **Financial Calculations and Rounding**

1. On-the-fly financial calculations during import, with support for rounding to the 5th decimal place to match external systems.
    

## **File Export**

1. Export functionality to generate files in specific formats, including various SIF file formats, based on the imported and processed data.
    

## Technical Specifications

1. Integration with NetSuite: The tool must seamlessly integrate with NetSuite's existing architecture, APIs, and data model to ensure smooth performance and data consistency.
    
2. Scalability and Performance: The tool should be designed to handle a high volume of concurrent users and large file sizes without compromising system performance or stability.
    
3. File Format Support: The tool must accurately parse and process data from various file formats (SIF, PMX, XML, CSV) and handle potential format variations or inconsistencies.
    
4. Error Handling and Logging: Robust error handling mechanisms should be implemented to gracefully handle and log any errors or exceptions encountered during the import process, ensuring data integrity and facilitating troubleshooting.
    
5. Security and Access Control: The tool should adhere to NetSuite's security best practices, ensuring that user access is properly authenticated and authorized based on their assigned roles and permissions.
    
6. Data Validation and Consistency: Strict data validation rules must be enforced to maintain data integrity and consistency within NetSuite, preventing the introduction of duplicate or inconsistent records.
    
7. Asynchronous Processing: Consider implementing asynchronous processing for resource-intensive tasks, such as file conversion or large data imports, to avoid impacting the overall system performance and user experience.
    
8. Logging and Monitoring: Implement comprehensive logging and monitoring mechanisms to track system performance, user activities, and any potential issues or bottlenecks.
    
9. Compatibility with NetSuite Customizations: The tool should be designed to be compatible with existing NetSuite customizations, scripts, or workflows to avoid conflicts or disruptions.
    
10. Performance Testing and Optimization: Conduct thorough performance testing and optimization to ensure the tool can handle the expected load and provide a smooth user experience.
    

## Architecture

## Dependencies

### SIF to JSON

JSON will be generated using [https://suitecentric.atlassian.net/wiki/spaces/Orion/pages/2181234689](https://suitecentric.atlassian.net/wiki/spaces/Orion/pages/2181234689).

### Line Item Display

Line items are displayed using the [https://suitecentric.atlassian.net/wiki/spaces/Orion/pages/2178908165](https://suitecentric.atlassian.net/wiki/spaces/Orion/pages/2178908165).

## Configuration JSON

- Item type
    
    - Options
        
        - Generic
            
        - Partnumber
            
    - Determines how to handle the lookup/creation of items. Generic items do not need to be searched for or created. Partnumber items do need to be in or added to the catalog.
        
- File naming fields
    
    - For fuzzy lookup, allow additional fields to be searched on the item record (othername).
        

## Objects

### BoM File Import

A custom record that links a particular imported file with the generated JSON from that file. This record is used to persist imports between sessions.

#### Fields

- File: Original Bom Import File
    
- File: Generated JSON File
    
- Integer: The order of this imported file
    
- List/Record: Transaction
    

### BoM Error

A custom record that is used to report on errors with the import tool. It will communicate with Proprio solutions so that we can triage the error.

#### Fields

- List/Record: BoM File Import
    
- ==List/Record: Status==
    
- Text: Error details
    

### BoM Lines

Field: File

This is the storage mechanism for the line details on a BoM Order. We allow a user to modify the lines after import. Once lines are modified or reordered we can no longer easily allow reordering via the import popup method.

## Scripts

- Record Creation
    
    - BoM File Import
        
    - BoM Error
        
- File creation
    
    - BoM Lines
        

Be the first to add a reaction