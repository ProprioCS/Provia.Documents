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
- 11 [Changes And Revisions](#Changes-And-Revisions)

## Overview

Our goal is to create Summary Lines on each transaction while the “real” lines live in the JSON. We want to have enough Summary Lines on each transaction to allow overall financial reporting at any time, but no more than that. Our bias is toward fewer of them, but we want reporting by Item, Vendor, and Book Month/Year to be possible and accurate.

## Solution Type

·       Utilities – less extensive functionality than modules

## User Stories

As a person interested in reports detailing total sell/cost by Vendor, Item, or Booking Month/Year - Summary lines will provide the ability for these reports to be created.

## Success Metrics

Summary Lines are properly created and maintained based on the criteria below.

## Design

No UI for this, other than the built-in NetSuite Item sublist on a transaction.

However, the fields in summary lines should look like this when viewed in the native netsuite sublist:

|   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|
|Line#|Name|Description|Division|Vendor|Date Created|Amount|
|1|Summary Line|Item Name (e.g. MillerKnoll Furniture)|Furniture|MillerKnoll|6/30/2024|$325,894|
|2|Summary Line|Item Name (e.g. Other Furniture)|Furniture|SitOnIt|7/1/2024|$103,429|
|3|Summary Line|Item Name|Walls|DIRTT|6/30/2024|$74,832|
|4|Summary Line|Item Name|Walls|Maars|7/1/2024|$22,801|
|5|Summary Line|Item Name|Flooring|Mohawk|6/30/2024|$98,753|
|6|Summary Line|Item Name|Flooring|Shaw|7/1/2024|$10,293|
||||||**Total**|**$636,002**|

## Features and Functionality

1. When Lines are added to a transaction’s BOM, Summary Lines will be created as native items.
    
2. The Summary lines will total the Cost and Sell of all the actual JSON lines, based on:
    
    1. **NetSuite Item** - if a Sales Order has 200 lines, and a total of 8 ==distinct Items,== then at least 8 Summary Lines will be needed, each totaling the cost and sell for each distinct Item found in the JSON lines.
        
    2. **Vendor** - in addition to having a ==summary line by distinct Item==, we will also have one for each distinct Vendor. So if there are 10 lines with Item “Other Furniture” from vendor Global, 5 lines with the same Item from vendor SitOnIt, and 3 lines with the same Item from vendor National - instead of 1 Summary Line for Item “Other Furniture”, we will have 3 Summary Lines:
        
        1. A Summary Line with Item “Other Furniture” and vendor Global.
            
        2. A Summary Line with item “Other Furniture” and vendor SitOnIt.
            
        3. A Summary Line with item “Other Furniture” and vendor National.
            
    3. **Month/Year** - If additional lines are added at a later time, within the same month as the original lines, we can consolidate the new JSON lines into the existing Summary Lines. However, so we can preserve the ability to report on bookings by month, if the new lines are added in a different month than the original lines, new Summary Lines will be created for them using the Item and Vendor criteria above. For this reason, we will need a new custom field on transaction lines to store the create date. When we actually constitute the NetSuite lines, NetSuite will assign their built-in create date as of that moment. The custom field will allow us to instead display the values we stored in it - when the line was originally imported/created in the JSON. **Note**: When a Quote is transformed into a Sales Order, The JSON lines on the Sales Order should include the current date/time in the custom field. This represents the line’s “book date”, and it should not use the date in the Quote JSON lines' custom field.
        
    4. In addition to new lines added after the original lines are imported, any modification to the JSON lines must also trigger recalculating the appropriate summary lines. This is true if the qty, cost, or sell change, or if the Item is changed, or if the Vendor is changed.
        
    5. If lines are removed from the JSON, or Items/Vendors are changed such that they are no longer represented in the JSON at all, then a Summary Line can be removed.
        

## Technical Considerations

We have a NetSuite Item defined for Summary Lines, but they should instead use the actual Item mapped during the BOM import - or selected by the user. We can then remove or inactivate the Summary Item, and should not create that in new accounts.

This approach ensures that reporting by Item will be what we want. However, it means we cannot tell the difference between a Summary Line and a “normal” Line, once some “normal” lines have been constituted. This would not matter if our plan was to constitute all lines on the Sales Order at the same time, but our design is to constitute lines by PO, when the user clicks the Finalize PO button. Since a Sales Order can have many POs, and they are created over time, it makes more sense to do it this way, so that we aren’t constituting potentially hundreds of Sales Order lines before they have even created a PO, let alone received all the Acks.

Which creates a problem - if a Sales Order has a mix of constituted lines for some POs, and the lines for other POs are not yet constituted - how do we tell the difference between the constituted lines and the remaining Summary Lines? One approach would be a custom field like “is_summary”. Yet we may not need that - we might be able to just use the field which contains the linked PO ID. Since we are constituting by PO, when the user believes all Acking is complete, all constituted product lines will have a PO ID. Summary Lines will never have a PO ID. But this raises another question - some lines will never be on a PO (internal labor items, stock items, fees/credits/whatever.) When do those become constituted? Maybe when the last PO is constituted, we also look for any non-summary lines that do not have a PO ID, and constitute them at that time. But again - we need to be able to distinguish them from Summary Lines. FOR DISCUSSION.

Since we are already creating Summary Lines, we need only modify the algorithm to utilize the above criteria.

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

Testing considerations mainly concern importing a variety of lines with different Items and Vendors, and also adding some manual lines.

It should then be fairly easy to check that the Summary Lines are properly created by distinct Item, distinct Vendor, and Month/Year.

Lines should also be added in a subsequent month (or simulate this), so that we can verify new Summary lines are created appropriately.

Existing Lines should be modified, including by:

- Changing Cost and/or Sell on some
    
- Changing Qty
    
- Changing the NetSuite Item
    
- Changing the Vendor
    

In each of the above tests, the expected result is that the Summary Lines will be re-created or modified to reflect the new minimum number of them, and their costs and sells.

Lines should also be removed, such that a given Item or Vendor is no longer represented on the transaction, to verify that the appropriate Summary Line(s) are also removed.

This will also entail removing new lines added in a subsequent month, with the expected result that any Summary Lines created only due to the Month/Year being different are removed.

## Unit Tests

## Process Tests

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development|4|
|NetSuite Setup||
|QA|2|
|**Total**|**0**|

## Changes And Revisions

Be sure to Tag Dev (Luke) any time a new change is made. Format will be

1. Change 1
    
    1. Details
        
2. Change 2
    
    1. Details
        

Be the first to add a reaction