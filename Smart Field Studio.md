- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Design](#Design)
- 5 [Features and Functionality](#Features-and-Functionality)
- 6 [Technical Considerations](#Technical-Considerations)
- 7 [Technical Specifications](#Technical-Specifications)
    - 7.1 [Object Definitions](#Object-Definitions)
    - 7.2 [Data Design](#Data-Design)
    - 7.3 [Scripts and Automations](#Scripts-and-Automations)
- 8 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 8.1 [Unit Tests](#Unit-Tests)
    - 8.2 [Process Tests](#Process-Tests)
- 9 [Time Estimate](#Time-Estimate)
- 10 [Changes And Revisions](#Changes-And-Revisions)

## Overview

Many dealers traditionally maintain a checklist of sorts, often called something like "Pre-Order Checklist". For the most part, this checklist is kept outside of their business system in document form, as their system doesn't really support it. The items in the checklist are all things that any given Order might require, ones that are easy to forget or overlook or simply fail to specify. The results of the checklist are sometimes pasted/typed into their systems' Order Scope note (or equivalent) as free-form text. Dealers on Core might take a few of these and use Core's rudimentary custom fields to display them on an Order, and store them. These checklist items are often categorized into categories like Financial, Design, Project, Operations, etc.

The Requirements feature is a way to support these in the business system in a highly configurable way, so that each dealer can create and manage their own, with only the items they want, worded the way they want, and organized the way they want. It is completely data-driven and does not require customizing any forms per-dealer, or any custom code per dealer. The data structure describes everything needed to display their items, including labels, field types, visibility, default, required attributes, and any workflow logic. There is no difference between ones we decide to pre-load vs ones added by a dealer themselves - it is all just data. A single javascript function then renders them into a container. Another function validates them, and another sends them to the server, where a server script saves the data.

This approach completely eliminates the needs for us to create a perfect "standard template" with every item a dealer might want, and none that they do not want. Which was an impossible task anyway. Each dealer simply adds and modifies as they want with no need for customization. Dealers will also refine their processes over time and make changes - and again we don't need to worry about that, they are affecting only their own data. Even if you could somehow account for every dealer with a standard template approach, it doesn't take into account that each dealer will continue to change and evolve over time.

**Claude's take:**

The Requirements feature within Provia aims to streamline and centralize the management of pre-order checklists for contract furniture dealers. This solution allows dealers to create, customize, and maintain their own checklist items within their business system, eliminating the need for external documents and manual data entry.

Key benefits of the Requirements feature include:

1. Flexibility and Customization: Dealers can create and manage their own checklist items, tailored to their specific needs, terminology, and organizational structure. This data-driven approach eliminates the need for per-dealer customizations or custom code.
    
2. Centralized Management: By integrating the pre-order checklist into the business system, dealers can ensure that all relevant information is stored and accessed in one place, reducing the risk of overlooking important details or requirements.
    
3. Improved Efficiency: The Requirements feature streamlines the order process by providing a structured and organized way to capture and manage pre-order checklist items, saving time and effort compared to manual documentation and data entry.
    
4. Scalability and Adaptability: As dealers' processes evolve over time, they can easily modify and update their checklist items without requiring any customization or intervention from the Provia team, ensuring the solution remains relevant and effective for each dealer's unique needs.
    

## Solution Type

· Modules – extensive functionality that may include external integrations, frameworks – big stuff·

## User Stories

1. As any role with the ability to view a Quote or Sales Order, I want to see a tab with the list of the dealer's requirements for this particular order.
    
2. As any role with the ability to create/edit a Quote or Sales Order, I want to see a tab with the list of the dealer's requirement options, organized as the dealer has set up, along with any already entered in the case of edit, and be able to enter/select any which apply to this particular order.
    
3. As an Administrator, I want to be able to manage all the dealer's requirement options, change their category, create new ones, order them, set their attributes, and create overrides by any of the supported criteria.
    
4. As a role responsible for supplying Labor/Design/PM quotes, I want to see this Quote/Order's entered requirements in order to better provide an accurate quote.
    

## Design

These screen grabs are from current dealers' Connect systems, and included here as examples and to help explain - the Provia UI can be different. These are all generated in code by the rendering function, so to change how they look we need only change CSS styles.

One dealer's (Catalyst) default requirements on a Quote or Order, as currently configured:

Here is how they look for Hawaii:

Here is what they look like at Hawaii on a **Work Order**:

## Features and Functionality

Requirement Options (the set of items) each belong to a category, which becomes basically the field group. A dealer can add categories, rename, remove, and set the order of them.

They can also be grouped within their category (the ones above with the yellow line around them.) Groups come in several types - they can just be a visual thing, or they can enforce that one of the items in the group must be selected - like the Delivery & Installation or Receiving sections above - at least one option must be chosen. Groups can also have other types, such as Parent/Child (see Dock and Elevator below) and Sum.

Notice that while there were some options in the Quote/Order's operations sections, there are a lot more in the Work Order's. You know (and are required to specify) less in the earlier stages, and more later on.

The Requirement Options are the list of these items, and any can be associated with multiple "objects", such as a Quote, a Sales Order, a Design or Labor Quote, a Work Order, a Customer Site, or a Labor Resource. Each such object, when created, will inherit any requirements values from its predecessor. The idea is a consistent place to enter and specify things you know this job will need - there are things you know at Quote time, and then more at Sales Order time, Labor Quote time, Work Order time - etc. The list of options, their organization, and whether they should be required, or default to "on", is by object - so that you may have one be non-required at Quote time, but by the time they are requesting a Labor Quote it is required. In this way you capture what is known at every stage, as the project comes into sharper focus.

**Requirement inheritance:**

**Field Types:**

- On/Off (checkbox)
    
- Yes/No (dropdown) (this is the new one that supports "required" better than a checkbox)
    
- Date
    
- Dropdown (single or multiple)
    
- Text
    
- Lookup
    
- Number
    
- Email
    
- URL
    

There are also combination field types, e.g. On/Off Date or On/Off Text or Yes/No Text. You can make the secondary required in these cases, IF the checkbox is checked. For example, above if "Receiving - Internal" is checked, the dropdown with the list of Internal Warehouses becomes required. These are both On/Off Date Text:

The Dealer can also specify Placeholder and hover text.

There are also field-type dependent settings, for example for a Date you can specify if past dates can be entered, or if a past date should display in red. Number types let you specify if they can be negative. Etc.

**Default, Required, and Visible:**

- _Default_: The dealer can specify that any requirement option should default to "checked" or "yes". They can specify default text, or number, or date or a select option. 
    
- _Required_: They can also specify that any option is required - the user must enter/check/select something. This has no meaning for the On/Off checkbox, as leaving it unchecked is a valid option. This is why Jenna asked for the Yes/No dropdown - if set to required, it forces the user to choose one of those.
    
- _Visible_ doesn't seem to make sense - why create a requirement option and then set it to not visible? The answer is in the Overrides section
    

**Overrides:**

Regardless of a particular option's Default, Required, and Visible setting, these can be overridden based on:

- Stage/Transaction Type
    
- Customer
    
- Order Type
    
- Work Order Event Type
    
- Labor Resource Type
    

Overrides by **Stage** in NetSuite mean by transaction type. For example, the dealer may want a particular requirement to be not required at the Quote stage, but become required at the Order stage (or any later stage). If the user knows the answer at the Quote stage, they can record it. But if not, they can leave it blank - until the Order stage, where the dealer now wants it to be required. Other stages are Labor Quote, Design Quote and Work Order.

As an example of a **Customer** override, it isn't uncommon for a dealer to need various badges at times. Catalyst for example has a few of these. They created requirement options for Amazon Badge and T-Mobile badge (and some other ones). This is where "Visible" comes into play. They set these to not be visible. But then overrode them by Customer. So if they are creating an Order for some other customer, they do not see these options at all. Only if they create one for Amazon, Amazon Badge appears - and is set to Default and Required. 

You can also override by **Order Type** - so for a Walls Order (as opposed to Furniture or Standard), a different set of options can be displayed and/or defaulted. The same would go for a Moves order, or Flooring, or AV - some normal requirements may not apply to these, while others may only apply to these. Another example - you can have one for ServiceNet #, which becomes visible only when the Order Type is Intermarket.

You can also override by **Work Order Event Type**. For example, if a user creates a Work Order Event of type Walls, a different set of requirements would be displayed than for one of type Furniture D&I. Some Event types would hide almost all of them - for example "Customer Pickup".

And finally, for the requirements that can attach to a Labor Resource, you can override by the **Labor Resource Type**. An example would be an option for if an Installer has a particular badge, or clearance, or CDL. You would want this visible for a human type, but not a Truck type. But you might want another called "Scheduled Service" to appear for the truck type, but not the human type.

The overrides avoid having every conceivable item always on screen, even when they are not applicable.

**Admin Interface:**

A comprehensive interface is provided to allow a dealer to manage all aspects of their Requirement Options. The same interface can be used by us to do so on a dealer's behalf when requested.

**Where do Requirement Options appear?**

In the previous Provia, we had them appear only in a Work Order or Labor Resource. Now we can have them appear in Quotes, Orders, and Customer Sites. They can also appear when submitting a Labor Quote Request or a Design Quote Request, as the requirement values do a much better job of communication than any free-form text could. In all cases we just need a container for the function to render to, and then handle the validation and save.

## Technical Considerations

**Saved Search Note:** While the Requirement Options, Object Assignments, Categories/Groupings, Overrides etc needed a more complex structure in the database, the actual values for the requirements are stored in a single custom record "customrecord_orion_requirement_value", by:

- The "object" type (Quote, Order, Customer Address, Work Order, Labor Resource)
    
- The ID of the "object"
    
- The Requirement Option ID
    

This makes the actual values accessible by saved searches anywhere we want them to display.

**Note about scope:** This looks like a big scope - and it is - but it is an area in which we can be way better than the other systems. The dealers who have this today (e.g. Catalyst) really like how it lets them fine tune their process, and would not want to lose it. Others (like COI) who do not have it today really liked it when they saw it for Work Orders and Labor Resources only. The good news is that while yes, it's big, it is also largely complete in Provia - once we can restore all of it to an instance with the new architecture in place. We only need to hook it up to Quotes/Orders, and build Labor Quoting/Design Quoting and Customer Site Conditions to use it - and we were going to have to build those areas anyway. 

## Technical Specifications

## Object Definitions

## Data Design

_**Custom Lists used by the custom Records:**_

**customlist_orion_req_option_group_type**

**customlist_orion_req_lookup_type**

**customlist_orion_req_number_type**

**customlist_orion_requirement_yesno**

**customlist_orion_req_override_types**

_**These custom records hold the information about the requirement options, categories, object assignments, grouping, and overrides:**_

**customrecord_orion_requirement_objects**

custrecord_reqobj_is_transaction (checkbox)

custrecord_reqobj_transtype (varchar)

custrecord_reqobj_is_custrecord (checkbox)

custrecord_reqobj_custrecord_id (text)

custrecord_reqobj_is_request_type (checkbox)

custrecord_reqobj_request_type_id (Request Type)

custrecord_reqobj_display_name (text)

custrecord_reqobj_display_order (int)

**customrecord_orion_requirement_options**  
id  
name  
isinactive  
custrecord_ro_internal  
custrecord_ro_external  
custrecord_ro_visible  
custrecord_ro_default  
custrecord_ro_required  
custrecord_ro_field_type_id  
custrecord_ro_text_max_length  
custrecord_ro_text_placeholder  
custrecord_ro_text_required  
custrecord_ro_text_default  
custrecord_ro_select_values  
custrecord_ro_select_labels  
custrecord_ro_select_default_values  
custrecord_ro_select_required  
custrecord_ro_date_past_allowed  
custrecord_ro_date_default_today  
custrecord_ro_date_required  
custrecord_ro_date_show_past_red  
custrecord_ro_number_type (Integer, Decimal, Currency, Percent - Integer, Percent - Decimal)  
custrecord_ro_number_min  
custrecord_ro_number_max  
custrecord_ro_number_step  
custrecord_ro_number_required  
custrecord_ro_number_allow_negative  
custrecord_ro_number_default  
custrecord_ro_number_placeholder  
custrecord_ro_number_zero_valid  
custrecord_ro_lookup_type (Vendor,Customer)  
custrecord_ro_show_on_schedule  
custrecord_ro_show_in_scheduling  
custrecord_ro_show_on_print  
custrecord_ro_show_on_picklist  
custrecord_ro_show_on_report  
custrecord_ro_show_to_sp

**customrecord_orion_req_field_type**  
id  
isinactive  
name  
custrecord_rft_is_top_level  
custrecord_rft_top_level_id  
custrecord_rft_has_on_off  
custrecord_rft_has_yes_no  
custrecord_rft_has_date  
custrecord_rft_has_text  
custrecord_rft_has_lookup  
custrecord_rft_has_number  
custrecord_rft_has_dropdown  
custrecord_rft_dropdown_is_multiple  
custrecord_rft_has_email  
custrecord_rft_has_url  
custrecord_rft_display_order  
custrecord_rft_num_controls

**customlist_orion_requirement_category**  
id  
name  
isinactive

custrecord_rc_object_type

custrecord_rc_display_order

Getting rid of this one - it was redundant. Now each Category belongs to an Object Type, so we don't need this link record:

**customrecord_orion_req_category_object**  
id  
isinactive  
custrecord_rco_category_id  
custrecord_rco_object_type ("Quote", "Order", "CustomerSite", "Event", "Resource", "RequestType") (customlist - and as a dealer defines new request types we will add them to the list so they can assign requirement categories to them)

custrecord_rco_display_order

**customrecord_orion_req_category_member**  
id  
isinactive  
custrecord_rcm_option_id  
custrecord_rcm_category_id  
custrecord_rcm_display_order  
custrecord_rcm_name_override

Rethinking this: we had override records for: Stage, Customer, Order Type, Work Order Event Type, and Labor Resource Type. It would be better to have one record for overrides with am Override Type ID

So let's do this:

**customrecord_orion_requirement_override**

id  
isinactive  
custrecord_reqov_option_id

custrecord_reqov_override_type  
custrecord_reqov_override_id  
custrecord_reqov_show  
custrecord_reqov_default  
custrecord_reqov_required

And ditch these:

**customrecord_orion_requirement_stage**  
id  
isinactive  
custrecord_rc_option_id  
custrecord_rc_stage (Quote, Order, Request, WorkOrder)  
custrecord_rc_show  
custrecord_rc_default  
custrecord_rc_required

**customrecord_orion_requirement_customer**  
id  
isinactive  
custrecord_rc_option_id  
custrecord_rc_customer_id  
custrecord_rc_show  
custrecord_rc_default  
custrecord_rc_required

**customrecord_orion_requirement_order_type**  
id  
isinactive  
custrecord_rot_option_id  
custrecord_rot_order_type_id  
custrecord_rot_show  
custrecord_rot_default  
custrecord_rot_required

**customrecord_orion_requirement_event_type**  
id  
isinactive  
custrecord_ret_option_id  
custrecord_ret_event_type_id  
custrecord_ret_show  
custrecord_ret_default  
custrecord_ret_required

**customrecord_orion_requirement_res_type**  
id  
isinactive  
custrecord_rrt_option_id  
custrecord_rrt_resource_type_id  
custrecord_rrt_show  
custrecord_rrt_default  
custrecord_rrt_required

**customrecord_orion_req_option_group**  
id  
name  
isinactive  
custrecord_rog_type ("Enforce Selection", "Parent/Child", "Sum")  
custrecord_rog_require_selection  
custrecord_rog_nothing_option_id  
custrecord_rog_sum_option_id  
custrecord_rog_parent_option_id  
custrecord_rog_allow_multiple

_**This record holds the actual values for a given object:**_

**customrecord_orion_requirement_value**  
id  
custrecord_rv_option_id  
custrecord_rv_object_type (from list - Quote, Order, Request, WorkOrder, CustomerSite, LaborResource)  
custrecord_rv_object_id (the internal id of the object above)  
custrecord_rv_value_onoff  
custrecord_rv_value_yesno  
custrecord_rv_value_date  
custrecord_rv_value_text  
custrecord_rv_value_number  
custrecord_rv_value_select  
custrecord_rv_value_select_label  
custrecord_rv_value_lookup  
custrecord_rv_value_lookup_label  
custrecord_rv_value_email  
custrecord_rv_value_url

## Scripts and Automations

Scripts from the 1st Provia project:

- orion_reqs.js (was a suitelet - functions to load reqs data for an object (existing or new), and to save)
    
- orion_reqs_client.js (functions for rendering, user interactivity, validating, save packaging/submitting)
    
- orion_reqs_admin.js (suitelet)
    
- orion_reqs_admin_client.js
    

orion_reqs.js will become a restlet named _____

**Endpoints:**

1. Loading the Requirement Options for a new object, by Category, based on the Requirement Object type. Payload will include the Requirement Object type (Quote, Order, Request Type (e.g. Labor Quote, Design Quote, etc), Customer Site, Labor Resource. We will 1st focus only on those, but later the payload will also include any predecessor objects - for example if the new object is a Request stemming from a Quote, the Quote ID. The new Objects initial requirement settings are then defaulted to the predecessor's matching ones (by Req Option ID), if any. Another example is a Customer Install Address - if its ID is in the payload, we will load any saved Requirement values for it. But until we have a new Request from a Quote, no need to worry about the inheritance.
    

Example for getting the options by category for a Request of type 1 - "Labor Quote - Internal"

The Object Types are in custom record: customrecord_orion_requirement_objects

Labor Quote Internal is ID 6

{reqObjectType: 6, predecessorObjectType: null, predecessorID: null}

Note: we can load them now just for the LQ request type, then later allow the predecessorObjectType to be "transaction" and supply a transaction ID - after we have saved requirements for at least one Quote

**Sample queries and code for the above in the file I emailed**

2. Loading the Requirement Options for an existing object, by Category, based on the Requirement Object type and ID. Since this object exists, it has its own saved Requirement Values, even if they initially defaulted from a predecessor. Therefor we do not need to look up predecessor requirements. We still need all of the available Req Options, by Category, based on the Requirement Object type, as the user may need to modify them. The additional need here is to join in the requirement values record and include any saved data.
    
3. Saving Requirement Values for a new object.
    
4. Saving Requirement Values for an existing object.
    

**Default Requirements data we deploy with:**

**Requirement Objects:**

- Quote
    
- Order
    
- Work Order
    
- Request Type - Labor Quote Internal
    
- Request Type - Design Quote Internal
    
- Site Conditions
    
- Labor Resource
    

**Requirement Categories:**

- Design
    
- Project Management
    
- Financial
    
- Delivery & Installation (or Operations - existing Dealer names vary)
    
- Labor Requirements
    
- Site Conditions
    
- Labor Resource
    

**Requirement Category Object:**

|**Requirement Object**|**Requirement Category**|**Display Order**|
|---|---|---|

|   |   |   |
|---|---|---|
|**Requirement Object**|**Requirement Category**|**Display Order**|
|Quote / Order|Design|1|
|Quote / Order|Project Management|2|
|Quote / Order|Delivery & Installation|3|
|Quote / Order|Financial|4|
|Work Order Event|Delivery & Installation|1|
|Work Order Event|Labor Requirements|2|
|Work Order Event|Site Conditions|3|
|Site Conditions|Site Conditions|1|
|Labor Resource|Labor Resource|1|
|Request Type - Labor Quote Internal|Delivery & Installation|1|
|Request Type - Labor Quote Internal|Labor Requirements|2|
|Request Type - Labor Quote Internal|Site Conditions|3|
|Request Type - Design Quote Internal|Design|1|

**Requirement Options**

**Work Order**

Client-requested Install Date

Hourly Job

Status Reports (dropdown)

Work Order Photos

Remove Existing Product

Product Returning to Warehouse

ServiceNet #

**Design**

xDesign Due Date onoff date

xSpecs onoff text

xDrawings onoff text

xInstall Prints onoff

xRenderings onoff text

xDesign Double Check Needed onoff text

xDesign Double Check Completed onoff date text (date) (who)

**PM**

Labor Quote onoff text

Site Verification onoff text

Customer Project Meetings onoff text

Customer Inventory onoff

PM Triple Check onoff date

Post-Install Inspection onoff text

Send Survey onoff email (Survey recipient email)

Project Sq Footage (number)

Quote Due to Customer onoff date

**Operations**

Customer Pickup

Work Orders Needed

Prevailing Wage onoff text

Night Job onoff text

CAM Pulls

CAM Return

MKPS

Pre-Install Meeting onoff date

Full PPE Needed? onoff text

Meet at Site

Crate Dropoff/Pickup

ID required onoff text (Govt/Military, Passport, Enhanced DL, Birth Cert/ID)

Vaccinated Only onoff text (booster?)

Travel Needed

Keyed Alike

Grommets

Plumbing (select - what were the options?)

Electrician (select - what were the options?)

Site Protection ((select - what were the options?))

Data Face Plates

Track Mounts

Surface/Panel Cuts

Existing Product Removal (select - what were the options?)

Trash Removal (select - what were the options?)

Power or Date Poles

**Labor Reqs**

After Hours/Weekend

**Financial**

Procurement Order Instructions onoff text

Send Quote

PO Required

Deposit Required onoff number percent

Use Contracts onoff text (Contract #s)

Desired Product Margin onoff um percent (Margin %

Desired Labor Margin onoff um percent (Margin %

Direct Bill - Send CAF onoff date text (Date Sent) (Sent To)

Invoice when Product Received

Invoice when Punch Complete

Invoice With (order # - (and here we had the special open button)

Financing Requested onoff date text

Financing Approved (same)

**Work Order**

Product Returning to Warehouse

Trash Removal - Install

Trash Removal - Customer

Wall Mounts

Track Mounts

**Labor**

Hourly Job

Normal Hours

Overtime Delivery

Doubletime Delivery

Overtime Install

Doubletime Install

Union

**Site Conditions**

Keys needed to access building?

Dock Available

Dock-Restricted Hours

Dock-Height Limitations

Dock must be scheduled (Dock Contact)

Commercial Vehicle Parking

Forklist required?

Ramps needed?

Are floors finished?

Wall protection required?

Steps or other obstructions?

Elevator Available (select with type)

Elevator - Restricted Hours

Elevator - Size Restrictions

Elevator - Must be Padded

Stair Carry (Which Floor?)

No Phones/Electronics

Escort Needed (who is contact?)

Walls - Drywall

Walls - Block

Walls - Glass

Electrical - Floor

Electrical - Ceiling

Electrical - Wall

Data - Floor

Data - Wall

Data - Ceiling

Certificate of Insurance Required

---

## Testing and Quality Assurance

Test Script Title: Requirements Feature Test Script

Test Objectives:

1. Verify that dealers can create, customize, and manage their own pre-order checklist items within the Requirements feature.
    
2. Ensure that the data-driven approach accurately displays and validates checklist items based on the defined data structure.
    
3. Confirm that the Requirements feature seamlessly integrates with the existing business system and order processing workflow.
    

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