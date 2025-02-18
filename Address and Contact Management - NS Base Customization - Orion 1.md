- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
- 7 [Technical Specifications](#Technical-Specifications)
    - 7.1 [Object Definitions](#Object-Definitions)
        - 7.1.1 [Custom Fields and Records](#Custom-Fields-and-Records)
    - 7.2 [Scripts and Automations](#Scripts-and-Automations)
        - 7.2.1 [Rest Endpoints](#Rest-Endpoints)
            - 7.2.1.1 [Entities Endpoint:](#Entities-Endpoint%3A)
            - 7.2.1.2 [Addresses Endpoint:](#Addresses-Endpoint%3A)
            - 7.2.1.3 [Contacts Endpoint:](#Contacts-Endpoint%3A)
        - 7.2.2 [Scripts and Workflows:](#Scripts-and-Workflows%3A)
- 8 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 8.1 [Unit Tests](#Unit-Tests)
    - 8.2 [Process Tests](#Process-Tests)
- 9 [Time Estimate](#Time-Estimate)
- 10 [Changes And Revisions](#Changes-And-Revisions)

## Overview

The NetSuite customizations for the Address and Contact Management will focus on extending the platform's functionality to support the enhanced address and contact management features. The customizations will handle data storage, validation, and integration with existing NetSuite records and transactions.

## Solution Type

Customization

## User Stories

1. As a Sales Admin, I want to be able to easily select the appropriate Bill To, Installation, and Ship To addresses and contacts for each transaction, so that I can ensure accurate information is used throughout the order process. The custom fields and REST endpoints will allow me to efficiently manage and retrieve the necessary data.
    
2. As a Procurement Manager, I need the system to automatically generate Purchase Orders with the correct Ship To address and contact information based on the Sales Order data. The customizations to the PO generation process and the integration between Sales Orders and Purchase Orders will streamline my workflow and reduce errors.
    
3. As a Warehouse Manager, I require the ability to view and filter addresses based on their type (Bill To, Installation, Ship To) and tags (warehouse, COM, showroom, billing). The custom fields and REST endpoints will provide me with quick access to the relevant address information, helping me manage inventory and shipping processes more effectively.
    

## Success Metrics

## Design

We require a design for a filtered select box. @Chris Trumble to design the following:

Selectbox component with filtering capabilities should provide users with an intuitive and efficient way to select the desired option from a list of choices. The selectbox should offer default filtering based on the most common or relevant options, while also allowing users to easily change or expand the filters to access additional choices.

Key elements of a user-friendly selectbox with filtering include:

1. Default Filtering:
    
    - Apply default filters to the selectbox based on the context or most commonly used options.
        
    - Display the default filter as the initial selection in the selectbox.
        
2. Filter Expansion:
    
    - Allow users to click on the default filter to expand the selectbox and view all available options.
        
    - Provide clear visual cues (e.g., an arrow icon or "Expand" link) to indicate that users can access additional options by interacting with the default filter.
        
3. Search Functionality:
    
    - Implement a search box within the selectbox to enable users to quickly find specific options.
        
    - Display search results dynamically as the user types, filtering the available options based on the entered text.
        
4. Clear Selection:
    
    - Provide a clear way for users to remove the selected filter and return to the default or expanded view of the selectbox.
        
    - Include an "X" icon or a "Clear" button to allow users to easily deselect the current filter.
        

## Features and Functionality

1. Bulleted list
    
    1. Outlines automations
        
    2. Defines actions users can take
        

## Technical Specifications

## Object Definitions

### Custom Fields and Records

1. Address Custom Fields:
    
    - Create custom fields on the Address record to store additional information
        
    - Add fields for address type (Bill To, Installation, Ship To) and tags (warehouse, COM, showroom, billing)
        
    - Implement fields for storing latitude and longitude coordinates
        
2. Contact Custom Fields:
    
    - Create custom fields on the Contact record to store additional information
        
    - Add fields for contact type (Bill To, Installation, Ship To)
        
3. Transaction Custom Fields:
    
    - Add custom fields to the Sales Order and Purchase Order records
        
    - Include fields for Bill To, Installation, and Ship To addresses and contacts
        

## Scripts and Automations

### Rest Endpoints

#### Entities Endpoint:

1. Create a REST endpoint to retrieve a list of entities (customers, vendors, partners, employees)
    
    - Filtering should be based on entity type
        
    - Parameters
        
        - Entity type (required)
            

#### Addresses Endpoint:

1. Create a REST endpoint to retrieve a list of addresses associated with a selected entity
    
    - Filter addresses based on address type (Bill To, Installation, Ship To)
        
    - Parameters:
        
        - Entity Id (required)
            
        - Entity Type (required)
            
        - Address Type
            
    - Returns JSON Array of addresses
        

#### Contacts Endpoint:

1. Create a REST endpoint to retrieve a list of contacts associated with a selected entity
    
    - Use the entity endpoint filtered to contacts only
        

### Scripts and Workflows:

1. Address and Contact Validation:
    
    - Implement validation scripts to ensure data integrity and completeness
        
    - Validate address and contact information before saving to NetSuite records
        
2. Geocoding Integration:
    
    - Integrate with a geocoding service (e.g., Google Maps API) to populate latitude and longitude coordinates for addresses
        
    - Implement an asynchronous process to update coordinates without impacting user experience
        
3. Purchase Order Generation:
    
    - Modify the Purchase Order generation process to use the custom Ship To address and contact fields
        
    - Ensure the correct address and contact information is used when creating POs from Sales Orders
        
4. Shipping Routes and Fulfillment:
    
    - Create custom workflows to handle different shipping routes and fulfillment scenarios
        
    - Implement logic to determine if a PO should be a drop ship or special order based on the selected addresses
        
    - Update fulfillment and billing processes based on the shipping route and PO type
        

## Testing and Quality Assurance

## Unit Tests

This testing can be done using Postman. Each rest endpoint should be validated to correctly process valid calls and return no results/error message when invalid calls come in.

## Process Tests

A user will interact with NetSuite and the smart table to confirm addresses and contacts are sourced as expected.

The user will also confirm that POs are generated with the correct addresses.

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|Development|18|
|NetSuite Setup|4|
|QA|12|
|**Total**|**34**|

## Changes And Revisions

Be sure to Tag Dev (Luke) any time a new change is made. Format will be

1. Change 1
    
    1. Details
        
2. Change 2
    
    1. Details
        

Be the first to add a reaction