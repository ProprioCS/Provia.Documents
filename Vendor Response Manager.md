- 1 [Overview](#Overview)
- 2 [User Stories](#User-Stories)
- 3 [Success Metrics](#Success-Metrics)
- 4 [Design](#Design)
    - 4.1 [UI/UX Overview](#UI%2FUX-Overview)
        - 4.1.1 [1. Smart Table Implementation](#1.-Smart-Table-Implementation)
        - 4.1.2 [2. Visual Indicators](#2.-Visual-Indicators)
        - 4.1.3 [3. Layout Structure](#3.-Layout-Structure)
        - 4.1.4 [Field Mappings:](#Field-Mappings%3A)
        - 4.1.5 [Quote Tool Specific Columns:](#Quote-Tool-Specific-Columns%3A)
        - 4.1.6 [Line Statuses:](#Line-Statuses%3A)
        - 4.1.7 [Action Controls:](#Action-Controls%3A)
        - 4.1.8 [Global Tolerance Controls:](#Global-Tolerance-Controls%3A)
        - 4.1.9 [Views:](#Views%3A)
    - 4.2 [Supporting Documents](#Supporting-Documents)
- 5 [Roles and Permissions](#Roles-and-Permissions)
    - 5.1 [Primary Users (Full Access)](#Primary-Users-\(Full-Access\))
    - 5.2 [Secondary Users (View + Accept/Ignore)](#Secondary-Users-\(View-%2B-Accept%2FIgnore\))
    - 5.3 [Oversight Access (View Only)](#Oversight-Access-\(View-Only\))
- 6 [Features and Functionality](#Features-and-Functionality)
    - 6.1 [User Actions](#User-Actions)
    - 6.2 [Automations](#Automations)
    - 6.3 [System Behaviors](#System-Behaviors)
    - 6.4 [Considerations (from Cat)](#Considerations-\(from-Cat\))
- 7 [Technical Considerations](#Technical-Considerations)
    - 7.1 [Architecture](#Architecture)
    - 7.2 [Integration Points](#Integration-Points)
    - 7.3 [Constraints](#Constraints)
    - 7.4 [Dependencies](#Dependencies)
- 8 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 8.1 [Test Script Title](#Test-Script-Title)
    - 8.2 [Test Scenarios:](#Test-Scenarios%3A)
    - 8.3 [Validation Scenarios:](#Validation-Scenarios%3A)
    - 8.4 [Test Objectives](#Test-Objectives)
    - 8.5 [Test Environment](#Test-Environment)
    - 8.6 [Test Data Requirements](#Test-Data-Requirements)
    - 8.7 [Test Steps](#Test-Steps)
    - 8.8 [Test Assertions](#Test-Assertions)
    - 8.9 [Test Metrics](#Test-Metrics)
    - 8.10 [Test Execution](#Test-Execution)
        - 8.10.1 [Tools Required](#Tools-Required)
        - 8.10.2 [Testing Schedule](#Testing-Schedule)
    - 8.11 [Test Results Documentation](#Test-Results-Documentation)
    - 8.12 [Defect Reporting](#Defect-Reporting)
        - 8.12.1 [Severity Levels](#Severity-Levels)
    - 8.13 [Test Script Approval](#Test-Script-Approval)
        - 8.13.1 [Reviewers](#Reviewers)
        - 8.13.2 [Acceptance Criteria](#Acceptance-Criteria)
- 9 [Change Log](#Change-Log)

## Overview

The Vendor Response Utility (VRU) utility streamlines how contract furniture dealers handle electronic responses from various manufacturer systems, including quote tool validations, purchase order acknowledgments, and vendor communications. This utility addresses a critical pain point in the industry where dealers must manually compare and reconcile differences between their original transactions and manufacturer responses, particularly for pricing, specifications, and other key data points.

The solution implements a unified, intuitive interface that allows users to efficiently review changes, understand discrepancies through clear visual indicators, and take decisive actions (accept/ignore) on both individual and bulk levels. By incorporating a child-row display approach within the SmartTable framework, users can easily compare original versus received data while maintaining a comprehensive audit trail of all electronic communications.

The utility supports multiple transaction types including Quote Tool responses, PO Acknowledgments, and Vendor Bills, with each type having specific handling requirements and available actions. The interface provides clear visual distinctions between original and response data through consistent styling, and supports both individual and bulk actions for efficient processing.Solution Classification

- Primary purpose is to streamline electronic response handling for contract furniture dealers
    
- Focuses on quote tool validations and PO acknowledgments in V1, with vendor bill handling coming in a future release
    
- Clear workflow for handling
    
- tolerances, exceptions, and manual interventions
    
- Support for both individual and bulk actions
    

**Type:** Utility

## User Stories

1. "As a dealer user processing a quote tool response, I want to quickly identify pricing discrepancies and accept/ignore changes in bulk, while seeing additional validation info like restricted products, so I can efficiently validate and update multiple lines."
    
2. "As a purchasing agent reviewing a PO acknowledgment, I want to see both original and response data clearly displayed with highlighted changes, so I can make informed decisions about accepting or ignoring manufacturer modifications."
    
3. "As a sales team member, I want to understand why certain prices or specifications were rejected through clear reason codes, so I can take appropriate action to resolve discrepancies."
    
4. "As a purchasing agent handling vendor bills, I need distinct action options appropriate for billing responses, so I can properly handle discrepancies that can't simply be ignored."
    
5. "As a procurement manager, I want to bulk process multiple response lines with similar changes, so I can efficiently handle large orders with consistent modifications."
    
6. "As a dealer administrator, I want to see separate handling of Quote Tool versus PO acknowledgment issues, so I can properly track and manage different types of discrepancies."
    
7. "As a purchasing agent, I want to handle special case lines like C dot lines through an ignore status that maintains original values, so I can manage exceptions appropriately."
    
8. "As a dealer administrator, I want global tolerance settings that automatically accept minor variances, so I can focus only on material discrepancies."
    

## Success Metrics

1. Time Reduction
    
    - Measure: Average time to process manufacturer responses
        
    - Target: 50% reduction in processing time compared to manual methods
        
2. Error Prevention
    
    - Measure: Number of data entry errors/discrepancies
        
    - Target: 90% reduction in manual entry errors
        
3. Response Processing Efficiency
    
    - Measure: Percentage of responses processed using bulk accept/ignore
        
    - Target: 75% of qualifying responses processed in bulk
        
4. User Adoption
    
    - Measure: Percentage of users utilizing the utility vs. manual methods
        
    - Target: 95% adoption rate within 3 months
        
5. Response Resolution Rate
    
    - Measure: Time between receiving response and final accept/ignore decision
        
    - Target: 80% of responses resolved within 24 hours
        
6. Issue Resolution Tracking
    
    - Measure: Percentage of issues resolved within SLA
        
    - Target: 90% of issues resolved within defined timeframes by type
        
7. Auto-Processing Rate
    
    - Measure: Percentage of lines processed via tolerance auto-accept
        
    - Target: 50% of lines processed automatically
        

## Design

Figma Design: [https://www.figma.com/design/d7Q8e3UIQycq8n5VP2CDQ5/Acknowledgement?node-id=0-1&node-type=canvas&t=q2RqgKK1WvVfdNzS-0](https://www.figma.com/design/d7Q8e3UIQycq8n5VP2CDQ5/Acknowledgement?node-id=0-1&node-type=canvas&t=q2RqgKK1WvVfdNzS-0)

### UI/UX Overview

#### 1. Smart Table Implementation

- Main grid displaying transaction lines
    
- Child row expansion showing response data
    
- Visual distinction between original and response rows:
    
    - Original row: Regular text
        
    - Response row: Bold italic text
        
    - Field-level highlighting for discrepancies
        
- Accept/Ignore buttons at both line and bulk levels
    
- Transaction-specific action options
    
- Bulk action controls in header
    

#### 2. Visual Indicators

- Highlighting of changed fields
    
- Status indicators for accepted/ignored lines
    
- Clear display of reason codes and soft data
    
- Filter toggle between all lines vs. exceptions only
    
- Bold italic styling for response rows
    
- Field-level highlighting for specific differences
    

#### 3. Layout Structure

- Hierarchical view with collapsible sections
    
- Responsive design supporting horizontal scrolling
    
- Stacked data fields where appropriate to conserve space
    
- Bulk action controls prominently displayed
    
- Transaction-specific column configurations
    

#### Field Mappings:

- Budgeted cost/cell (initial sent values)
    
- Unit cost/cell (acknowledged/updated values)
    
- Acknowledged list/list
    
- Purchase discount/acknowledged purchase discount
    
- Quantity/acknowledged quantity
    

#### Quote Tool Specific Columns:

- Lead time (replaces ship date)
    
- Restricted product
    
- Pricing effective date
    
- Available for GSA
    
- Error messaging
    

#### Line Statuses:

- Accepted
    
- Ignored
    
- Pending
    
- Exception
    

#### Action Controls:

- Accept button: Updates unit cost/quantity fields with acknowledged values
    
- Ignore button: Updates line status only, maintains original values
    
- Create Issue button: Supports both bulk and per-line issue creation
    

#### Global Tolerance Controls:

- System preference level settings
    
- Cost variance settings
    
- Auto-acceptance for within-tolerance items
    
- No date tolerance settings
    

#### Views:

- All Responses
    
- Exceptions Only
    
- Within Tolerance
    

### Supporting Documents

- Detailed wireframes/mockups
    
- Style guide alignment with existing Provia UI
    
- Component interaction flowcharts
    
- Transaction-specific field mappings
    
- Response handling workflows by type
    

## Roles and Permissions

### Primary Users (Full Access)

- Provia - Sales
    
- Provia - Salesperson/Account Manager
    
- Provia - Purchasing
    
- Provia - Procurement
    
- Provia - Sales Support
    

### Secondary Users (View + Accept/Ignore)

- Provia - Sales Leadership
    
- Provia - Ops Manager
    
- Provia - Project Manager
    

### Oversight Access (View Only)

- Provia - Executive Leadership
    
- Provia - Controller/CFO
    
- Provia - Daily Administrator
    

## Features and Functionality

_In the future this solution could also be applied to vendor bills, but currently (as of 01/16/25) we can use NetSuite's default three-way bill processing to fill the same need._

### User Actions

- Toggle between all lines and exceptions only
    
- Expand/collapse child rows for response details
    
- Accept/Ignore behaviors:
    
    - Accept: Writes acknowledged values to unit cost/quantity fields
        
    - Ignore: Only updates line status, requires manual handling
        
    - Create Issue: Supports bulk or per-line creation
        
- Bulk accept/ignore selected lines
    
- Create issues (single or per-line)
    
- View response history
    
- Filter by response type
    
- Export comparison data
    
- Tolerance Processing:
    
    - Global system preferences for variances
        
    - Auto-acceptance of within-tolerance items
        
    - Record keeping of all deltas regardless of tolerance
        

### Automations

- Automatic detection and highlighting of changes
    
- Response data parsing and mapping
    
- Reason code categorization
    
- Status updates tracking
    
- Notification generation for new responses
    
- Audit trail creation
    
- Data validation checks
    
- Historical response tracking
    
- Transaction-type specific validation rules
    
- Bulk action processing
    
- Issue creation workflows
    
- Response status tracking
    
- Action audit logging
    

### System Behaviors

- Child row expansion on demand
    
- Real-time update of accept/ignore status
    
- Automatic field comparison
    
- Response Processing:
    
    - Auto-process within-tolerance items
        
    - Maintain audit history of all changes
        
    - Support PO finalization after acknowledgement
        
    - Enable auto-finalization for no-discrepancy POs
        
- Integration with manufacturer systems
    
- Soft data consolidation
    
- Transaction-type specific handling
    
- Dual issue creation workflows
    
- Status tracking for both response and action states
    
- Bulk operation processing
    
- Error Handling:
    
    - Surface quote tool validation errors
        
    - Handle invalid product IDs
        
    - Support C dot line processing
        
    - Manage rekey scenarios
        

### Considerations (from Cat)

Here is a great example of where 2020 has a different DESCRIPTION than what HM Quote Tool will return and we might not want to flag all those text differences as discrepancies - when the user really needs to pay attention to the pricing discrepancies

---

Another example - and please note Point 3 - while not a line discrepancy that we have a field for, this is a very important piece of the Quote Tool response to the user to be able to capture and display to make them aware that this is a Restricted Product.  Lead Time is also important "extra" info - I envision those things to be displayed in one column stacked on top of each other... they are all in the API response XML that Provia receives.  This would be a big enhancement over CORE (IMO).

## Technical Considerations

### Architecture

- Integration with SmartTable framework for child row implementation
    
- Custom record type for response tracking
    
- Real-time data comparison engine
    
- Response history storage mechanism
    
- Response type handling framework
    
- Action status tracking system
    
- Bulk operation processor
    
- Issue creation engine
    
- Field Mapping:
    
    - JSON storage for tracking original vs acknowledged values
        
    - Support for multiple snapshots (budgeted, acknowledged, billed)
        
    - Separation of display fields vs stored values
        
- Constituted Lines:
    
    - Process both accepted and ignored lines
        
    - Maintain original values for ignored lines
        
    - Support rekeyed line matching
        

### Integration Points

- Quote Tool:
    
    - Handle validation error responses
        
    - Process restricted product flags
        
    - Support effective date validations
        
    - Enable GSA status checks
        
- PO acknowledgment processing
    
- Vendor bill processing
    
- Issue management system
    
- Future vendor integration capability
    
- Document capture system readiness
    

### Constraints

- Must maintain performance with large data sets
    
- Handle multiple response versions
    
- Support concurrent user actions
    
- Manage horizontal scrolling efficiently
    
- Handle variable field mappings
    
- Support transaction-specific behaviors
    
- Handle dual issue creation workflows
    
- Maintain performance with bulk operations
    

### Dependencies

- SmartTable framework updates
    
- Manufacturer API specifications
    
- NetSuite record type limitations
    
- UI rendering capabilities
    
- Issue management system
    
- Response type handlers
    
- Action tracking system
    

## Testing and Quality Assurance

### Test Script Title

Vendor Response Utility (VRU) Utility Test Script

### Test Scenarios:

- Auto-tolerance processing
    
- Special case line handling (C dot, rekey)
    
- Error condition processing
    
- Validation message display
    

### Validation Scenarios:

- Out of tolerance responses
    
- Invalid product codes
    
- Restricted products
    
- Missing effective dates
    
- GSA validation failures
    

### Test Objectives

1. Validate accurate processing and display of manufacturer responses
    
2. Confirm proper functioning of accept/ignore actions
    
3. Verify data integrity across response history
    
4. Validate transaction-specific behaviors
    
5. Verify bulk operation processing
    
6. Test dual issue creation workflows
    

### Test Environment

- Primary: NetSuite Sandbox
    
- Secondary: Production with test data
    
- Integration test environment for manufacturer connections
    

### Test Data Requirements

1. Sample quote tool responses
    
2. PO acknowledgment data
    
3. Multiple response versions
    
4. Various exception scenarios
    
5. Different user role configurations
    

### Test Steps

1. **Response Receipt and Display**
    
    - Expected: Accurate parsing and display of response data
        
    - Validation: Child row expansion, field mapping, highlighting
        
2. **User Action Processing**
    
    - Expected: Proper handling of accept/ignore actions
        
    - Validation: Individual and bulk updates, status tracking
        
3. **Integration Verification**
    
    - Expected: Successful communication with manufacturer systems
        
    - Validation: Data synchronization, error handling
        
4. **Performance Testing**
    
    - Expected: System responsiveness under load
        
    - Validation: Multiple concurrent users, large data sets
        
5. **Security Testing**
    
    - Expected: Proper role-based access control
        
    - Validation: Permission enforcement, data protection
        

### Test Assertions

1. All response data is accurately captured and displayed
    
2. Accept/ignore actions correctly update transaction records
    
3. Child rows display proper formatting and data alignment
    
4. Performance remains stable with large data sets
    
5. User permissions are properly enforced
    

### Test Metrics

1. **Response Processing Time**
    
    - Target: < 3 seconds for individual responses
        
    - Target: < 10 seconds for bulk operations
        
2. **Data Accuracy Rate**
    
    - Target: 100% match between received and displayed data
        
3. **System Performance**
    
    - Target: Support 50+ concurrent users without degradation
        

### Test Execution

#### Tools Required

- NetSuite Test Environment
    
- Integration Testing Suite
    
- Performance Monitoring Tools
    

#### Testing Schedule

- Unit Testing: Development Team
    
- Integration Testing: QA Team
    
- User Acceptance Testing: Selected Dealer Users
    

### Test Results Documentation

- Detailed test logs
    
- Performance metrics
    
- User feedback documentation
    
- Issue tracking records
    

### Defect Reporting

#### Severity Levels

- Critical: Blocking core functionality
    
- High: Major feature impairment
    
- Medium: Non-critical function impact
    
- Low: Minor UI/UX issues
    

### Test Script Approval

#### Reviewers

- Development Team Lead
    
- QA Manager
    
- Business Analyst
    
- Client Representative
    

#### Acceptance Criteria

- All critical and high-priority tests passed
    
- Performance metrics met
    
- User acceptance confirmed
    

## Change Log

|   |   |   |   |   |
|---|---|---|---|---|
|**Version**|**Date**|**Author**|**Type**|**Description**|

|   |   |   |   |   |
|---|---|---|---|---|
|**Version**|**Date**|**Author**|**Type**|**Description**|
|1.1|2024-11-14|@John Dasharion|Changed|- Updated UI/UX approach: implemented bold italic styling for response rows and field-level highlighting for discrepancies [Watch @35:54](https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=2154.48 "https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=2154.48")<br>    <br>- Renamed field references from "acknowledgment data" to "response data" for consistency [Watch @25:11](https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1511.92 "https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1511.92")|
|1.1|2024-11-14|@John Dasharion|Added|- Extended transaction type support with specific handling for Quote Tool, PO Acknowledgment, and Vendor Bill responses [Watch @3:16](https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=196.58 "https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=196.58")<br>    <br>- Implemented dual issue creation workflows: bulk (single issue for multiple lines) and individual (per-line issues) [Watch @20:42](https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1242.1 "https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1242.1")<br>    <br>    - Enhanced status tracking to separate response status from action status (accept/ignore) [Watch @28:37](https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1717.14 "https://fathom.video/share/G2VpWJGkz2ohG4AWaK685mJmxxggBXyh?timestamp=1717.14")|
|1.2|2024-11-19|@John Dasharion|Added|Added Figma design link, and examples provided by Cat|
|1.3|2025-01-16|@John Dasharion|Changed / Added|- Updated field mappings for cost tracking<br>    <br>- Removed sell-related columns from acknowledgement view<br>    <br>- Added quote tool specific columns<br>    <br>- Clarified ignore vs accept behaviors<br>    <br>- Added global tolerance controls<br>    <br>- Updated line status definitions<br>    <br>- Added error handling specifications|

Be the first to add a reaction