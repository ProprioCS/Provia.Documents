- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Roles and Permissions](#Roles-and-Permissions)
- 7 [Features and Functionality](#Features-and-Functionality)
- 8 [Technical Considerations](#Technical-Considerations)
- 9 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 9.1 [Test Script Title](#Test-Script-Title)
    - 9.2 [Test Objectives](#Test-Objectives)
    - 9.3 [Test Environment](#Test-Environment)
    - 9.4 [Test Data](#Test-Data)
    - 9.5 [Test Steps](#Test-Steps)
    - 9.6 [Test Assertions](#Test-Assertions)
    - 9.7 [Test Metrics](#Test-Metrics)
    - 9.8 [Test Execution](#Test-Execution)

## Overview

The Provia SharePoint Sync is designed to streamline file management and enhance collaboration for contract furniture dealers. This solution bridges the gap between NetSuite and SharePoint, ensuring that critical documents are automatically synced and easily accessible within the appropriate NetSuite records. By integrating these systems, we improve efficiency in locating customer contracts, order-related files, and other essential documents. This integration maintains open communication channels across business units, allowing team members to work in their preferred platforms while keeping all information centralized and up-to-date.

## Solution Type

Module - extensive functionality including external integration

## User Stories

1. As a sales representative, I want to easily access customer-related documentation directly from their NetSuite record, so that I can quickly reference important information without switching between systems or searching through multiple folders.
    
2. As a warranty specialist, I want to view the original product documentation linked to a specific sales order in NetSuite, so that I can efficiently process warranty claims and provide accurate information to customers without delays.
    
3. As a project manager, I want any project-related files I upload to SharePoint to automatically sync with the corresponding NetSuite project record, so that I can ensure all team members have access to the latest documentation regardless of which system they're using.
    

## Success Metrics

1. Customer satisfaction: Gather feedback from clients on their experience with document accessibility and management after implementation.
    
2. User feedback: Collect qualitative feedback from internal teams on the ease of use and perceived time savings.
    

## Design

The Provia SharePoint Sync module will feature a tab in the NetSuite interface that exposes the folder structure of SharePoint. Users will be able to interact with files directly inside of SharePoint as well. The design ensures that users can navigate downstream in the file structure (into subfolders) but cannot navigate upstream (to parent folders).

## Roles and Permissions

All Provia user roles will have access to the SharePoint integration. Permissions will be based on existing SharePoint document-level permissions, not on NetSuite roles.

## Features and Functionality

1. Two-way synchronization between NetSuite and SharePoint
    
2. File access tab in NetSuite interface displaying SharePoint folder structure
    
3. Ability to view and interact with synced files directly in SharePoint
    
4. Downstream navigation in file structure (into subfolders), with restricted upstream access (to parent folders)
    
5. Automatic file association with relevant NetSuite records
    

## Technical Considerations

The primary technical consideration is to ensure that the integration does not violate or bypass SharePoint's permissions when accessed through NetSuite.

## Testing and Quality Assurance

## Test Script Title

Provia SharePoint Sync Test Script

## Test Objectives

1. Verify that the SharePoint integration respects existing SharePoint permissions when accessed through NetSuite.
    
2. Ensure accurate two-way synchronization between NetSuite and SharePoint.
    
3. Confirm that downstream navigation functions correctly while upstream navigation is properly restricted.
    

## Test Environment

SDN demo account

## Test Data

- PDF documents, images, Word documents, Excel workbooks
    
- Various folder structures created in SharePoint
    
- Files associated with appropriate folders in SharePoint based on the record they were stored in NetSuite
    

## Test Steps

1. Access the SharePoint integration tab in NetSuite
    
    - Expected result: SharePoint folder structure is visible within NetSuite interface
        
2. Upload various file types (PDF, image, Word, Excel) to different NetSuite records
    
    - Expected result: Files are successfully uploaded and visible in both NetSuite and the corresponding SharePoint folders
        
3. Navigate through the folder structure in NetSuite
    
    - Expected result: Able to navigate into subfolders (downstream) but not to parent folders (upstream)
        
4. Modify a file in SharePoint
    
    - Expected result: Changes are reflected in NetSuite after synchronization
        
5. Attempt to access a file in NetSuite that the user doesn't have permission for in SharePoint
    
    - Expected result: Access is denied, respecting SharePoint's existing permissions
        

## Test Assertions

1. The SharePoint folder structure is accurately represented in the NetSuite interface.
    
2. Files of all types (PDF, images, Word documents, Excel workbooks) sync correctly between NetSuite and SharePoint.
    
3. Users can navigate downstream in the folder structure but are prevented from navigating upstream.
    
4. File modifications in SharePoint are accurately reflected in NetSuite after synchronization.
    
5. SharePoint permissions are respected when accessing files through the NetSuite interface.
    

## Test Metrics

1. Synchronization accuracy: Percentage of files that are correctly synced between NetSuite and SharePoint without errors.
    
2. Permission enforcement rate: Percentage of attempts to access restricted content that are correctly blocked.
    

## Test Execution

1. Use a test script that covers all the test steps outlined.
    
2. Perform tests with different user accounts to ensure permissions are working correctly.
    
3. Document any errors or unexpected behaviors encountered during testing.
    
4. Verify each test assertion after completing the corresponding test steps.
    
5. Calculate the test metrics based on the results of multiple test runs.
    

Be the first to add a reaction