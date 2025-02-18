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
    - 8.3 [UI Considerations](#UI-Considerations)
    - 8.4 [Scripts and Automations](#Scripts-and-Automations)
- 9 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 9.1 [Unit Tests](#Unit-Tests)
    - 9.2 [Process Tests](#Process-Tests)
- 10 [Time Estimate](#Time-Estimate)
- 11 [Changes And Revisions](#Changes-And-Revisions)
- 12 [Script Endpoints](#Script-Endpoints)

## Overview

Furniture Dealers have a need to send Requests for various services. These requests can be to an Internal group, to an External provider, or to both. External Requests can be sent to multiple vendors. Internal Requests need settings to control who the Request goes to, by Role, Location, or User. The typical things a Dealer requests in this way are:

- Design Services/Quotes
    
- Labor Quotes
    
- PM Services/Quotes
    

But there can be more: a Request to pull customer-owned inventory for example, or for Flooring or AV services. Move Services. Refurb Services. Reconfigurations. A request for an on-site meeting. A Request for travel. And many things that aren’t typical but that an individual Dealer wants to track in this way.

Each Request needs to specify certain dealer-defined information about the Order/Project involved. A Labor Quote Request, for example, needs to communicate all the information an internal or external Labor Quoter would need in order to provide an accurate quote. This can include information about the product on the Order, conditions at the Customer Site, the Install address and distance from the Warehouse, specific services and requirements for the job, attributes required of the specific Installers (e.g. Badging), and even financial considerations such as Union vs Non-Union, and Prevailing Wage. Contrast a Design Request - there will be a lot of overlap with a Labor one, such as the Product information, but much of the information needed for a Labor Quote is not needed for a Design Quote. Other information however, is needed, such as the need for advanced Renderings, a “Lookbook”, Design double-checks, contract info, and more.

Rather than attempt to define each type of Request a dealer might want, and attempt to exhaustively list all the relevant requirements for each, we will make this a data-driven configurable and open-ended feature. We will include the typical ones, with a typical set of requirements, but each Dealer will be able to add, modify, inactivate them in all aspects, with no need for a Professional Services customization.

## Solution Type

·       Modules – extensive functionality that may include external integrations, frameworks – big stuff

·   

## User Stories

Add 1-3 User Stories

## Success Metrics

Outline how we know this solution meets our goals.

## Design

This feature will be a SuiteApp Suitelet, and will also consume Restlet Endpoints created to return/save data.

It will be accessible from a variety of other interfaces, for example when on a Quote the user should be able to click something and open the interface for a new Request tied to the Quote. They should also be able to see existing Requests on a Quote or Sales Order, and probably other places, such as the ability to open a Labor Quote from a Work Order.

The Request Suitelet will utilize the Requirements Engine for the purpose of letting the Dealer specify the job/design/etc requirements. **(reference the Order Requirements Engine solution design)**

A Request will also have other fields such as notes. It can have attached files/documents.

And, if it is a type that can be Quoted, it will have specific quote fields broken down into the level of detail the Dealer wants to have. These fields will be in rows that can auto-calculate - for example one row for Install Labor would have a field for # Installers, Reg Hours, Overtime Hours, Reg Rate, OT Rate and a Total. Another row might be the number of vehicles, their type, hours needed, distance, etc. Another might be for Materials, or Parking.

A Quoted Request can be “Accepted” or “Awarded”. Doing so can optionally create Lines on the Quote or SO with the cost information, and any sell the acceptor wants to add. The Request will keep track of the Line UUID, so that if the quote is modified, the lines can be also - up to a certain point of course.

Visibility to Requests will need to be provided in portlets or dashboards that certain roles will have access to. Each Request will have a Status, and it is TBD if different Request Types will need differing statuses. The Kanban solution design will likely be used as well to display Requests of a filterable type in a card format that will allow for a nice visual look.

We will create an Admin/Setup area for a dealer (or us on their behalf) to manage their Request Types, Templates, Fields and other settings.

## Features and Functionality

We will define a record for a list of Request Types.

Each Request Type will have fields controlling how the Request will be created, routed, quoted or otherwise responded to, including:

- Request Type Name
    
- If available to submit Internally, Externally, or Both
    
- If a Quote is required
    
- If self-quotable
    
- default due days
    
- and more
    

Each Request Type will also tie to one more Request Template Items. The template items are where we specify the informational fields on the request - such as instructions. They also specify which quotable rows appear and in which order. Each row consists of Template Fields, which have their own properties.

The Requirements Engine will be enabled for each Request Type, and the list of Requirement Options for each type will be definable in an Admin/Settings Suitelet (this has been built already in the previous project.)

Crappy diagram:

## Technical Considerations

Enter any guidance to our developers with regards to NetSuite (ie: I envision this to be a customer record/field etc and it should trigger on save of record)

## Technical Specifications

## Object Definitions

- Request Type
    
- Request Template Line
    
- Request Template Fields
    
- Request
    
- Request Template Values
    
- Request Field Values
    

## Data Design

_**Custom Lists**_

**customlist_orion_request_status**

- New - or maybe Unsent
    
- Awaiting Quote
    
- Assigned for Quote
    
- Quoted
    
- Assigned for Work
    
- Information Needed - aka sent back, declined, rejected
    
- Accepted
    
- Cancelled
    

**customlist_orion_request_field_types**

- Checkbox
    
- Date
    
- Dropdown - Single
    
- Dropdown - Multiple
    
- Lookup
    
- Number
    
- Text Field
    
- Text Box
    
- Yes/No
    

**customlist_orion_request_display_units**

- (None)
    
- Each
    
- Hours
    
- People
    
- Days
    
- Dollars
    
- Trips
    

_**Custom Records**_

**customrecord_orion_request_type**

custrecord_reqt_all_locations (checkbox)

custrecord_reqt_locs (multi)

custrecord_reqt_internal (checkbox)

custrecord_reqt_external (checkbox)

custrecord_reqt_display_order (int)

custrecord_reqt_needs_quote (checkbox)

custrecord_reqt_self_quotable (checkbox)

custrecord_reqt_can_have_hours (checkbox)

cuatrecord_reqt_has_due_date (checkbox)

custrecord_reqt_default_due_days (int)

custrecord_reqt_has_exp_date

custrecord_reqt_default_exp_days (int)

custrecord_reqt_is_assignable (checkbox)

**customrecord_orion_req_type_recipient**

custrecord_reqtq_request_type

custrecord_reqtq_recipient_emp (multi, emp)

custrecord_reqtq_recipient_vendor (multi, vendor)

custrecord_reqtq_all_locations (checkbox)

custrecord_reqtq_locations (multi, location)

**customrecord_orion_request**

custrecord_req_quote (trans id)

custrecord_req_order (trans id)

custrecord_req_type (req type)

custrecord_req_status (status id)

custrecord_req_due_date (date)

custrecord_req_requested_date (datetime)

custrecord_req_expire_date (date)

custrecord_req_assigned_to (emp)

custrecord_req_quoted (datetime)

custrecord_quoted_by_emp (emp)

custrecord_sent_to_vendor (vendor)

custrecord_sent_to_vendor_contact (contact)

custrecord_req_accepted (date)

custrecord_accepted_by (emp)

custrecord_total_cost (decimal)

custrecord_total_sell (decimal)

custrecord_total_gp (decimal)

custrecord_gp_percent (decimal)

**customrecord_orion_request_template_row**

custrecord_reqtr_all_locations (checkbox)

custrecord_reqtr_locations (multi)

custrecord_reqtr_display_order (int)

custrecord_reqtr_default (checkbox)

custrecord_reqtr_required (checkbox)

custrecord_reqtr_allow_multiple (checkbox)

custrecord_reqtr_calc_from_rest (checkbox)

custrecord_reqtr_calc_order (int)

custrecord_reqtr_is_fill_in (checkbox)

custrecord_reqtr_is_subtotal (checkbox)

_(below fields only for when they want it to become a line on the transaction)_

custrecord_reqtr_default_vendor (vendor)

custrecord_reqtr_default_item (item)

custrecord_reqtr_default_prodid (text)

custrecord_reqtr_default_proddesc (text)

**custrecord_reqtype_template_row**

custrecord_reqtyperow_type (Request Type)

custrecord_reqtyperow_template (Request Template Row)

custrecord_reqtyperow_display_order (int)

**customrecord_orion_req_template_fields**

custrecord_reqtf_template_row (Request Template Row)

custrecord_reqtf_field_type (Request Field Type)

custrecord_reqtf_is_label (checkbox)

custrecord_reqtf_is_qty (checkbox)

custrecord_reqtf_is_rate (checkbox)

custrecord_reqtf_is_reg_time (checkbox)

custrecord_reqtf_is_overtime (checkbox)

custrecord_reqtf_is_doubletime (checkbox)

custrecord_reqtf_is_num_people (checkbox)

custrecord_reqtf_is_line_total (checkbox)

custrecord_reqtf_display_order (int)

custrecord_reqtf_in_row_calc (checkbox)

custrecord_reqtf_allow_direct_entry (checkbox)

custrecord_reqtf_exclude_from_total (checkbox)

custrecord_reqtf_is_denominator (checkbox)

custrecord_reqtf_numerator_field_id (int)

custrecord_reqtf_numerator_factor (decimal)

custrecord_reqtf_placeholder (text)

custrecord_reqtf_css (text)

custrecord_reqtf_display_unit (Request Display Units)

_(below here are fields relating to the field type)_

_(for field types text field and text box)_

custrecord_reqtf_default_text

_(for field type number)_

custrecord_reqtf_number_type (Requirement Number Types)

custrecord_reqtf_allow_negative (checkbox)

custrecord_reqtf_number_min (int)

custrecord_reqtf_number_max (int)

custrecord_reqtf_number_step (int)

custrecord_reqtf_default_number (decimal)

_(for field type select)_

custrecord_reqtf_select_values (textarea)

custrecord_reqtf_select_labels (textarea)

custrecord_reqtf_select_default (text)

_(for field type lookup)_

custrecord_reqtf_lookup_type (Requirement Lookup Types)

custrecrd_reqtf_lookup_default_id (int)

**customrecord_orion_request_field_values**

custrecord_reqfv_request (request id)

custrecord_reqfv_template (template id)

custrecord_reqfv_field (field id)

custrecord_reqfv_value_text (text)

custrecord_reqfv_value_number (decimal)

custrecord_reqfv_value_select (text)

custrecord_reqfv_value_lookup (int)

custrecord_reqfv_value_date (date)

custrecord_reqfv_value_on_off (checkbox)

custrecord_reqfv_value_yes_no

**customrecord_orion_req_template_values**

custrecord_reqtrv_request (request id)

custrecord_reqtrv_template (template id)

custrecord_reqtrv_lineuuid (line uuid)

custrecord_reqtrv_total_cost (currency)

custrecord_reqtrv_total_sell (currency)

custrecord_reqtrv_total_gp (currency)

custrecord_reqtrv_gp_percent (percent)

custrecord_reqtrv_sell_line_uuid (line uuid)

## UI Considerations

**Existing Catalyst samples**

_Dashboard (logged in as a Quoter)_

_Opening a Quoted LQ - the old design had a lot of vertical scrolling - we could use tabs now_

_The Template Lines specified for this Request Type in the database are rendered dynamically:_

And same for the Requirements - these are initially inherited from the Quote but can be overridden and added to for the LQ. They are what this dealer thinks their Labor Quoters need to know.

Notes - we should talk about both Notes & Documents - they are a big deal to the dealers. In Connect (and see COR later), Notes are centralized in one record, and the ID of the transaction or entity or custom record they belong to is stored there. They have a Note Type - a list configurable by the dealer. Here you see a Scope note created by the requestor, and a Quoter Note added by the Quoter.

Documents/Files are similar - one record with the ID (and type) of thing they are attached to.

_Actions (with lame icons):_

- Save
    
- Cancel
    
- Send to Quoter
    
- Accept and Add to transaction lines
    
- Un-accept and remove transaction lines
    
- Send Quote back to Requestor (puts it in status “Information Needed” and alerts)
    
- Submit Quote to Requestor (puts it in “Quoted” status and alerts)
    

_A Quoted and Accepted LQ (logged in as the Requestor)_

The template lines/fields/totals still appear, but disabled. Probably could have made that more concise since this user cannot edit them.

When the LQ has been Accepted, it shows the information from the Lines. Note the top line - some dealers like to have all of the detailed breakdown as cost-only lines, and consolidate them all into one Sell line. The Cost lines are hidden from the Customer, who sees only the Sell line. The feature can do that for them, if they enable that option.

_When on an open Quote/Order, an Order Team member can request a new Quote:_

_They select one of the defined Types, and options specific to that type appear:_

The “Pricelist” quote (what Catalyst calls this type) is for smaller jobs where they use a spreadsheet of common simple delivery/install tasks. Many dealers allow their people to do this as long as the total labor cost is under a certain threshold. These are not routed to the Quoters, but can still be reviewed by them if desired. Note: we should allow for these, and someday seek to bring the spreadsheet or other things they use into the system a la IQ)

Since a member of the Order Team is allowed to enter these, they can also choose to Accept and add lines to the Quote/Order. If they do that, additional options appear:

They can choose to add a new labor line, or to update an existing one.

They can enter an external Quote also - like one obtained from a Service Provider or Intermarket network dealer:

With an External quote, they get the same Accept and add to order options as with a Pricelist quote

Note: We can improve this by letting the send the request to external quoters, who can enter the quote online using a suitelet with no authentication needed. Then the dealer wont have to type in the info - it will be saved automatically, and the Requestor alerted.

You can see that in Catalyst’s existing system, they have all this only for Labor Quotes. But our version will abstract that to any kind of Request, each with different Requirements and Template Lines.

Finally, they can Save, and once saved, Send. Being able to save one they are working on and Send when ready is good.

**COR Samples**

So COR does it a bit differently. They created their own system they call Project Registration. But, it isn’t a Project in the sense we would think - it is just a Quote in Core (note the Quote # field below.) They fill this out, and indicate what kind of services it will need at a high level, and then when they check “Ready for Labor Quote”, the Quoter(s) gain visibility to it.

_This is their equivalent of Requirements - they are not configurable and need to be changed in code when they change:_

**Note** the Change Log above - they said that is very important to them. To see the history of the Requests, who did what, and when.

COR does NOT do Quotes for Design or PM - that is why they have only checkboxes for “Design Services Needed”. There is no design Quote, they just add a traditional “load” or “burden” cost to each Order, based on a percent of the total cost. So for them a Design Request is really just asking the Design Manager to assign one or more Designers.

Our Request Types will have a field for “is_quote_needed”, so that we can let the dealer choose how they work - since probably most of them DO want things like Design to be quoted.

_For an Internal Quote, this is what the Quoter enters:_

_When COR sends an LQ Request to an external Subcontractor, it emails a PDF:_

_When they receive an email reply from the Sub, they type it in here:_

Most of their subs will send back just the top total number, but they may detail some additional costs.

_They track Quote Revisions by appending a number:_

## Scripts and Automations

Endpoints:

1. Loading the Requirement Options for a new object, by Category, based on the Requirement Object type. Payload will include the Requirement Object type (Quote, Order, Request Type (e.g. Labor Quote, Design Quote, etc), Customer Site, Labor Resource. Payload must also include any predecessor objects - for example if the new object is a Sales Order or Request stemming from a Quote, the Quote ID. The new Objects initial requirement settings are then defaulted to the predecessor’s matching ones (by Req Option ID), if any. Another example is a Customer Install Address - if its ID is in the payload, we will load any saved Requirement values for it.
    
2. Loading the Requirement Options for an existing object, by Category, based on the Requirement Object type and ID. Since this object exists, it has its own saved Requirement Values, even if they initially defaulted from a predecessor. Therefor we do not need to look up predecessor requirements. We still need all of the available Req Options, by Category, based on the Requirement Object type, as the user may need to modify them. The additional need here is to join in the requirement values record and include any saved data.
    
3. Saving Requirement Values for a new object.
    
4. Saving Requirement Values for an existing object.
    

**Default Request Types we deploy with (likely to grow when we can create them in the Orion interface):**

- Labor Quote - Internal
    
- Design Quote - Internal
    
- Labor Quote - External
    
- Design Quote - External
    
- ?
    

**EMAIL TEMPLATES**

So far we have two Request Types defined (in customrecord_orion_request_type)

- Labor Quote - Internal
    
- Design Quote - Internal
    

There will be more, but they are just data so they will do for now. Dealers will be able to create their own, and each Request Type can have its own Email Template. They can also use a generic template, so I think we start with that.

I have not created any Email Templates in NetSuite, so I’m not aware of the functionality available. But as a starting point, I think we would want each to have:

The word “Request” and then the Request Type name as the subject (e.g. Request: Labor Quote - Internal)

The actual Request data is in customrecord_orion_request. Data we should include in the email template would be:

- A free-form instructions field the dealer can put anything they want in.
    
- The Quote or Order number (the request record has at least one of these)
    
- The Request Due Date - if any (not all types support Due Date)
    
- The Request Originator Note - with value
    
- For employees, a link to the specific Request (if the Request has its “Internal” checkbox field set to true) Clicking this link will take them to the place where they can process the request - supplying a quote is the typical expectation.
    
- A section where we render the Requirements for this Request. Those can be found in record customrecord_orion_requirement_value. So far we have them only for Request ID 10. There can be any number of them, and to get them in SQL you have to specify both the custrecord_rv_object_id value (e.g. for Request ID 10, 10) and the custrecord_rv_object_type value (from customlist_orion_requirement_objects) - a Request of type Labor Quote - Internal is requirement object type 6, for reference. You join in customrecord_orion_requirement_options to get the option’s name.
    

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
        

## Script Endpoints

Request Engine Endpoint

Script ID: customscript_or_request_engine_endpoint

Deployment ID: customdeploy1

Requirements Engine Endpoint

Script ID: customscript_or_requirements_engine_gen

Deployment ID: customdeploy1

Be the first to add a reaction