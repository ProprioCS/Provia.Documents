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

Describe the solution in two to three paragraphs

## Solution Type

·       Utilities – less extensive functionality than modules

## User Stories

As a Project Coordinator type person, I sometimes want to create a new transaction not by starting from scratch, but by cloning an existing transaction that was for the same customer and very similar to the new one.

## Success Metrics

A user can select an existing transaction and create a new one by cloning with a number of options for what to bring over and what not to bring over.

## Design

Here is some old UI that gave Connect a better set of options for cloning a Core order than Core did:

![image-20240701-122704.png](blob:https://suitecentric.atlassian.net/4888650b-a6cb-49ba-b3f5-933619c390d2#media-blob-url=true&id=e1aae4af-0988-4c02-b851-07c08033b8e9&collection=contentId-2266365955&contextId=2266365955&width=1361&height=920&alt=image-20240701-122704.png)

This was a popup that opened when the user was on an existing transaction and clicked the Clone button. It was a rather large popup haha.

The first section contained some body-level fields the user might wish to change in the new transaction. And in most of these, they had the option to remove them.

Then there was a section about what to do with the Lines. They could keep them all, keep only the ones they had selected (in the smart table in our case), or have no lines at all (I don’t think this is an option in NetSuite.)

They also had a checkbox for whether to bring over Void lines (Closed in our terms.) This was probably not checked very often.

Then they had a “Text Codes” section - that’s a Core term. But these refer to item fields like Tag, etc.

They also had an option to retain the Groupsets - see the Line Items Group solution design for what this meant.

They then had an option for which notes to include (Connect allowed many notes of different types on the same transaction.)

And the same for Files - but note that certain File Types were probably not shown here because they couldn’t possibly be useful on a newly-cloned transaction. For example, Work Order Completion files and customer signatures - they just can’t apply. I would think that things in Orion’s Communications sublist would fall into the same bucket - they can have no relevance to a new transaction.

There was then an option to open the new transaction after saving, and it defaulted to checked as you would usually want to do something with your new transaction immediately.

One thing that I’m surprised isn’t shown here is the Order Team - it seems we should show that and let them retain it, or make changes. You might be copying an old Sales Order where the Designer no longer works here, and you want to select a new one here. The same would go for Customer Contacts. I imagine they simply made any such changes in the new Transaction - and it wouldn’t be the end of the world if they still need to.

The result will be a Quote if the source was a Quote or a Sales Order. This ensures that it goes through any Quote Approval process, and any scripting on a new Quote is triggered.

Oh and we should provide an option about the Project. They can keep it as the original Project, They can have a new Project created (already existing behavior.) Or they can select an open Project for the same customer.

Hmm, maybe we have a checkbox to associate with original transaction. Does that mean we don’t need a separate Associated Order thing?

## Features and Functionality

1. Be able to Clone a transaction with options.
    
2. From Solution meeting:
    
    1. **New Create Date for Line Items**: When cloning, the create date on the line items should be updated to the new create date​(clone transcription)​.
        
    2. **Source Field Creation**: Implement a field to indicate the source of the clone, making it clear that an order was created as a copy of another order. This helps in troubleshooting and tracking the origin of the cloned order​(clone transcription)​.
        
    3. **Activity Logs**: Record cloning activity in the activity logs, including who performed the clone and when it was done​(clone transcription)​.
        
    4. **Data Dropping**: Ensure that any data that doesn't apply to the cloned transaction (e.g., acknowledgment transactions, certain records) is not carried over. Only the relevant data should be cloned​(clone transcription)​.
        
    5. **Handling Margin Erosion**: Be aware of the risks of not updating pricing information when cloning. Multiple clones of an original order with outdated pricing can lead to significant financial losses due to margin erosion​(clone transcription)​.
        
    6. **Header Information**: Provide options to select what header information comes over with the clone. Users should be able to decide which parts of the header information should be cloned alongside the lines​(clone transcription)​.
        
    7. **UI Considerations**: The user interface for cloning should be intuitive, making it clear when users need to select lines or specify details for the cloned transaction​(clone transcription)​.
        
    8. **Project Information**: Include options to either tie the clone to the existing project or create a new project. This should be user-selectable rather than defaulting to one option​(clone transcription)​.
        
    9. **Order Types**: Allow users to choose the type of transaction they want to clone into. For example, copying a sales order to another sales order or to a quote should be a user choice​(clone transcription)​.
        
    10. **Default Values and Options**: The UI for associating new orders should be similar to cloning, but with different default settings. This includes having no lines by default in certain cases​(clone transcription)​.
        

## Technical Considerations

Enter any guidance to our developers with regards to NetSuite (ie: I envision this to be a customer record/field etc and it should trigger on save of record)

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