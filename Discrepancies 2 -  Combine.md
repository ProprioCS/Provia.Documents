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

There are a number of common types of Issues in Commercial Furniture and related business units. Instead of treating each as its own thing, we will generalize them under the title “Issues”. **Broadly defined,** **an “Issue” is anything that can go wrong with a project/transaction which can cost the dealer money they did not expect to pay, or time they did not expect to spend, after the Quote has been signed off on by the Customer**. Note that any errors or discovered costs before that point are not Issues - if the Customer has not yet agreed to the Quote, there is still time to adjust the sell to reflect all known costs. Thereafter, with the exception of Change Orders agreed to by the Customer, any new or increased costs are an Issue. In other words, if you make a mistake and catch it (or someone else does) BEFORE the Sell is agreed to by the customer, it is not an Issue. If cost must be added but you cannot increase the sell - it is an Issue. An issue can also be time lost due to an unquoted need - we will record the time, and if the dealer has a rate for this, also the cost.

## Solution Type

·       Utilities – less extensive functionality than modules

## User Stories

As almost any role, I want to be able to track Issues and have visibility to them, filtering by their type, dates, and cost amount.

As an Order Entry person, PM, or Operations person, I want to be able to enter/update Issues wherever they occur in the process.

## Success Metrics

Success will come from a dealer being able to easily record any Issue Category and have access to all the data they want to track.

## Design

We have completed Punch, which is the “biggest” Issue Category in terms of UI/UX. We now need to modify the Punch UI to include an Issue Category dropdown, and have UI for the entry of all other Issue Categories with their appropriate fields.

Note that this feature lays the groundwork for a dealer in the future to be able to create their own Issue Categories, but in Phase 1 we will not provide an interface for this, or map a Category to specific fields in the database.

Returning Product will have its own UI as part of the Operations modules - it can be entered in the field, or in the office.

Receiving Issues will be entered in the Orion Receiving UI.

Pricing and Ack Issues are line-related and should have a quick and easy UI in the smart table/left hand nav. I question if they need a full suitelet UI as Punch / RP do - but maybe they do if the user wishes to assign them to someone else, or later enter a Resolution, or create Tasks, or add notes - and if they do, perhaps our UI has a “quick add” for the basic information, and also a button to open the “detailed UI”, which the user can click only when they want/need to. I think that approach will keep simple things simple but allow for complexity when desired.

Time Lost issues

## Features and Functionality

1. **Punch Issues** (Issues discovered in Operations - generally executing Work Orders)
    
2. **Acknowledgement Issues** - Issues discovered when a Vendor Acknowledgement is received and the dealer learns that they included the wrong Cost for one or more Lines.
    
3. **Pricing Issues** - outside of an Acknowledgement, the dealer discovers on their own that incorrect pricing was used for some Lines, but the Customer has already signed the Quote. An example could be using an outdated catalog in CAP, or using the wrong Contract #, or specifying options incorrectly in such a way that the correct option(s) would have a higher cost.
    
4. **Returning Product** - product coming back from a job that we did not anticipate. This can be associated with a Punch Issue (e.g. bringing a damaged table top back for repair, or for returning to the Vendor, or for disposal.) But it can also simply be the Customer asking the crew to take items away when we did not have a cost/sell for that on the Order. It is fine if we knew this and quoted it - but it happens unexpectedly also, and dealers over time find their warehouse filling up with “stuff”. There may not be a cost recorded for this type (although the time it takes can be recorded), but a resolution process is needed.
    
5. **Receiving Issues** - formerly handled under Punch, but can now be its own Category. This typically happens when received product is discovered to be damaged, missing, or the wrong product. It involves a Quantity field also - we may have ordered 12, but received 10. Or there may be 6 tables, but only 1 is damaged. There is often no cost associated with these, but can certainly be a Resolution which requires tasks.
    
6. **Time Lost issues** - break these out of Punch (where we just parked them because we had no other place). E.g. Wrong Contact. Door locked. Elevator down. Somebody blocked the loading dock.
    

## Technical Considerations

Some Issue Categories do not require much storage in the database. For example, an Acknowledgement Discrepancy will have its information stored on the Line itself. However, the cost variance in this case should be stored in a new generalized Issue custom record. The existing Punch utility will also write to this record - not all of the detailed fields on a Punch Issue (which are in the punch issue record), but the Cost of the Punch Issue (the total of all Resolution Lines). Updates to an existing Punch records Resolution Lines will adjust its Issue record automatically. Other Issue Categories may also have their own records (e.g. Returning Product will have a bin field - where did we put it when we brought it back?), but any Issue with a cost in dollars or time lost will create an entry in the Issue record. This allows us to quickly query for any or all Issue Categories in one place, when we are looking for the basic data - we will not need to join in all Lines or all Punch or all Returning Product or all Acknowledgements.

## Technical Specifications

## Object Definitions

## Data Design

**customrecord_orion_issue_category**

name:

- Punch
    
- Acknowledgement
    
- Pricing
    
- Receiving
    
- Returning Product
    
- Vendor Incident?
    

custrecord_ori_ic_lines

custrecord_ori_ic_resolution

custrecord_ori_ic_files

custrecord_ori_ic_tasks

custrecord_ori_ic_bins

custrecord_ori_ic_time

custrecord_ori_ic_types

custrecord_ori_ic_statuses

custrecord_ori_ic_reasons

**customrecord_orion_issue**

custrecord_ori_issue_category

custrecord_ori_issue_transaction

custrecord_ori_issue_related_type (e.g. punch record, returned product record, line item - or could be null if the issue category does not require a record for other details)

custrecord_ori_issue_related_id

custrecord_ori_issue_cost (can be null - e.g. a Receiving Issue)

custrecord_ori_issue_time

custrecord_ori_assigned (employee)

custrecord_ori_issue_tasks

custrecord_ori_resolution_date

custrecord_ori_resolution_by (employee)

custrecord_ori_issue_status (i think we can just use customlist_orion_punch_status here?):

- Not Started
    
- Investigating
    
- Resolution Entered
    
- Resolution in Progress
    
- Resolution Completed
    
- Cancelled
    

custrecord_ori_resolution_type (here is what we have now in punch res type list - do we need more for other Issue Categories?):

- Return and Credit
    
- Replace Product
    
- Repair Product
    
- Storage
    
- Customer Agreement
    
- Customer Goodwill
    
- Other
    

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