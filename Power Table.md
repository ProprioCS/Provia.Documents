- 1 [Overview](#Overview)
- 2 [Solution Type](#Solution-Type)
- 3 [User Stories](#User-Stories)
- 4 [Success Metrics](#Success-Metrics)
- 5 [Design](#Design)
- 6 [Features and Functionality](#Features-and-Functionality)
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

The smart table element is an advanced component designed to revolutionize data management within the Orion suite for contract furniture dealers. Developed as a separate interface on top of NetSuite, it utilizes generic items and JSON to ensure optimal performance, with finalized data written back to NetSuite.

Key features include a right-hand flyout panel for editing row fields, intuitive data sorting, filtering, and column management, flexible row selection and manipulation, advanced cell editing, grouping and subtotaling, customizable views, and seamless NetSuite integration.

The smart table element serves as a foundation for other Orion modules, enabling consistent data management experiences. It integrates with the BOM import tool, allowing users to import items from existing design software, streamlining data population and ensuring accuracy.

Benefits include enhanced data management capabilities, streamlined workflows, faster decision-making, and improved bottom line. The smart table element's robust structure facilitates integration and interoperability among Orion modules, providing a cohesive user experience.

## Solution Type

·       Modules – extensive functionality that may include external integrations, frameworks – big stuff

## User Stories

1. As a project manager, I want to use the Orion Smart Table to easily manage and update project data, including item quantities, prices, and descriptions, so that I can keep project information accurate and up-to-date, ensuring smooth project execution and client satisfaction.
    
2. As a designer, I want to import my design data from existing software into the Orion Smart Table using the BOM import tool, so that I can seamlessly populate the table with relevant information, reduce manual data entry, and maintain consistency between my design files and the Orion system.
    
3. As a sales representative, I want to leverage the Orion Smart Table's advanced filtering, sorting, and grouping capabilities to quickly identify and analyze key sales data, such as top-selling items, regional trends, and customer preferences, so that I can make data-driven decisions, target my sales efforts effectively, and ultimately increase revenue for the dealership.
    

## Success Metrics

1. Time Savings: Achieve a significant reduction in time spent on data management and analysis tasks, such as data entry, updating, and reporting, compared to the current processes.
    
2. Data Accuracy and Consistency: Maintain a high level of data accuracy, ensuring that the information within the Orion Smart Table is reliable, consistent, and free from errors.
    
3. Project Management Efficiency: Increase the efficiency of project management and execution, measured by factors such as faster project setup, easier tracking of project progress, and reduced communication gaps.
    
4. Sales Performance: Demonstrate a measurable improvement in sales performance, such as an increase in revenue or the number of successful deals closed, attributed to the insights and efficiencies gained through the Orion Smart Table.
    
5. Ease of Use: Achieve a high user satisfaction rate when surveyed about the ease of use and intuitiveness of the Orion Smart Table interface, including data entry, navigation, and overall user experience.
    
6. Availability of Necessary Functions: Ensure that all identified critical functions, such as data import, sorting, filtering, grouping, and editing, are fully implemented and operational within the Orion Smart Table module.
    
7. User Satisfaction: Maintain a high average user satisfaction score based on periodic surveys measuring overall satisfaction, perceived value, and likelihood to recommend the Orion Smart Table to colleagues and industry peers.
    

## Design

The Orion Smart Table will follow a user-centered design approach, focusing on creating an intuitive, efficient, and visually appealing interface for contract furniture dealers. The key design principles and considerations for the module include:

1. Layout and Navigation:
    
    - Clear and logical layout that promotes easy navigation and discoverability of features
        
    - Consistent placement of key elements, such as search, filters, and action buttons
        
    - Efficient use of screen real estate to maximize data visibility and minimize scrolling
        
2. Visual Design and Branding:
    
    - Clean, modern, and professional visual design that aligns with the Orion suite's branding guidelines
        
    - Consistent use of color, typography, and iconography to create a cohesive look and feel
        
    - Appropriate use of whitespace and visual hierarchy to guide users' attention and enhance readability
        
3. Responsive Design:
    
    - Flexible and adaptive layout that ensures optimal viewing and interaction across various devices and screen sizes
        
    - Prioritization of critical information and features on smaller screens
        
    - Smooth and efficient resizing and rearrangement of elements to maintain usability
        
4. Accessibility:
    
    - Adherence to web accessibility standards and best practices, such as WCAG 2.1
        
    - Proper use of semantic HTML, keyboard navigation, and screen reader compatibility
        
    - Sufficient color contrast and clear visual cues for interactive elements
        
5. Consistency with Orion Suite:
    
    - Consistent use of UI patterns, components, and interactions across the Orion suite
        
    - Seamless integration with other modules to provide a unified and familiar user experience
        
    - Adherence to Orion's design system and style guide to maintain visual and functional consistency
        

Supporting Documents:

1. Figma Mockup: [https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=0%3A1&mode=design&t=yLQZCSfsa4zRtFWl-1](https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=0%3A1&mode=design&t=yLQZCSfsa4zRtFWl-1)
    
    - This mockup provides a visual representation of the Orion Smart Table's user interface and key features.
        
2. Design Document: [https://suitecentric-my.sharepoint.com/:w:/g/personal/marcus_dallacqua_suitecentric_onmicrosoft_com/EYWgAeqsRqFKoo9mDMk34XgB6J-ldujws3ogmLCrbQEAXQ?e=ZvJaho](https://suitecentric-my.sharepoint.com/:w:/g/personal/marcus_dallacqua_suitecentric_onmicrosoft_com/EYWgAeqsRqFKoo9mDMk34XgB6J-ldujws3ogmLCrbQEAXQ?e=ZvJaho)
    
    - This document outlines the detailed design specifications, user flows, and interaction patterns for the Orion Smart Table.
        
3. Jira Project: [https://suitecentric.atlassian.net/jira/software/c/projects/C000046276/boards/200](https://suitecentric.atlassian.net/jira/software/c/projects/C000046276/boards/200)
    
    - The Jira project will be used to manage the development and implementation of the Orion Smart Table, track issues, and facilitate collaboration among team members.
        

## Features and Functionality

1. Left Hand Navigation
    
    1. There is a separate mockup for this in the same Figma file listed below
        
    2. This will contain all views available to a user in a given record type
        
    3. The Left Hand Nav is the control center of the smart table and can show a wide variety of information, most commonly, but not limited to Smart Table views.
        
    4. It will also contain user-generated views. Possible views are here:
        
    5. Transactions
        
    6. Time Entries
        
    7. Project
        
        1. Commissions
            
    8. Registers
        
        1. WIP Register
            
        2. IRNB Register
            
        3. Item Audit
            
        4. Cash Register
            
        5. Margin Erosion*Added later
            
    9. Issues
        
        1. Punch
            
        2. Ack Discrepancies
            
        3. Cost Verification Discrepancies
            
    10. Tasks - Across all transactions, showing trans#
        
        1. Editable
            
        2. Add New, assigns directly to project record
            
    11. Communications
        
        1. Emails
            
        2. Phone Calls
            
        3. User Notes
            
    12. Calendar view of events
        
    13. Files (across transactions)
        
    14. Reports (Summary Views)
        
    15. Transactions Totals
        
        1. Sales Orders
            
        2. Purchase Orders
            
        3. Vendor Bills
            
        4. Item Receipts
            
        5. Customer Invoices
            
        6. Adjustments
            
    16. Vendor Summary
        
    17. Budget vs Actual
        
    18. Order Team
        
2. Save/ Edit Button
    
    1. This was updated to be one button with 2 states - Save and Edit. It will follow the state of the actual Netsuite record
        
3. BOM Import Button
    
    1. Will launch the BOM Import Module
        
4. Export Function
    
    - Ability to export table data to various formats, including CSV, XML, SIF, PMX, and PDF
        
5. Create Button will be used to launch a number of functions including Draft PO, Finalize PO, Invoice, PDF Composer, Clone Transaction, Associated Transaction, and Request which will have an additional sub dropdown for Request Types
    
6. Column Management
    
    - Command Column: Frozen and located on the far right, with show/hide icons for printing purposes
        
    - Column Freezing: Ability to freeze columns to the left, keeping them visible while scrolling horizontally
        
        - Frozen columns will still be to the right of critical fields for a given view. It will always be right of the checkbox and line number. In the case of a sales order, for example, Product ID woudl also be in this set.
            
    - Sorting: Visible up/down arrows next to column labels for sorting data (temporary, doesn't change actual order)
        
    - Filtering: Advanced filtering functionality similar to AG Grid
        
    - Column Visibility: the dropdown will offer show/hide forcolumns
        
    - Add/Remove Columns: Ability to add or remove columns from the table
        
    - Resize Columns: Click and drag on column borders to resize
        
    - Move Columns: Click and drag column headers to reorder columns
        
7. Row Management
    
    - Row Selection: Single click, shift-click, and control-click for selecting rows
        
    - Select All/Deselect All: Functionality to select or deselect all rows (using the checkbox in the header
        
    - Row Detail: Icon on the far left to open a right pane displaying row data and allowing editing, saving, or deleting
        
    - Delete Row: Ability to delete rows with confirmation
        
    - Add Row: Ability to add new rows
        
    - Hover Highlight: Rows are highlighted when hovered over
        
8. Cell Editing
    
    - Text Entry: Double-click to edit text, single-click to select cell
        
    - Field Types: Support for various field types, including list/record (with dropdown), currency, integer, percent, and date
        
    - Validation: Validation rules defined for each cell/field type
        
    - Single Update: Double-click to edit, highlight text on second click, and highlight cell border in edit mode
        
    - Mass Update: Ability to update multiple cells across concurrent or non-concurrent rows
        
    - Cell Images: Support for image galleries, setting primary image, and copy-pasting images
        
9. Data Manipulation
    
    - Calculate Values: Automatic recalculation of affected cells when a value is changed
        
    - Reorder Lines: Ability to reorder rows
        
    - Add/Delete/Copy Lines: Functionality to add new lines (items or labor), delete lines, and copy lines
        
    - Subtotal Lines: Ability to add subtotal lines for list, sell, and cost
        
    - Group Lines: Functionality to group lines based on specific criteria
        
    - Indent/Outdent Lines: Ability to indent or outdent lines
        
10. User Interface
    
    - Infinite Scrolling: Top to bottom scrolling with bottom and top scroll bars
        
    - Table Themes: Support for light and dark modes, following system settings or user preferences (later version)
        
    - State Maintenance: Ability to save, load, and share table states
        
11. View Management (Left Nav)
    
    - Manage Views: Ability to save, load, and share views
        
    - Quick Views: Configuration record for creating quick views based on column groupings
        
12. Line Action bar
    
    1. Remains consistently available regardless of the right hand flyout state
        
    2. Includes all actions that can be done to a set of lines. Includes:
        
        1. Add Lines
            
        2. Delete Line(s)
            
        3. Copy Lines
            
        4. Reorder Lines
            
        5. Move to Top
            
        6. Move to Bottom
            
        7. Group Lines
            
        8. Indent Lines
            
        9. Outdent Lines
            
        10. Close Line
            
        11. Add Subtotal
            
        12. Clone Lines
            
        13. Split Lines (Includes Pop Up)
            
        14. Item Context (Right side Flyout menu)
            
13. Right Hand Flyout
    
    1. This bar can be shown or collapsed
        
    2. Regardless of the view a user in, the right hand bar will show all
        
    
    4. If one line is selected, it will be in Individual Edit mode
        
    5. If multiple lines are selected, it will indicate Bulk Edit
        
14. Footer: Grid summary element displaying rows visible, rows hidden, and total list, sell, and cost
    
    1. Selected Lines: Total list, sell, and cost for selected lines
        

## Technical Specifications

1. Front-end Framework
    
    - The Orion Smart Table will be built using a modern JavaScript framework such as React, Angular, or Vue.js
        
    - The chosen framework should provide a robust set of tools and libraries for building interactive and responsive user interfaces
        
    - The framework should also support efficient data rendering and management, especially for large datasets
        
2. Back-end Integration
    
    - The Orion Smart Table will integrate with the existing Orion back-end system, which is built on NetSuite
        
    - RESTful APIs will be used to facilitate communication between the front-end and back-end systems
        
    - Proper authentication and authorization mechanisms will be implemented to ensure secure data access and manipulation
        
3. Data Storage and Retrieval
    
    - The table data will be stored in a JSON format within the Orion system
        
    - Efficient data retrieval and caching mechanisms will be implemented to ensure optimal performance, even for large datasets
        
    - Pagination and lazy loading techniques will be employed to handle large amounts of data efficiently
        
4. Responsive Design and Cross-Browser Compatibility
    
    - The Orion Smart Table will be designed to be fully responsive and compatible with various screen sizes
        
    - The module will be thoroughly tested across different browsers and versions to ensure consistent performance and functionality
        
    - Proper fallback mechanisms and polyfills will be implemented to handle browser-specific issues and limitations
        
5. Accessibility and Usability
    
    - The Orion Smart Table will be developed with accessibility guidelines and best practices in mind
        
    - Keyboard navigation, screen reader compatibility, and proper ARIA attributes will be implemented to ensure accessibility for users with disabilities
        
    - User experience (UX) best practices will be followed to ensure intuitive and user-friendly interactions
        
6. Performance Optimization
    
    - The Orion Smart Table will be optimized for performance, ensuring fast rendering and smooth interactions
        
    - Techniques such as code splitting, lazy loading, and caching will be employed to minimize the initial load time and improve overall performance
        
    - Regular performance testing and profiling will be conducted to identify and address any performance bottlenecks
        
7. Security Considerations
    
    - Proper security measures will be implemented to protect sensitive data and prevent unauthorized access
        
    - Input validation, output encoding, and protection against common web vulnerabilities (e.g., XSS, CSRF) will be implemented
        
    - Secure communication protocols (e.g., HTTPS) will be used to encrypt data transmission between the front-end and back-end systems
        
8. Scalability and Extensibility
    
    - The Orion Smart Table will be designed with scalability and extensibility in mind
        
    - The module architecture will be modular and loosely coupled, allowing for easy addition of new features and functionalities
        
    - Proper abstraction layers and separation of concerns will be maintained to facilitate future enhancements and modifications
        
9. Documentation and Maintainability
    
    - Comprehensive documentation will be maintained throughout the development process, including code comments, API documentation, and user guides
        
    - Proper version control practices (e.g., Git) will be followed to track changes and facilitate collaboration among team members
        
    - Code review processes will be established to ensure code quality, consistency, and adherence to best practices
        

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

1. Test Script Title: Orion Smart Table Test Script
    
2. Test Objectives:
    
    - Verify the functionality, usability, and performance of the Orion Smart Table
        
    - Ensure the module integrates seamlessly with the existing Orion system
        
    - Validate the module's compliance with accessibility and security standards
        
3. Test Environment:
    
    - The testing will be conducted in a dedicated testing environment that mirrors the production environment
        
    - The testing environment will include the necessary hardware, software, and network configurations
        
    - The module will be tested on various browsers and devices to ensure compatibility and responsiveness
        
4. Test Data:
    
    - A comprehensive set of test data will be prepared, covering various scenarios and edge cases
        
    - The test data will include sample table data, user roles and permissions, and input values for different field types
        
    - The test data will be version-controlled and maintained separately from the production data
        
5. Test Steps:
    
    - The test steps will be documented in detail, covering each feature and functionality of the Orion Smart Table
        
    - The test steps will include both positive and negative test scenarios to ensure thorough coverage
        
    - The test steps will be reviewed and approved by the project stakeholders before test execution
        
6. Test Assertions:
    
    - The expected results for each test step will be clearly defined and documented
        
    - The test assertions will cover the expected behavior, data integrity, and user experience
        
    - The test assertions will be measurable and verifiable
        
7. Test Metrics:
    
    - The testing process will track key metrics such as test coverage, defect density, and test execution progress
        
    - The test metrics will be regularly reported and analyzed to identify trends and areas for improvement
        
    - The test metrics will be used to assess the overall quality and readiness of the Orion Smart Table
        
8. Test Execution:
    
    - The testing will be executed by a small team of solution architects who are familiar with the Orion system and the Smart Table module
        
    - The testing will be performed iteratively, focusing on the functionality, usability, and performance of the module
        
    - The solution architects will follow the approved test steps and test data during the testing process
        
9. Test Results:
    
    - The test results will be carefully documented, including the actual results, any deviations from the expected results, and observations
        
    - The test results will be categorized as pass, fail, or pending further investigation
        
    - The test results will be reviewed and analyzed to identify any defects, performance issues, or areas for improvement
        
10. Defect Reporting:
    
    - Any defects or issues identified during the testing process will be logged and tracked using a defect tracking system
        
    - The defects will be categorized based on their severity and impact on the module's functionality and usability
        
    - The defects will be assigned to the relevant development team members for investigation and resolution
        
11. Test Script Approval:
    
    - The test script, including the test objectives, test steps, test data, and test assertions, will be reviewed and approved by the project stakeholders
        
    - Any changes or updates to the test script will be properly versioned and communicated to the testing team
        
    - The test script approval process will ensure that the testing efforts align with the project goals and requirements
        

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