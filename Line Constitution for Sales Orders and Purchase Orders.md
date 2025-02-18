- 1 [NetSuite Special Order PO Solution Design](#NetSuite-Special-Order-PO-Solution-Design)
    - 1.1 [Overview](#Overview)
    - 1.2 [Key Components](#Key-Components)
    - 1.3 [Detailed Process Flow](#Detailed-Process-Flow)
    - 1.4 [Reporting Process](#Reporting-Process)
    - 1.5 [Technical Considerations](#Technical-Considerations)
    - 1.6 [Key Considerations](#Key-Considerations)
    - 1.7 [Implementation Phases](#Implementation-Phases)
    - 1.8 [Next Steps](#Next-Steps)
- 2 [Time Estimate](#Time-Estimate)
- 3 [Changes And Revisions](#Changes-And-Revisions)

## ==NetSuite Special Order PO Solution Design==

## Overview

This solution design outlines the process of creating special order Purchase Orders (POs) connected to Sales Orders (SOs) in NetSuite, using a custom draft PO process and a master JSON file for line item data. It includes a reporting mechanism to validate the process and inform key stakeholders and the initiating user.

## Key Components

1. Custom Records:
    
    - Draft Purchase Order
        
    - Master JSON File (for line item data)
        
    - Process Execution Log (for reporting)
        
2. Custom Fields:
    
    - Sales Order: Add a field to store the associated Draft PO ID
        
    - Purchase Order: Add a field to indicate if it's a special order PO
        
3. SuiteScripts:
    

- MAP Reduce Script and whatever else Luke wants to do ![slightly smiling face](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/standard/caa27a19-fc09-4452-b2b4-a301552fd69c/64x64/1f642.png)
    

## Detailed Process Flow

1. Draft PO Creation:
    
    - Use existing process to create Draft POs with line items stored in the master JSON file
        
2. Draft PO Finalization:
    
    - User changes Draft PO status to "Finalize Purchase Order"
        
    - User Event Script triggers, adding the Draft PO to a processing queue
        
3. Sales Order Line Creation:
    

- Map/Reduce Script processes the queue of Draft POs
    
- For each Draft PO:  
    a. Retrieve associated Sales Order  
    b. Read line item data from master JSON file  
    c. Create transaction lines on the Sales Order  
    d. Update summary lines and totals  
    e.
    

4. Special Order PO Creation:
    
    - Within the same Map/Reduce Script:  
        a. Create a new Purchase Order marked as a Special Order PO  
        b. Create PO lines corresponding to SO lines  
        c. Use `orderline and orderdoc to associate lines between the two transactions`  
        d. Set the WIP asset account for receiving  
        e. Set the reference number field to the Draft PO number
        
5. Linking and Updating:
    
    - Update the Sales Order with the newly created Special Order PO ID
        
    - Update the Draft PO status to indicate processing is complete
        
6. Process Logging and Reporting:
    

- Create a new record in the Process Execution Log custom record, including:  
    a. Sales Order ID and total before and after line constitution  
    b. Draft PO ID, number, and total  
    c. Special Order PO ID and total  
    d. Number of lines on Draft PO and Special Order PO  
    e. User who initiated the process
    
- Trigger the Scheduled Script to generate and email the report
    

## Reporting Process

1. Scheduled Script Execution:
    
    - Runs after the Map/Reduce Script completes
        
    - Queries the Process Execution Log for new entries
        
2. Report Generation:
    
    - Creates a formatted report including:  
        a. Sales Order details (ID, before/after totals)  
        b. Draft PO details (ID, number, total, line count)  
        c. Special Order PO details (ID, total, line count)  
        d. Validation results (matching totals, line counts)
        
3. Email Distribution:
    

- Sends the generated report to:  
    a. Marcus and Luke (key stakeholders)  
    b. The user who initiated the process
    
- Uses NetSuite's email capabilities (nlapiSendEmail or N/email module)
    

## Technical Considerations

1. Lot Number Handling:  
    a. Special Order PO Inventory Detail:
    
    - Set lot numbers during the Special Order PO creation process in the Map/Reduce Script
        
    - Use `setSublistValue()` method on the PO line item to set the inventory detail sublist
        
    - Consider using a custom naming convention or retrieving lot numbers from the master JSON file
        
    
    b. Sales Order Line Inventory Detail:
    
    - Set lot numbers after the Special Order PO creation, in the same Map/Reduce Script
        
    - Use `setSublistValue()` method on the SO line item to set the inventory detail sublist
        
    - Ensure lot numbers match between corresponding PO and SO lines
        
2. Performance Optimization:
    
    - Use `SuiteScript 2.1` for better performance and maintainability
        
    - Implement pagination in the Map/Reduce Script to handle large volumes of data
        
    - Use bulk API operations where possible to reduce governance usage
        
3. Error Handling and Rollback:
    

- Implement try-catch blocks in critical sections of the script
    
- Create a rollback mechanism to revert changes if an error occurs mid-process
    
- Log detailed error messages in the Process Execution Log for troubleshooting
    

4. Data Consistency:
    
    - Use `@NAmdConfig` modules to share code and ensure consistent lot number generation across scripts
        
    - Implement database locking mechanisms to prevent concurrent modifications of the same records
        
5. Customization and Flexibility:
    
    - Use script parameters to allow easy configuration of key values (e.g., WIP account, lot number prefixes)
        
    - Design the solution to be easily extensible for future requirements
        
6. Testing and Debugging:
    

- Create a comprehensive suite of unit tests for each function
    
- Implement detailed logging throughout the process for easier debugging
    
- Set up a sandbox environment that closely mirrors production for thorough testing
    

7. Security:
    
    - Implement proper role-based access controls for all custom records and scripts
        
    - Use NetSuite's native encryption for sensitive data in custom fields
        

## Key Considerations

1. Performance: Use Map/Reduce Script for bulk processing to handle large volumes efficiently
    
2. Error Handling: Implement robust error handling and logging throughout the process
    
3. GL Impact: Ensure correct WIP asset account assignment for Special Order POs
    

4. Reporting:
    
    - Design with reporting requirements in mind, leveraging the SO-PO line associations
        
    - Implement validation checks in the reporting process
        
5. User Interface: Create a custom form or Suitelet to manage the Draft PO finalization process
    
6. Testing: Develop a comprehensive test plan, including unit tests and integration tests
    

7. Security: Implement appropriate role-based permissions for the new processes
    

## Implementation Phases

1. Phase 1: Develop custom records and fields
    
2. Phase 2: Implement core SuiteScripts (User Event and Map/Reduce)
    
3. Phase 3: Create SuiteFlow workflow
    
4. Phase 4: Develop reporting mechanism (Process Execution Log and Scheduled Script)
    
5. Phase 5: Develop UI enhancements and client-side scripts
    
6. Phase 6: Implement lot number handling logic
    
7. Phase 7: Thorough testing and refinement
    
8. Phase 8: User training and documentation
    
9. Phase 9: Deployment to production
    

## Next Steps

1. Review and refine this updated solution design with stakeholders
    
2. Create a detailed technical specification for each component, including lot number handling
    
3. Develop a project timeline and resource allocation plan
    
4. Begin implementation of Phase 1
    

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