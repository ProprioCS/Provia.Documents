- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
    - 5.1 [Receiving:](#Receiving%3A)
    - 5.2 [Expected Receipts](#Expected-Receipts)
    - 5.3 [Work Orders](#Work-Orders)
    - 5.4 [Scheduling Interface](#Scheduling-Interface)
    - 5.5 [Field interface (not necessarily an actual NetSuite user)](#Field-interface-\(not-necessarily-an-actual-NetSuite-user\))
    - 5.6 [Placeholder Work Orders](#Placeholder-Work-Orders)
    - 5.7 [Hold List](#Hold-List)
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

The Provia Operations modules encompass several different aspects of a typical dealer's "operational" practices. These include:

Receiving POs into one of the Dealer's Warehouses, using Bins, with an improved interface over the default NetSuite Inventory Detail popup.

An Expected Receipts Calendar, which shows both past and upcoming Receipts in a calendar view.

A Work Orders sublist on a Sales Order, which allows you to see a list of that Order's Work Orders, open them, and create new.

The ability to control all aspects of a Work Order, from the Type, to the number of Events and their Types, to the number of days the work will go on for. The Work Order interface utilizes the Requirements Engine for communicating the work requirements for the specific job.

A Work Order calendar/schedule allowing most roles to see what work is upcoming (or past), the Work Order status, and other important summary information. They default to seeing their Work Orders, meaning the Work Orders tied to Orders they are on the Order Team for. But they can filter to see All.

A Scheduling interface used by the Scheduler (aka Dispatcher, aka Operations Manager). This interface is used to Approve Work Orders, to group them into Routes, to assign Labor Resources (people, subs, trucks, etc), to Complete Work Orders, and to enter time worked (when that was not done in the field), and other functions, including a Map view.

A Hold List where Work Orders can be "parked" when you don't know exactly when you will be able to get to them.

A mobile-optimized field application used to see all information about a Work Order while in the field, Complete it, send Status reports, obtain the Customer Signature, create Punch, notify the Warehouse about unexpected returning product, take photos, and more.

An Administrative area where the Operations Manager (or System Admin) can manage their Work Order/Event Types, Labor Resources, and other settings.

## Solution Type

·       Modules – extensive functionality that may include external integrations, frameworks – big stuff

·  

## User Stories

Due to this already having been developed, and the sheer number of them, user stories will not be listed at this time.

## Success Metrics

Due to this already having been developed, and the sheer number of them, success metrics will not be listed at this time.

## Design

We do not have this in our account yet, but it will be migrating (with adaptations to our architecture/fields). We do have some screen grabs from the previous effort, but not all of them.

## **Receiving:**

To replace the standard NetSuite interface for receiving POs, a suitelet was developed. It was accessed by a button added to the PO form called "Provia Receiving". The standard NetSuite Receive button was removed/hidden. The Provia Receiving button only displayed on Special Order POs, not Drop Ship POs. When Provia Receiving was clicked, the suitelet opened in a new tab, and then the client script called an endpoint to load the PO items and list of Bins for the Warehouse the PO was shipping to. It allows for listing the items on the PO - just some basic information. It also has fields for the Bin the item should be received to, and the Qty placed in that Bin. To the right of this is a box displaying all the Bins for the Warehouse that the PO was shipped to.

The user can select items using the checkboxes, with a Select/Deselect all at the top. They can also select using Shift and Ctrl, so they don't need to click every box. They can then drag the selected items onto a single Bin and drop them. This will fill that Bin name into the items' Bin field, and in the case of a single Bin, put the Item's PO Qty into the Bin Qty field.

The user can also do the reverse - select one or more bins and drag them to a single Item. In this case, the user needs to specify the Qty to go in each of the multiple bins. They are not allowed to receive more than the PO Qty (see OverReceipts later for how those can be handled - in presold furniture the risk of accidentally receiving too many is not worth allowing it. Flooring is a different case.)

In either direction, the user can select multiple destination objects (Items, or Bins), and then drag multiple source objects on to them, creating a many to many scenario - e.g. I want the 3 selected Lines to go to the 2 selected bins. Again, in this case, they need to adjust Qtys for each bin. This makes the simple case extremely simple, while allowing for complex cases. For example, if I want to receive every one of the 500 Lines on the PO to a single Bin called "Staging", I can simply check the top "Select All" checkbox, and then drag any item to the Staging Bin. All of the selected items will then be set to go there, in full Qty. Then click Save.

A Warehouse may have many Bins, or few Bins. And Bin Names are up to the Dealer and can be long or short. For this reason, the Bins box allows the Dealer to choose how many columns the Bin names are displayed in. This can also be defaulted, per Warehouse, so they do not need to keep changing it each time. This allows them to fit more of their Bins on the screen without scrolling.

Similarly, they can type into the filter box any part of a Bin name, and it will hide all the Bin names which do not match. Clicking the X in the filter field will clear any filter they have typed, and show all the Bin names again.

Note that since the list of Lines can be quite long in some cases, as the user scrolls down, the Bins box follows so that they always see it next to where they are in the Lines, stuck to the top of the visible viewport.

Existing Receipts can be removed using the X icon, and are removed on Save.

The little Info icon allows the user to enter a Receiving Note for that item/bin/qty.

  
It also allows the user to create what we called a "Component Receipt". This is a situation which can arise with certain manufacturers (e.g. Knoll), where they do not ship the full item at the same time. A simple example is you order 4 tables, and then a truck arrives and they have parts of those 4 tables. It isn't that they shipped 2 complete tables - that is easy to handle, as you simply receive the 2 which came, instead of the full 4. This scenario is when they send you 4 tops - but 0 bases. How many tables do you have now? You don't have 4 complete tables. If you receive a Qty of 2 - the system thinks you have 2 complete tables, but you do not. The correct answer is 0 - you have received 0 complete tables. However, you did receive 4 tops, and want to put them into a bin or bins, and record where you put them for later, when the bases arrive. Our approach was to store this in a custom record called receiving_extra. The user could type in a brief description of what they received (e.g. "4 tops"), and still select a Bin or Bins to put them in. They could also enter what was still expected (e.g. "4 bases"), and had a date field where they could put the expected date - which we were told is sometimes communicated in this scenario.

Finally, this is where we would also allow them to record an intentional Over-Receipt. We did NOT put any overage into the NetSuite Item Receipt - because that would change the financials on the Order. The intention here was to simply record it, and display it here for this PO, and likely have a saved search that would show them any actual over-receipts they had to deal with. They might go ahead and adjust the PO (and then sync to the SO), or they might transfer ownership of the overage to the Dealer and have it be in Stock. We did not get any further with this situation, other than letting them record it and storing it in the custom record.

Finally again - there was another scenario with Walls Orders that COI brought up, one that we have not yet solved for. In this scenario, they enter a single line for all the product on a Walls Order. It has a Qty of 1 Lot. And yet in fact it consists of scores of separate items, which when received will need to be placed into multiple bins. Because the line Qty is 1, we were not letting them put it into more than 1 Bin. What will be needed to handle this will be a concept of "additional bins", used when a single Qty item is "too big" to fit in a single Bin, and can "overflow" to additional Bins. The NetSuite Item Receipt will show that 1 was received to the primary Bin, and a custom record will store the list of additional bins it is in.

## Expected Receipts

This Suitelet displays a calendar view, defaulting to the current week. Within that calendar view, it shows all POs as tiles that:

- Have been fully received this week
    
- Have been partially received this week
    
- Are expected to be received this week.
    

The greenish tiles are fully received. The yellowish tiles are partially received. And the pinkish tiles are expected receipts.

The Expected Receipt date is calculated from the historical experience of the dealer when receiving product that had an Ack Ship Date. In Provia Receiving, when items are received, we track how many days from their Ack Ship Date it took for them to get here and be received. We store this in the database by Vendor ID, Vendor Ship-from Zipcode, and Destination Zipcode (which is often a Dealer Warehouse location, but can also be a Customer Location for Direct Ship POs, or a Subcontractor location for POs shipped to a Sub.) This way a Dealer with multiple warehouses in different regions, and/or a Vendor with multiple manufacturing facilities, will store the correct value for this PO/Ack. And for items shipped to a Customer Location or Sub Location, the expected date will be pretty accurate as well.

We store (currently 12) of the most recent receipts for that Vendor/Origin Zip/Destination Zip, and use the average of those 12 (or however many we have if fewer than 12) to calculate the average transit days, which are then added to the Ack Ship Date to form the Expected Receipt Date.

If we do not have any stored transit information for the particular Vendor/Origin/Destination, we display the PO on its Ack Ship Date and instead of a date, show "TBD". As receipts happen, this will self-correct.

If vendors get better at getting product to the dealer, or (we hope not!) worse, the average transit days will start to shrink or grow with each new Receipt, and so the Expected dates will continually self-correct.

When looking at previous weeks, you see any actuals, and also see any Expecteds which land on those dates and have not yet been received. But when looking at the week which includes "today", meaning today's actual date, it works in a special way. When looking at the week which contains "today", every unreceived PO that was expected before the currently-viewed week will show up, and will show up on "today".

In this way, POs that were expected earlier but have not yet been received will always roll forward to the current week. This helps ensure visibility is not lost – you do not need to go back in time to hunt for them – they will display this week until they are received. Another way to put is this: today is Monday, and we had a PO we expected to arrive on the previous Friday, but we have not received it. It will show on today (Monday). If not received today, then tomorrow it will appear on "today" again, which will now be Tuesday. And so forth – until it is actually received. Once received, it will then be frozen as an actual receipt on that day.

But sometimes, things can go wrong, so we have some override capabilities. If you click the down arrow in the lower right, it opens an action menu:

The first item on the menu, "**Open in Provia Receiving**", does exactly that. There you can see the details for any actual receipts, either full or partial, and actually receive (if you have permission to create Item Receipts) unreceived/partial POs. The icon that is supposed to represent "boxes", located to the left of the menu arrow, does the same thing -  opens the PO in Provia Receiving, but without having to open the menu.

"**Stop Showing this PO**" – in the past in other systems we have seen bad data, and there have been POs that simply aren't going to be received. There was a need to just stop showing them, so they don't keep rolling forward to every new week. This should not be an issue in NetSuite, but at least for now you can select that item and that PO will no longer appear in Expected Receipts. Note that this wouldn't mean you couldn't receive it when the product actually arrives – you can still get to Provia Receiving from the PO, and likely from a Warehouse menu we will create. You just won't see it here anymore, because you said to stop showing it here.

"**Set Expected Date for this PO**" – sometimes a PO is calculated to arrive on a certain date, but you are informed of a problem by the Vendor or their Carrier – e.g. the truck broke down in Minnesota, or a mountain pass is closed. When you are informed of such a thing, you can set a hard Expected Date just for that PO, and thereafter it will only show as Expected on the date you set here. So if we have a PO with such a problem, and we are tired of seeing it show up every day when we know it isn't coming for a couple more weeks, we can simply enter an override expected date using this menu option – and it won't show again until then.

And should we find that despite our best efforts, some Vendor's averages are all over the map and we want the system to stop calculating for that Vendor, we can enter a hard-coded number of transit days for that Vendor. In that case, we can click "**Set this Vendor's Transit Days**" and enter a number of days, and from that point forward POs coming from that Vendor will show as expected on the day that is calculated from the Ack Ship Date plus the number you entered here.

These Overrides should not be needed often, but they are available for the occasional edge cases. It is best initially not to use them, but instead to receive POs as they arrive and let the system do the math and get better without any manual intervention.

## Work Orders

Work Orders are a set of custom records and suitelets intended to bring best of class Furniture dealer operations into NetSuite Provia.

Work Orders are always tied to a transaction, and almost always a Sales Order. One special type called a "Placeholder Work Order" can be tied to a Quote as well. There can be zero, one, or many Work Orders on any given Sales Order.

The Sales Order had a sublist to display information about each Work Order tied to it. This was done with SuiteQL as the Work Order's overall status is a rollup of all of its Events' statuses, and each Event can have multiple Days with their own status. For this reason, we added the query to the beforeload user event for a Sales Order and created the sublist on the server. We could (and probably should) instead use a client script to hit an endpoint for the data after the SO loads. The sublist also had a New Work Order button which would open the suitelet with no "woid" param, which meant it is a new one.

You could also open existing Work Orders from the Work Order Schedule, and from the Scheduler interface.

The Work Order suitelet form showed basic information about its Sales Order/Customer. It had a few fields in the header as well:

**Name**: The name of the Work Order. Required. (should default from the Order Name)

**Note**: This is where free-form scope of work information would be entered. Required.

**Placeholder**: a checkbox, not defaulted.

One of our Pilot dealers who have been using my old Connect product have "fancy notes". These allow HTML rich text, and for the pasting of image snips, or the drag/drop of image files into the note body.

This is very popular with that dealer (Catalyst), and so I previously incorporated it into the Work Order and Work Order Event notes. In real life, it generally does not contain a picture of my dog, but instead a variety of things that the dealer finds useful when communicating from the Order Team to Operations (which of course is what a Work Order is all about.) Often there are cnips of floor plans, for example, showing exactly where and how product should be placed.

_**(More about this below in Technical Considerations.)**_

A Work Order also had several Sublists:

- Addresses
    
- Contacts
    
- Line Items
    
- Files
    
- Events
    

Each of these sublists except for Events then had two subtabs - one which showed the list from the Sales Order or Customer, and one which showed the list assigned to this Work Order.

Take Addresses, for example. Under the Addresses tab, you would see a subtab called Customer Addresses. This showed a a list of all that Customer's addresses. Then you had a subtab called Work Order Addresses showing where this Work Order is going. The Customer Address specified as the Install Address on the Sales Order would appear here by default. However, you could also pick **additional** Customer Addresses - as sometimes a Work Order has multiple stops.

Contacts, Files, and Lines worked similary - you see what is on the Order, and select which apply to this Work Order. You could also add an ad hoc Address, Contact, or File, and these would apply only to the Work Order, without writing back to the Sales Order or Customer.

Finally, the Events tabs displayed a list of the Events created for this Work Order. A new Work Order requires at least one Event, but any number are allowed. It is very common for a Work Order to have several Events of different types.

Here are sample Work Order and Event Types (gleaned from a few existing dealers):

So a "Standard" Work Order might contain a number of Events, such as:

- Pre-Install Walkthrough
    
- Pre-Install Meeting
    
- CAM Pull
    
- Delivery & Installation
    
- Post-Install Walkthrough
    
- Punch
    

Each of these Events would typically be scheduled for different dates, have different Labor Resources assigned, and each would have their own status and completion data.

**Event Creation**

Currently, you create new Events from the Events sublist via a popup. It lets you select the Event Type, an optional name (if none entered is just inherits the Work Order name.) You can enter an Event-specific note, and then you have Scheduling Options. These let you pick the intended date(s) for the Event. There can be as many days as you think you will need. you can add dates manually, or use a bulk add feature that lets you specify how many days to add, and has checkboxes for whether to include Saturdays, Sundays, and Holidays.

Each Event can have a Time field - and this can be a specific time, but can also be things like "Anytime", "Morning", "Afternoon", "Night", "First Stop", "Last Stop".

**Work Order/Event Statuses**

Work Orders and Events share the same statuses. When a Work Order is Cancelled, all of its Events are also. When all Events in a Work Order are complete – IF all lines on the Work Order are also completed – then the overall Work Order is complete. The Statuses default to a standard set, but their display names can be edited. These are the standard set:

- Needs Approved
    
- Approved
    
- Reschedule Requested
    
- Locked
    
- Partial
    
- Complete
    
- Hold List
    
- Cancelled
    

## Scheduling Interface

There is a toolbar at the top of the Scheduling Interface, which consists of:

- A Save button
    
- Subcontractor Confirmation
    
- Operations Report
    
- Hold List (the button has a number beside it indicating how many Events are currently Hold-listed)
    
- A Date field, and arrows to move to the previous or next day.
    
- The day of the week.
    
- The "fullness" meter for the day – the Scheduler can set this, and the Order Teams can see how full a given day is when they go to select a date for their job. Note: we can support multiple fullness meters, in case the dealer wants to have multiple fullnesses for a day e.g. a day might be fairly open for Furniture, but very full for Walls, or Service or Moves, etc. By default there is only one.
    
- A Location filter – This will contain all Warehouse/Operations Locations that the logged-in Scheduler has access to. If more than one, they can filter per location. They can also see all.
    
- A Customer filter – this allows them to filter and see only the selected Customer's jobs on screen temporarily.
    
- A Salesperson filter – works the same way as Customer.
    
- A Types filter – this lets them select one or more Work Order and/or Event Types, and displays only the selected ones. The default is All.
    
- A Status filter – this lets them select one or more statuses and see only those. It defaults to all but Cancelled, but can be used to see those too (in the event that they want to Uncancel one).
    

- Search button – this lets them search for Work Order Events by Order, Work Order, or Event number.
    

- A list is returned, and from it the Scheduler can open the Event, or navigate within the Scheduling interface to any of its days.
    
- A Map View button
    

**Work Order Map View**

The Work Order Map View is accessed from within Work Order Management by clicking the Maps icon in the top right.

It opens a new window that then displays a map of the Events on that day:

Each Event displays on the map as a "job site" marker with a building icon:

While the Warehouse Location that was selected in Work Order Management displays a "warehouse" marker:

The panel in the top left shows the date, the number of Work Order Groups, and the number of Work Order Events:

It also has 3 buttons:

- "View Map in Normal Mode" (default)
    
- "View Map in Real-time Mode" (only available when you are looking at "today" – and is dependent on the Installers' tablets sharing their location.
    
- "Collapse or Expand All"
    

Below this is a panel showing all the Work Order Groups and Events for the day. Each group is randomly assigned a color (with the Ungrouped Events lumped together and always Gray):

Within each group, the Events are displayed with:

- Work Order Number
    
- Event Type color (hover shows the type)
    
- Schedule Type and/or Start Time
    
- Stop Number
    
- Work Order (or Event) Name
    
- Addresses
    

The job site markers for the Grouped events display in the same color as their group on the left:

Events with multiple addresses will have a job site marker for each address.

You can click any marker to see more details about that Stop:

You can collapse any group (or the ungrouped jobs), and their map markers will be hidden:

Re-expanding the group will show them again:

You can click on the header of any group, and it will draw the route from the warehouse to each Event, and then back to the Warehouse, in Stop Number order:

This view also shows the directions, and distance of each leg, along with a time estimate. Note: the time estimates are averages and can of course be different due to traffic conditions.

Clicking the same Group header again will hide its route, as will clicking a different one.

In the Ungrouped Events, this works a little differently. Since they are not grouped, you click the Event's header, not "Ungrouped Events". Doing that will show the route to the ungrouped event and back:

**Approving a Work Order Event**

When Work Order Events are created, regardless of who creates them, they appear in the Scheduling interface on the date for which they were created. They appear in the right pane, aka the "Unapproved" pane.

They display information about the Order/Work Order in a compact format:

The information included is:

Sales Order number – Work Order Event number. Both are links to open the object in a new tab in case the Scheduler wants to see the details.

Order Team icon – this can be a custom image derived from the Dealer's logo, for example in the MK sandbox we are borrowing Catalyst's. Clicking this will show the Order's Team – in case the Scheduler wants to contact one of them without having to open the whole Sales Order.

Collapse arrow  when clicked, this will collapse the Event into a smaller, less detailed format. There is a corresponding Collapse All button at the top of the Scheduling interface.

When a Scheduler drags them to the left pane (aka the "Approved" pane), their status changes from Needs Approval to Approved. The Scheduler can leave them in the Unapproved Pane until deciding when to do them. The Scheduler has the permission to simply reschedule them for a different date. The Scheduler can also send them back to the originator and request that person to reschedule them for a different date. If she does this, the Event changes to "Reschedule Requested" status, and the originator is notified. The Scheduler can optionally include a short note with the request, perhaps to explain why the original date does not work, or to provide coaching on a date range that would be more acceptable.

**Locking Events**

Locking happens automatically when resources are assigned to an Event. When an Event's status changes to "Locked", non-Schedulers can no longer make modifications to it. If modifications are needed after that point, the Scheduler must be asked to Unlock the Event. This prevents people from changing an Event's scope or product list or address after the Scheduler has already processed it and assigned resources, without the Scheduler's knowledge.

The Scheduler can also manually Lock or Unlock an Event at any time.

**Grouping Events**

In the Scheduler interface, Groups can be created. They are free-form and can be named anything – a calendar direction/destination like "South" or "Bainbridge Island", after the Lead (e.g. "Carlos"), after a Project or Customer (e.g. "T-Mobile Mac"), etc. The group header block appears at the top of the Approved pane. Events can then be dragged into the group, from either pane. Within a Group, Events can be dragged up or down to change the stop number order. Groups can be created ad-hoc for the current date, or dragged over from a Groups Library on the left, which contains Groups that are used often, so that they don't need to be created over and over on specific dates. Within the Group Library, the Scheduler can auto-create a Library Group on future days. Some Groups are used almost every day, e.g. one called "Service". Putting those on all future days for the next Quarter or so means they won't need to be added for every day as the Scheduler gets to it. However, they can be removed from a day, if for example the Service Tech is on vacation one week and no Service Events will be scheduled then.

**Assigning resources to Events/Groups**

The Resource pane on the far left contains all of the Labor Resource, Vehicles, Tablets, and any other kind of resource the dealer wants to assign specifically to Work Order Events. These can be put into dealer-created/maintained categories in the Work Order Settings -> Operations Resources area. You can drag any resource to an Event, or to a Group. When events are grouped, the assignment is to the group. Adding more Events to the Group does not require changing the resource assignments. Ungrouped Events can also be assigned resources individually. Resources can also be removed from the Event or Group, by clicking the Action menu arrow.

This is also how you can designate one or more people resources as the Lead.

Resources in the Resource Pane also have an Actions menu. This allows the Scheduler to indicate that the Resource called off that day, or to enter scheduled time off in the future. They then become unavailable for those days. You can also make non-people resources unavailable – for example when a truck is scheduled to be in the Shop for some days, or an iPad is at the Apple store being fixed.

Resources also support Customer Restrictions and Customer Preferences. This is for those situations which unfortunately arise where a Customer has asked you not to send a particular resource to their jobs. The flip side of this is a new thing, to allow indicating that a particular resource is preferred by the Customer. Knowing that allows the Scheduler to assign the Customer's preferred resource(s) to their jobs, if feasible.

**Completing a Work Order Event**

In the Office, a person with the Scheduler role can complete an Event. This is typically done by people in the Field, but if they did not or could not do so for some reason, it can also be done in the office, with the exception of the Customer signature (since that cannot be obtained when not in the field.) When Lines on Work Orders are completed in full Qty, it is recorded to a custom record called Work Order Completion. Item Fulfillment records were also created for the completed lines - but will no longer need to be given our new use for Item Fulfillments.

We do not have screen grabs of Completing a Work Order Event at this time, but will when we have it running in our accounts.

## **Field interface (not necessarily an actual NetSuite user)**

The Field interface is a Suitelet which does not require a login, and uses a Restlet to retrieve and submit data to the dealer's NetSuite instance. This allows the installers (and perhaps service providers) using the field interface to not be actual Netsuite users with a login.

We do not have screen grabs of it currently - it was done late in the former project and not documented, so as not to share it with you know who.

**Viewing assigned Work Order Events for a given day**

When the Provia icon is tapped on the device, it will load a list of the Events that device is assigned to for the current day. The date can be changed to provide a view of past or future days. The Events are listed in Stop Number order. Tapping an Event will load all of its data, including:

- Basic information about the Work Order, Event, Sales Order, Customer Location(s) and Contact(s).
    
- The Work Order Note
    
- Work Requirements for this Event
    
- The assigned Roster of internal or external labor resources assigned to the Event.
    
- Line Items/Qtys (either for the Event if lines were added, or for the overall Work Order otherwise)
    
- Files associated with the Work Order (with any specifically associated with the Event at the top and highlighted)
    

**Completing Event Lines and Events**

Each Line Item has a column for Completed Qty next to the Line Qty column. Each Line also has a checkbox to mark it as complete, which will put the Line Qty into the Completed Qty column automatically. There is also a checkbox at the top to complete all of the lines and fill in their Completed Qtys. Lines can be marked as completed as you go, or at the end of the day.

There is a button to Save whatever has been entered, and this can be tapped at any time.

There is a button to send a Status Update. This does not complete the Event, but allows sending interim updates, optionally including time worked, signatures, and any other information entered.

There is a button to Complete the Work Order Event. This typically will also send a Status Update as well. If Event Lines are used, this button will only be available if all the Event Lines have been completed. If Event Lines are not used, this button will be available only if all the Work Order Lines are completed.

We plan to add a new capability here for working offline, because sometimes a customer site does not allow connectivity, or simply has a very week signal. Offline mode will let you download the Event information when you DO have signal, in advance, and work with the information while offline. When connectivity has been restored, you can upload the information you have entered, including any completion or status updates. We will just use the browser's offline mode capabilities with local storage to accomplish this.

**Entering Time Worked**

Above the roster, there is a section where you can enter a start time and end time, and optionally time off (e.g. lunch). When you do this, it will calculate the time worked, and divide it into Regular, Overtime, and Double Time based on the dealer-specific settings in force for Reg/OT/DT. Alternatively, you can simply enter the time worked in each of those buckets.

You can then "fill down" the values entered or calculated at the top into each person listed on the roster.

You can then make individual adjustments for specific people as needed. This typically includes filling in the name of each external person who showed up to the job when assigned as Supplemental Labor from a Service Provider.

You can enter an optional note for any roster member.

You must also select the Work Type performed – in some other systems this was known as Job Activity. You can do this at the top from a dropdown and fill it down into all, or you can adjust it for each resource. There is an ability to use more than one Work Type and split it – if for example a person worked 6 hours on Install and 2 hours on Moves.

**Adjusting the Roster**

If a person who was assigned does not show up, you can remove them from the Event. You can enter a note explaining why you did so, e.g. "ran out of gas on the way in". No time will be recorded for such a person.

If others who were not originally scheduled do show up, you can add them to the Event. There is a dropdown of defined resources you can select from.

**Photos**

The Lead can take photos of their work or anything else relevant to the job. These are general photos, and are outside and separate from specific photos tied to Punch Items. There is a Standard Work Requirement called "Work Order Photos" which allows the Order Team to indicate they want those on a particular job. These can then be used by Marketing or for other purposes.

**Signatures**

When completing an Event, or when sending a Status Update, you can obtain signatures from the Client and/or the Installer.

If a Client person is available to sign, we record their name, their email, and of course the image of their signature, along with the date/time.

If a Client person is available but does not want to sign, we record the same information except for the signature. In its place, we have a note explaining why they did not want to sign.

If there is no one available, the Lead can indicate that, with an optional note explaining why.

The Client can opt out of receiving the Status Update. It is checked by default. Any internal updates will be sent even if the Client opts out.

The Lead can also sign, and we record who they are, the date/time, etc. A setting determines if this is required. Dealers typically want it to be.

NOTE on signatures: some dealers (COR) have stated that they absolutely require a customer signature on file (for the purposes of audits, to show that the product has changed ownership.) They then need a dashboard or reminder to tell the Order Team which Work Orders were unable to obtain a signature. The Order Team then has to actually contact the customer and send them something to be signed, which they upload as a document. This was a new one for me.

**Recording Punch Items**

There is an interface for recording Punch Items from the field, which writes to our punch record, tied both to the Sales Order, and to the Work Order.

**Recording Unexpected Returning Product**

This is defined as product being brought to the Warehouse that was NOT part of the Scope. It is separate from Punch – where you might bring back a damaged product item on the Work order for repair. This is for unexpected product that the Client asks you to remove when there was no Line Item or Scope for doing so. This of course could be considered a Change Order, but the purpose of this feature is to be able to track such items, which tend to accumulate in the Warehouse over time, so that there can be a process for their disposition. This typically involves aging these items, so that we can see how long they have been open.

## Placeholder Work Orders

When creating a Work Order, you can click the Placeholder checkbox:

When this box is checked, there are fewer required things in order to Save. You don't need to:

- Add a Work Order Note
    
- Select/Add one or more Addresses
    
- Select/Add one or more Contacts
    
- For Events, select the Confirmation Type
    
- For Event Days, select the Schedule Type
    
- For Event Days, specify a specific time when Specific Time is selected in the Schedule Type
    

You still need to supply a name for the Work Order, and have one Event with one date. And you can fill in more details if you have them, you simply don't have to because it's a Placeholder.

When the Placeholder box is unchecked at some point when you want it to become a "real" Work Order, then the data that wasn't required as a Placeholder becomes required, in order to Save.

Placeholder Work Orders appear differently, in the Work Order Schedule

They also look differently in Scheduling:

## Hold List

The Hold List is a parking lot for Work Orders that we are not sure when they will be done. This can be because they are small and non-time-critical, or they might be larger jobs where we do not yet know when the Customer will be ready for them. They originally had a date or dates when first created, but once moved to the Hold List they are basically date-less.

First, we go to **Work Order Management**, as that is the place where we can remove Events from the Schedule and put them into the Hold List.

You can move individual Events to the Hold List, or entire Groups of Events.

For an individual Event, you click the "down arrow" action menu on the Event:

And then click "Move to Hold List"

You are then given these options:

You can choose to not Group the Event in the Hold List.

Or you can choose to put the Event into an existing Hold List Group (if you choose that option, you must select one from the dropdown.)

Or you can enter the name of a new group to create in the Hold List, and your Event will be put into that group after it is created.

You can also choose to retain any assigned resources – if you don't check that checkbox, they will be removed, and when the Event comes off the Hold List you will need to assign resources again. This often makes sense when you don't know how long the Event will be in the Hold List – as the original resources may not be available when it comes back off.

You can also retain any Scheduler Sticky Notes if you want.

If the Event has multiple days, all of them will be moved to the Hold List, with the exception of any that are Complete or Partially Complete.

Finally, you can enter a Hold List note - this is optional. If entered, it will appear in a column in the Hold List. This can include why you are putting this Event onto the Hold List, or to indicate when it might be rescheduled, or anything else you want to enter.

Moving an entire group of events to the Hold List works exactly the same way, except you get to it from the action menu on the Group Header:

**Once there are Events in the Hold List, you can open and view it.**

The Hold List is accessed from within Work Order Management by clicking the Hold List icon in the top left area:

The number next to it is how many Events are currently in Holdlisted status.

When opened, the Hold List initially looks like this:

Along the top toolbar, we have:

- ![image-20240521-194715.png](blob:https://suitecentric.atlassian.net/8cd0208e-2718-49e0-8fab-10411fa377bc) Select/Deselect All
    
- ![image-20240521-194732.png](blob:https://suitecentric.atlassian.net/9509e421-a002-4b1c-aff7-4b863329560c) Location Filter
    
- ![image-20240521-194753.png](blob:https://suitecentric.atlassian.net/9a3b9cd2-41d5-4e69-9045-e56fc0ac88ab) Expand or Collapse all sections (only enabled when the Events are arranged into sections, as opposed to the default flat list. Sections explained below.)
    
- ![image-20240521-194808.png](blob:https://suitecentric.atlassian.net/566d1d41-d263-4413-8d1d-b50b2a431676) Section up/down buttons (only enabled when the Events are arranged into sections, as opposed to the default flat list.)
    
- ![image-20240521-194824.png](blob:https://suitecentric.atlassian.net/4ed808ec-fa60-43b5-987a-b8fdac1dd43b) Section sort order (only enabled when the Events are arranged into sections, as opposed to the default flat list.)
    
- ![image-20240521-194842.png](blob:https://suitecentric.atlassian.net/9b375d36-e60e-468f-877e-3c2ba9bcd46f) Remove from Hold List and reschedule (enabled only when one or more Events are selected.)
    
- ![image-20240521-194854.png](blob:https://suitecentric.atlassian.net/bbb24434-ad87-45cc-82e3-5b651e40b3d5) Refresh – reloads the Hold List data using current filters.
    
- Arrange By:
    

You can arrange the Events by:

- None – the default flat list
    
- Work Order Group
    
- Sales Order
    
- Customer
    
- Work Order Type
    
- Event Type
    
- The Original Date (the date initially assigned to the Event, before it was moved to the Hold List)
    
- Receipt status: Full, Partial, None, NA
    
- Distance: distance from the Warehouse, in miles or km depending on your NetSuite setting
    
- Direction: The compass direction from the Warehouse.
    

When you Arrange the Events by one of these criteria, the Events in the list will be separated by headers that describe that section, and say how many Events it contains. For example, it looks like this when we arrange by Customer:

When you arrange by Original Date, it lists them by Week:

And arranged by distance, like this:

If you arrange the Events by their Work Order Group, the section headers have some additional controls to let you manage the Groups in the Hold List:

These Work Order Group controls are covered later.

  Next are the table columns:

All columns are sortable. When you have the results Arranged into sections, they sort within each section.

  **Cancelling Events on the Hold List:**

Within each Event's WO # column, there is an X icon – this is used to Cancel the Event. It asks if you are sure. All Days on that Event will be cancelled, unless they are Completed or Partially Completed. If this Event is the only Event on the Work Order, the Work Order itself will be cancelled as well.

  **Grouping Events on the Hold List:**

Within each Event's WO Group column, there are some buttons. If the Event is NOT currently in a Hold List Work Order Group, there is a plus sign button to add it to one:

Clicking the plus sign displays a dropdown of the Hold List Groups:

Clicking one of the Hold List Groups will put that Event into that Group.

.

When the Event IS in a Hold List Group, there are two buttons, one to Edit (put it in a different Group), and one to Remove it from its Group.

The Edit button displays the same dropdown of the Hold List Groups, so you can select a different one.

The Remove button removes this Event from its current Group/

**Adding, modifying, or removing Schedule Sticky Notes**

If when you put the Event into the Hold List, you chose to retain Stickies, they will appear in a column:

You can add new Scheduler Sticky notes with the plus sign. Clicking the plus sign, shows you the available Sticky colors:

Clicking one of those will put in your note, which you can then type into:

You can modify an existing Sticky simply by clicking it, and then typing.

To remove a Sticky completely from the Event, you just clear its text.

**Hold List Group management**

You can add, change, or remove a given Event's group membership in any view, but to manage the Hold List Groups themselves, you need to Arrange by WO Group:

When arranged by WO Group, you have additional buttons in each Group's header to manage the Groups themselves.

**New Hold List Group**

You can add a new Hold List Group by clicking the green plus sign button. This will insert a new group above the group whose "new" button you clicked.

You can then type to enter the actual name you want for the Group. There will not be any Events in it initially, of course.

**Delete a Hold List Group**

The X button on the group header will remove that Hold List Group. Any Events currently in that group will be moved to the "Ungrouped Events" section.

**Change the display order of the Hold List Groups**

The Scheduler typically wants frequently-used Hold List Groups to be near the top of the list by default. You can change the display order of the Groups by clicking the Up and Down arrow buttons in the Group header:

These move the group up or down.

**Scheduling a Hold List Event**

When it is time to remove an Event from the Hold List and schedule it for an actual date or dates, you first need to select the Event (or multiple Events)

**To select Events, you can:**

Click to select a single Event. It will turn yellow:

Clicking a different Event will de-select the first and select the new one. However, you can select multiple Event rows by using the **Ctrl/Command** key as you click. You can also use the **Shift** key to select a whole block of them. The Ctrl and Shift keys work just like they would with files in a folder.

You can also Arrange by any of the available options, and within the section's header, click the select button on the left. This will select all the Events in that section, and the button itself will turn yellow to indicate that all of its events are selected. Clicking the selection button again will de-select them all:

When you have one or more Events selected, you can Reschedule them off the Hold List and back to being "normal" Work Orders – which once again have date(s).

To do that, you click the Reschedule button in the top toolbar (this button is enabled only when one or more Events are selected):

That will open a popup with your Reschedule options:

All the Events you had selected will appear in a list. The list shows some of the original information from the Events.

**The first thing to do is select a new Date for the Event(s) – this is required:**

Once you have a new date, you can also select the Schedule Type and/or Specific Time – these are optional, if you don't enter anything they will retain their original values. If the dropdown is set to Specific Time, the Time field becomes required, otherwise it is disabled.

If any of your selected Events have multiple days, they will be scheduled for after the date you pick, using the same day difference they had before. You can override this by clicking to avoid Saturdays/Sundays/Holidays. These options only appear if the Event has multiple days.  (NOTE: Holidays are yet to be implemented)

You also have options about whether to put the rescheduled Events in Groups.

You can choose not to Group them at this point:

Or you can put them in one of the Work Order Groups which currently exist on your selected date – if there are any they will be listed in the dropdown (with 2023-12-25 selected in the date field):

If there are no Work Order Groups on the date you selected, this option is disabled:

Or you can enter a Group name and select to put in that Group – if it exists on the date selected, they will be put in it. If not, it will be created, and then they will be put into it:

If you choose this option, you must enter a name for the new Group to be created on the selected date.

Finally, you can also select if you want to have the Events be Unapproved, Approved, or Locked status, as well as which pane of Work Order Management they should land on.

When you have entered your date, and selected the other options to your liking or as required, you simply click the "Schedule" button:

The selected Event(s) will be removed from Hold List status, and will now appear on the Schedule and in Work Order Management on the date(s) selected.

## Technical Considerations

**Receiving and constituted lines.**

Before, all SO and PO lines were of course just normal transaction lines in Netsuite. I think moving the Receiving into Provia is a good opportunity to discuss if and when we plan to constitute them. From conversations, the idea has been expressed as "when all the Acks are in". But that is unfortunately not a single point in time. There will be POs cut early, which will be acknowledged and received sometimes far before other POs are even generated, let alone acked or received. And in many cases, there will be unacked lines on POs - some Vendors simply do not acknowledge, and dealers are not perfect at adding their own.

We could use at attempt to receive a PO as the time when we constitute its lines - and would not need to constitute ALL of the SO's lines at that time, only the lines on this PO. We would need some way to know that this has been done vs it needs to be done. We could just query the transaction lines and get a pretty quick answer. However, if we first have to create possibly hundreds of lines when the user saves their receipt info, and then immediately also create Item Receipts, it seems that would be very slow.

As noted earlier, we are already having to store some of the information around receiving in a separate record. What if we stored receipt information the same way? In our own record(s), with bin info. Or maybe even in JSON? Maybe even in our line item JSON - adding fields for received Qty, and an array of bin/qtys to a Bin field? Then in theory it would be fast and easy retrieve and display receiving information anywhere. And when they save a receipt, we could return and display the results from our record - but also initiate an asynchronous call to an endpoint to create the item receipts.

I'm not sure which way would be best - but it is something to discuss!

**"Fancy Notes"** - this should be part of a larger discussion about Notes & Files, and if we want our architecture to centralize and componentize these for use all over the place.

Previously I've done this with a free library that's been around forever, called TinyMCE. However - the most recent cloud version wants money after a certain number of uses. We could attempt to use the older version, which was totally free but consisted of a bunch of nested files and folders with code and assets. If we put all of them into the File Cabinet, it should work with relative paths.

But - we may want to use another tool, and maybe we have one already that we prefer. Besides basic formatting, font sizes, and colors, that ability to paste a snip or drag an image is the key functionality we want.

In the database, because a longtext field created by a suitelet is limited to 100,000 characters, I simply added 20-something such fields to the record, called note_1, note_2, etc. I could then store enough information to hold images, which in the note data are base-64 encoded data urls. This means they are just strings, and can be split up and stored in successive fields, and then easily concatenated for returning to the client. For performance reasons, I did not do this on the server while loading, but instead retrieved the note from the client after load using an endpoint.

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