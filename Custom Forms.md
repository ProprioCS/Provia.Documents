- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
- 7 [Technical Considerations](#Technical-Considerations)
    - 7.1 [Object Definitions](#Object-Definitions)
    - 7.2 [Data Design](#Data-Design)
    - 7.3 [Scripts and Automations](#Scripts-and-Automations)
- 8 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 8.1 [Unit Tests](#Unit-Tests)
    - 8.2 [Process Tests](#Process-Tests)
- 9 [Time Estimate](#Time-Estimate)
- 10 [Changes And Revisions](#Changes-And-Revisions)

## Overview

The Orion Custom Record Forms for Furniture Dealers is a comprehensive set of record forms tailored specifically for furniture dealers, designed to streamline and optimize their workflow within the Orion software. These custom forms include all the necessary custom fields relevant to the furniture industry while eliminating NetSuite's default fields that do not apply to this sector. By providing a clean, focused, and industry-specific interface, these forms greatly enhance usability and efficiency. The Custom Forms serve as a starting point for each furniture dealer, with further personalization options available during their individual implementation process. This approach ensures that the forms align perfectly with each dealer's unique business processes and requirements, resulting in a highly customized and efficient user experience within the Orion software.

## Solution Type

·       Customizations – standard netsuite customization including point and click and simple scripts

## User Stories

1. As a project coordinator, I need a consistent and logically organized layout of custom fields across various record types, so that I can efficiently input the necessary data when working on a quote.
    
2. As a sales representative, I want the custom opportunity form to clearly indicate mandatory fields, ensuring that I provide all the required information when completing the form.
    
3. As a sales leader, I require the custom forms to have industry-specific field names that align with the furniture sector's terminology, enabling my team to work more effectively within the Orion software.
    

## Success Metrics

1. Consistency: Custom fields are placed in the same location across different record types, ensuring a consistent user experience.
    
2. Usability: Users report that the custom forms are easy to understand and use, with minimal searching required to find relevant or mandatory fields.
    
3. Efficiency: Users experience a significant reduction in time spent entering data compared to using standard NetSuite forms.
    
4. Data Completeness: Records have all mandatory fields filled out correctly.
    
5. Industry Alignment: Users agree that the field names and groupings are intuitive and aligned with furniture industry terminology.
    

## Design

The Orion Custom Record Forms for Furniture Dealers will use NetSuite's default form layout, so there are no specific UI/UX considerations or supporting documents needed.

## Features and Functionality

1. Field group names are inteligent, intuitive and appropriate for furniture dealers
    
2. Custom fields are created and organized in a logical manner on each record type, ensuring a consistent user experience
    
3. Field names are aligned with furniture industry terminology, making it easy for users to understand and navigate the forms
    
4. During implementation, dealers can:
    
    - Determine which fields are mandatory based on their specific requirements
        
    - Clearly mark these fields as mandatory on the custom forms to ensure users provide all the required information
        
    - Rename fields to better match their internal terminology or processes
        
5. User actions:
    
    - Users can easily navigate through the forms and input data in the appropriate fields
        
    - Users can save partially completed forms and return to them later
        
    - Upon submission, the system checks for mandatory fields (as designated by the client) and alerts users if any required information is missing
        
6. The system administrator has the ability to edit and customize the forms as needed, ensuring the forms continue to meet the dealer's evolving requirements
    

## Technical Considerations

- Do not need a dev for this work but a functional consultant - at least for the first part and then we need a dev to create the bundle
    
- Will this be an account customization or a suiteapp?
    
- The custom fields must be created before the forms are altered to ensure that the necessary fields are available for inclusion on the custom forms.
    
- The custom forms should be bundled and installed as a separate solution, but they are contingent on the custom field creation.
    
- The installation process should include a check to verify that the required custom fields are present before proceeding with the form customization.
    
- The solution architect team will review the initial layouts and make any necessary changes before finalizing the custom forms
    

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

- Test Objectives:
    
    1. Verify that all custom fields are correctly placed and functioning as intended on each custom record form.
        
    2. Ensure that the custom forms are user-friendly, easy to navigate, and align with the furniture industry terminology.
        
    3. Confirm that mandatory fields (as designated by the client) are properly marked and validated upon form submission.
        
- Note: The test objectives will be completed by the solution design team before the custom forms solution is installed. The custom fields need to be created before the custom form solution is installed.
    

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