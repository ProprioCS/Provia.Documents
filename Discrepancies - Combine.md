- - 1.1 [Overview](#Overview)
    - 1.2 [Proposed Solution: Discrepancy System](#Proposed-Solution%3A-Discrepancy-System)
    - 1.3 [Corrective Action Orders](#Corrective-Action-Orders)
    - 1.4 [Reporting and Analysis](#Reporting-and-Analysis)
    - 1.5 [Conclusion](#Conclusion)
    - 1.6 [Estimate](#Estimate)
        - 1.6.1 [Custom Records](#Custom-Records)
        - 1.6.2 [Record links](#Record-links)
        - 1.6.3 [Scripts](#Scripts)
- 2 [Time Estimate](#Time-Estimate)

## **Overview**

The furniture installation process, particularly within the contract furniture industry, is intricate and subject to various challenges. One of the critical aspects that can significantly impact customer satisfaction, project timelines, and overall profitability is the management of discrepancies (often called punch issues) that arise during the installation process. These issues, ranging from incorrect or damaged items to installation errors, require timely documentation, analysis, and resolution to maintain project integrity and client trust. Loosely defined, Punch is anything that unexpectedly goes wrong in an Order’s Receiving/Delivery/Installation phase that could cost the dealer money. Note that the cause of the issue can be earlier in the process, before the operations phases - what defines these discrepancies is that they are discovered in the operations phase. As such, they differ to an extent from a cost discrepancy discovered during the Acknowledgement phase.

For Orion, we have identified the need for a more structured and efficient way to handle these discrepancies within NetSuite, aiming to improve visibility, accountability, and process flow from issue identification through to resolution and analysis of associated costs and impacts.

## **Proposed Solution: Discrepancy System**

The Discrepancy System is a comprehensive solution designed to document, track, and resolve these issues efficiently within NetSuite. This system is centered around two main records: the **Punch Issue Record** and the **Punch Resolution Record**, supplemented by Corrective Action Orders to ensure a thorough resolution process. There will also be a record for Punch Problem Types, and custom lists for Punch Problem Reasons, Punch Statuses, Resolution Types, etc.

Discrepancies will most often be created from the Orion Work Order field interface, but must also be creatable in NetSuite from the Discrepancies tab on a Sales Order.

**Punch Issue Record**

The Punch Issue Record is the cornerstone of this solution, designed to capture detailed information about each punch issue as it arises. Key fields include:

- **ID**: Auto-generated unique identifier for each punch issue.
    
- **Created By**: The user who documents the punch issue.
    
- **Date Created**: The timestamp of when the punch issue was identified.
    
- **Original Sales Order #**: Reference to the related Sales Order for context.
    
- **Customer Name**: The name of the customer affected by the punch issue.
    
- **Work Order Day ID**: Link to the specific work order day for detailed tracking. (Not required - sometimes Punch is discovered outside of executing a Work Order.)
    
- **Problem Type (What went wrong)**: A drop down list of potential issues adminable by the users administrator. Examples of these which would make a good starter set include:
    
    - Damaged Product
        
    - Missing Product
        
    - Wrong Product
        
    - Product Not Ordered
        
    - Site Conditions
        
    - Damage to Site
        
    - Drawing Issues
        
    - Inaccurate Work Order Information
        
    - Wrong Address/Contact
        
- **Problem Reason (Why it went wrong)**: Categorization of the issue's root cause, with options such as:
    
    - Needs Identified (the default status when entered from the Field interface, as Installers usually do not know the “why”)
        
    - Sales Error (e.g. the wrong product was ordered, or in the wrong quantity)
        
    - Design Error (e.g. the wrong product was specified - or options such as finishes, or the design drawings showing product placement were incorrect.)
        
    - Customer Support Error (e.g. wrong customer address specified, incorrect site conditions, etc.)
        
    - Procurement Error (Wrong product was ordered, or in wrong Qty, or some items were never ordered.)
        
    - Manufacturer Error (Wrong product shipped, wrong Qty, product defective.)
        
    - Warehouse Error (the wrong product was pulled, or not in the proper quantity. Or it was not loaded on the truck after being pulled, or placed on the wrong truck.)
        
    - Installation Error (e.g. product was damaged during installation, or the customer site was damaged)
        
    - Subcontractor Error (same as Installation, but done by a Sub.)
        
    - Concealed Freight Damage (product damaged in freight)
        
- **Line Item(s)**: Any specific item(s) involved in the punch issue, with the ability to select multiple items from the original order. Some Punch Problem Types will require at least one Line Item to be selected. For others it will be optional. When Line Items are selected, there is also a Punch Quantity field to indicate how many of the item are affected (e.g. an Order Line Item might be for 12 chairs, but only 2 were damaged. (NOTE: a Punch Issue may be initiated from the Sales Order’s Discrepancy Sublist, or from selected lines.) When not initiated from Lines, depending on the Problem Type, a new Popup Line Selector version of the Smart Table can be opened. This will not have all the capabilities of the Smart Table - its sole purpose here is to help the user identify which lines they wish to select. Therefore it will include a subset of columns, and the ability to sort and filter, and simply return the selected lines' data to the calling code as an array of objects.
    
- **Additional Notes**: Any other relevant details or comments about the punch issue.
    
- **Location Note**: Information about where at the install site the issue occurred.
    
- **Product Returning:** Check box for if product is being unexpectedly returned to the Warehouse, and a text note to describe what.
    
- **Images**: One or more images to be associated with the Punch Issue record. Typically they are photos of damage, but could be anything.
    

**Punch Resolution Section**

Nested within the Punch Issue Record, the Punch Resolution section outlines the steps that will be taken to resolve each issue. Key fields include:

- **Punch Issue ID**: Linking back to the parent Punch Issue.
    
- **ID**: Unique identifier for the resolution.
    
- **Resolution Type**: Intended resolution. Examples include:
    
    - Return and Credit
        
    - Replace Product
        
    - Repair Product
        
    - Customer Agreement
        
    - Customer Goodwill
        
- **Date Created**: When the resolution information was entered.
    
- **Resolved Date**: The completion date of the resolution.
    
- **Created By**: The user responsible for the resolution.
    
- **Corrective Action Order Number(s)**: Associated order numbers for tracking and cost analysis.
    
- **Line Items:** As opposed to the selectable Problem lines from the original Sales Order, a Resolution can also be associated with lines (typically newer ones) which are intended to correct the problem. These lines could potentially have been added to the original Sales Order, but would usually instead be added to a Corrective Order tied to the original. Because the user may have already created these lines, the Resolution section will also allow them to use the Line Selector popup. However - we will also allow them to create lines here using the Smart Table/BOM Importer. They may do so manually, or by importing a SIF. When they create resolution lines here, we will create a Corrective Order for them, and save the lines they enter to its JSON file. This avoids the user having to go somewhere else to create the lines, and then come back to the Punch Resolution to select them.
    
- **Additional Notes**: This could include instructions
    
- **Status:** This could include, Not Started, investigating, Resolution Entered, In Process, Completed. These status can be automatically updated based on predefined business rules. Ex. When the corrective action order is placed, the Punch Resolution record could be updated to Completed, so long as that is how the dealer wants to define completed. Completion could be after installation of the Corrective Action Order.
    

## **Corrective Action Orders**

To ensure a seamless resolution process, Corrective Action Orders will be created as necessary, linked directly to the Punch Resolution Records and the original Sales Order. These orders are crucial for managing the logistics and financial aspects of resolving punch issues, including ordering replacement items, scheduling additional installation, and tracking all associated costs. The total Cost to the dealer for all Resolution Lines tied to a Punch Issue represents what the original Problem cost them - the ability to report on this is the ultimate payoff for having this feature. By analyzing the Problem Types, Reasons, by employee, by date range (etc), a dealer can determine where they are losing the most profit do to Punch issues. They can also compare to previous periods to gauge their improvement.

## **Reporting and Analysis**

A comprehensive reporting system, powered by SuiteQL, will be developed to monitor and analyze the punch issue resolution process. Key reports will include:

- **Punch Management Dashboard:** One master dashboard will be created using SuiteQL that allows the user to see Punch Resolution Status for the all projects, a particular project, down to a specific Sales Order.
    
- **Punch Issue Resolution Time**: Tracking the time from punch issue creation to resolution record creation and final resolution.
    
- **Bottleneck Identification**: Analysis of the process flow to identify stages where delays commonly occur.
    
- **Cost Analysis**: Detailed reporting on the costs associated with resolving punch issues, including the impact on project profitability and commissions. When a Punch Resolution is linked to Line Item(s) on a Corrective Order, the total Cost of those Line Items is the cost to the dealer for that Punch Issue. Reporting on these by Punch Problem Type, or Punch Reason, within a time period will provide valuable information to a dealer about margin erosion due to Punch, as well as help them gauge their progress towards improvement.
    

## **Conclusion**

The proposed Punch Record System within NetSuite offers a structured and efficient approach to managing punch issues in the contract furniture installation process. By providing detailed documentation, clear resolution pathways, and in-depth reporting, Orion dealers will improve operational efficiency, enhance customer satisfaction, and maintain project profitability. This solution design is a step towards optimizing internal processes and ensuring that every project is executed with the highest level of precision and accountability.

## Estimate

### Custom Records

Punch Problem Types

Punch Issue

Punch Item

Punch Resolution

**Custom Lists**

Punch Statuses

Punch Reasons

### Record links

Punch to Order

Punch Item to Punch

Punch Resolution to Punch

Punch Resolution to Punch Item

Punch Resolution to Sales Order (corrective or completion)

### Scripts

1. Punch Creation Button
    
    1. 4 hours
        
2. Punch Item list generation
    
    1. 4 hours
        
3. Resolution to Order creation
    
    1. 16 hours
        
4. Linking of records
    
    1. 6 hours
        

40 hrs would be reasonable to build this solution without the custom interface. Adding the custom interface will take additional time.

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development|28|
|NetSuite Setup|4|
|QA|8|
|**Total**|**42**|

Be the first to add a reaction