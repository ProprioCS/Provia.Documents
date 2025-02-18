- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
    - 6.1 [Example UI from the Past](#Example-UI-from-the-Past)
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

Most of the dealers are accustomed to being able to assign Line Items to Groups. These Groups have a freeform name entered by the user, and a few other attricutes. They are an actual database table, and so also have an ID. Each Line Item has a Group ID field, but in the interface only the Group Name appears. They can sort by the Group column, and select Lines by the Group column, and leverage Groups primarily for the following:

- Quote PDF generation
    
- Invoice PDF generation - using the exact same settings as had been used for the Quote (a reason for the persistence of the Group ID for each Line.)
    
- Selecting lines for PO generation.
    
- Selecting lines for Work Orders
    
- Simple housekeeping of the Lines (e.g. putting all the Time Entry lines into a group, or all of the D&I lines)
    
- Assigning images to Groups - with the ability for the image to display on a Quote PDF or Invoice PDF. (Less common than the previous use cases.)
    
- Line Groups are in essence a tool for communication - to the Customer in the case of the Quote/Invoice PDFs, and to yourself or other internal groups for POs and Work Orders.
    

## Solution Type

·       Utilities – less extensive functionality than modules

## User Stories

As an Order Entry role, I want to create Line Item Groups and assign lines to each. I want these group names to be a column in the smart table, and be able to sort and filter by them.

When doing many other operations on Lines, I want to be able to sort/filter by Line Group so as to select lines for something else: like a Quote PDF, a PO, an invoice, a Work Order.

When creating a customer-facing Quote or Invoice PDF, I want the option to create a “Grouped” PDF, one that will contain a summary/rollup of the items in each group. When I do this, the PDF shows the Group Name, any Group Description, and any Group Image, along with the total sell of all the Lines in the group.

## Success Metrics

We will be listing the functionality with two tags:

1. MVP - Meets current furniture system functionality.
    
2. RO - (Reasonably Outstanding) - Exceeds current furniture system functionality.
    

## Design

See section below “**Example UI From the Past**”

## Features and Functionality

**MVP:**

- Create a record for line groups. It has an ID, a Name, and a Description.
    
- Add a custom field to transaction lines for the ID of the group.
    
- Display the Group Name as a column in the smart table, and the constituted lines.
    
- Allow sorting/filtering by Line Group for selection purposes.
    
- Provide a way to add a selected line or lines to either a new group or an existing group. Their current Core system does this from a right-click, but we would do it from our Action menu. If “Add Line(s) to new Group” is selected, then there needs to be a popup to let them enter the group Name and Description.
    
- Also provide a way to remove selected Lines(s) from their current Group, if any.
    
- Our JSON data will also need to hold a list of the Transaction’s Groups - IDs and Names. But our Line JSON needs only the Group ID. A UUID can be used for Groups that do not yet exist in the database. Once constituted, the actual database record ID can be used.
    
- Allow uploading an image file to be associated with the group, used only for Quote/Invoice PDFs.
    
- In the PDF Composer, provide a choice of what type of PDF to create:
    
    - Groups Only (I suggest naming this “Summaries Only”)
        
    - Lines Only (I suggest naming this “Details Only”)
        
    - Groups and Lines (I suggest naming this “Summaries and Details”)
        

**RO:**

- Additional Group fields:
    
    - _Hide Group_ - this is useful for housekeeping groups, to hide them from the Quote/Invoice PDF. A Group cannot be hidden if any of its lines have a Sell. Hiding the group affects only the “Groups” part of the PDF.
        
    - _Hide Group Lines_ - this controls if the Group’s Lines are also hidden. Lines cannot be hidden if they have a Sell. In this way you could group all of your D&I lines in a group called “Delivery and Installation. You could hide that group - but in a “Groups and Lines” PDF, still display the actual lines.
        
    - _Group Display Order_ - so it doesn’t have to be alphabetic, or given a number prefix to force the order you want.
        
- Allow multiple images to be attached to a Group.
    
- Allow a Title and a Caption for each Group Image.
    
- Allow layout options for each image: “Inline” or “Stacked”
    
- Allow options for where the Title and Caption are displayed:
    
    - Title on top, Caption below
        
    - Title and Caption above image
        
    - Title and Caption to the left of image
        
    - Title and Caption to the right of image
        
    - Title and Caption below image
        

**MVP:**

One weakness of most dealers current system is that traditionally each and every Line Group had to be created manually. It isn’t hard as the Name is the only required thing, but as some point Core added an optional Default Group feature they called Predefined Line Item Group. This was a very basic table that simply let you input a name and description, and then every new Order would be born with any default groups entered here. It’s not a bad idea.

**RO:**

Other than the above optional default groups on every new Order, the current systems do nothing to create your Line Groups for you based on data in the SIF. This is a huge missed opportunity for them. What we could do is:

- Analyze the SIF and its contents.
    
- Provide an interface in the BOM import tool to display what data we found in the SIF columns they may want to group by: mostly the Tags and Subtotals. But we could do something with SIF attributes as well.
    
- Let them decide which SIF column (or Subtotals) goes into our buckets, like Tag1, Tag2, Contract #, and Group By.
    
- Also support a dealer default for which SIF elements should map to which Line columns/grouping. If the dealer has specified these settings, we default to them. But they can change them by dragging and dropping.
    
- This solves one problem we kind of have now - how do we know if the dealer put the Contract # in Tag, Alias1, Alias 2, Alias 3? There is no way to programmatically distinguish a Contract # from a Tag. We could tell them how they have to do it - but remember they will have many SIFs from the past they may wish to import, they obtain SIFs from other tools, and they obtain SIFs from other dealers who may follow a different practice. This interface lets them decide for each SIF, based on a preview of its actual data that we display to them.
    
- It also creates an RO opportunity - creating the Line Groups automatically from their chosen SIF element. The Lines are then imported with their Group info already there, and no longer need to be grouped manually. (This has been extremely popular at Catalyst and Hawaii.)
    
- One other benefit of having an analysis preview UI in the BOM Import is we can show them if there are any SIF items where we were unable to determine which Vendor to use. This could be because the SIF item has no MG or MC element, but usually it is that the dealer does not have the SIF code in MG or MC mapped to a Vendor in their database. In Core, every line had to have a Vendor ID. This is not the case in NetSuite, so we could leave the Vendor blank in these cases, or substitute a special TBD Vendor. In either case however, there is a very good chance that it was unintentional, and we should warn the user that we have imported Lines for which we could not determine the Vendor to use. In the past I displayed any such items and made them choose a Vendor.
    

**MVP:**

Dealers are accustomed to being able to create new Groups, and associate lines with them for a different purpose.

A fairly typical process is to create a new Quote in Core, import the lines from a SIF, and then manually create groups and group the lines for the customer-facing Proposal PDF.

Once the customer has signed the proposal, and the Order is ready to book, the dealer will then carefully record how the lines were groups for the Proposal and stash this data outside of the system. They do this because they understand that the ultimate Invoice PDF must show the exact same Grouping and Line format as the Proposal did - this is a frequent customer mandate.

After squirreling away their screen grabs, or color-coded highlighted printouts, or Excels capturing the original line groupings (I’ve seen all three of these used), they will then regroup the lines for the purpose of PO generation. Whether the dealer has a dedicated Procurement group or each PC-type person does their own Procurement, this is done so that the proper lines end up on the proper POs at the proper times.

After the PO/Ack cycle is complete (or between phases), the dealer may regroup the lines once again for the purpose of Work Order generation.

Finally, when all is complete, the dealer will manually and painstakingly put the lines back into their original Quote PDF groupings for the purpose of Invoice PDF generation.

**RO:**

Connect had a feature we called GroupSets.

Every Order was born with a default groupset, called Default. The dealer did not have to do anything if they never planned to regroup the lines later. Any Groups created from the SIF import were automatically in the Default Groupset.

But within the Groups popup, which was an easier way to create Groups, drag lines into and out of them, and set up the enhanced options and image settings, you could also create a new Groupset, and give it a name.

Only one Groupset could be “active” at a time. You could switch all the Lines to a different Groupset simply by selected its name.

This meant that after the initial grouping for the Quote PDF, the dealer could create a 2nd Groupset, and call it something like “Procurement”. They could then easily regroup the lines within that Groupset. And then make the Procurement Groupset the active Groupset. This would change the Group ID for every line to the new grouping.

Additional Groupsets could be created and saved as well, for example “Operations:.

At any time the dealer could switch the active Groupset on the order, and the lines would be grouped differently. It was a way of persisting their previous grouping work to be recalled later.

And, at the end, when it is time to Invoice, they could switch back to the Default Groupset with a click (they may have renamed it from “Default” to “Quote” or something.)

## Example UI from the Past

Importing a SIF file would present the user with a preview of the data found in this particular SIF:

It shows examples of any data found in the SIF for Tag, Alias1-3, and the SIF Subtotals (if it was a CAP Studio SIF format.) You could then drag those boxes to the ones on the right and say where to put them in our system: Contract #, Line Item Tag, or Grouping. Grouping would mean to automatically create Line Item Groups with the names from the SIF, and automatically put the corresponding Lines into those Line Groups.

This way you can auto-group the Lines by any of the Tag/Alias columns, or by the Subtotals (which is the most common case.)

Once you said where you wanted the SIF data to go, it would reformat the preview below to show what your Line data will look like:

Group Names were a column in the Lines table:

You could select any number of lines, and have these options relating to Groups:

If you said New Group, you got this:

**Groupsets:**

Groupsets are all RO, as Core does not have them. They are intended to solve the problem of people grouping lines one way for the Proposal, and then grouping them differently for other purposes - and ultimately having to group them back the original way for the Invoice.

At the time the first group is created for a transaction, a default groupset is created. Each group created for that transaction then has this groupset’s ID in it. And for some transactions, that is all that ever happens.

But if a user creates a new Groupset (either with a New button, or by cloning an existing groupset), they can group/regroup/ungroup any or all lines differently. When they save this groupset and its groups, they can make it the active groupset for the transaction. This was done simply by selecting from a dropdown in the header of the Line Items section.

This would change the Group ID in every line to the group ID it had in the selected groupset, which now becomes the active groupset. So it was now easy to switch to different groupings, and back to previous ones, at any time.

## Technical Considerations

If we stick with **MVP** in Phase 1, we will still need a custom record for the Groups, and a custom field on the Lines for the Group ID.

If we want to do the Group images in Phase 1, we will need storage for those as well. In their current systems, this feature is used, but not on a majority of Orders - mostly the big ones. Still, if we don’t do it, the dealers on Core (or Connect) will be losing something temporarily. I looked at a copy of Catalyst’s data, and out of 52000 groups in their database, only 500 of them had images attached.

If we can squeeze in the **RO** things, we will need more fields in the Line Group records, and more UI/Code. Particularly it would mean adding the mapping interface to the BOM import., as well as an interface to create/manage the Groups, and make assigning lines to them easy.

If we want to support auto-grouping the Lines by SIF Subtotals (the most common choice), we will need to make sure we support importing the “CAP Studio SIF” format. If we do this, we can distinguish it from the “Expanded Legacy SIF” format by looking for this key in the SIF:

CT1=

If that key is there, it is a CAP Studio SIF. Otherwise it is not. Before I only supported that one and the Expanded Legacy (which is all Core supports), but really most of the others are very similar.

If there was a CT1=, I called it CAP Studio SIF.

If there was no CT1=, but there was at least one PN=, I called it Expanded Legacy.

If there was no PN=, I called “Unknown” and wouldn’t import it.

As we parse, we then look for this key (which we can always look for, it just won’t be there in most SIF formats):

SU=

This key indicates a SIF subtotal. When we find one, the lines above the subtotal, since the beginning of the file OR since the last subtotal, are included in this subtotal.

Any text on the SIF line after SU= is the name of the subtotal. It is followed by a PD=, and any text there is the subtotal’s description. Both can have text, but it is also possible for SU= to be empty and only the PD= to have text. In that case, we use the PD= text as the subtotal name, and leave its description blank.

When a subtotal is encountered in the SIF, we would store it in an array of them. Each subtotal object in this array has a first_item and a last_item. The first subtotal has its first item as item number 1, and its last item as the item right before the next subtotal, if any. In this way, we know which items belong to each subtotal, and if the user chooses to auto-group the lines by Subtotal, we know which lines to put in each Line Group we create, using the Subtotals name and/or description. Note that the goal is not to create NetSuite subtotal lines, merely to let the dealer user group the lines by SIF subtotal. In Orion, it is just a Line Grouping and therefore the lines no longer need to be contiguous (although on import they will initially be contiguous, as that is how SIF subtotals work.)

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