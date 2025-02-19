- 1 [Provia Pre-PO Utility](#Provia-Pre-PO-Utility)
- 2 [Technical Specifications](#Technical-Specifications)
    - 2.1 [Object Definitions](#Object-Definitions)
    - 2.2 [Data Design](#Data-Design)
    - 2.3 [Scripts and Automations](#Scripts-and-Automations)
- 3 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
    - 3.1 [Unit Tests](#Unit-Tests)
    - 3.2 [Process Tests](#Process-Tests)
- 4 [Time Estimate](#Time-Estimate)
- 5 [Changes And Revisions](#Changes-And-Revisions)

## **Provia Pre-PO Utility**

**Overview**  
The Provia Pre-PO Utility is a utility designed to streamline the purchase order creation and acknowledgment process for contract furniture dealers using Provia. This solution allows users to generate preliminary purchase orders (pre-POs) directly from the sales order smart table, with the ability to split POs based on various criteria such as vendors, ship addresses, requested ship date, tag 1, and contract numbers. The pre-PO data is stored in a custom record, and the corresponding transaction lines in the smart table are populated with the pre-PO and PO line numbers. Users can generate and manage PDF versions of the pre-POs using the PDF composer utility. Acknowledgments are handled within the sales order smart table, eliminating the need for a separate order adjustment solution. The system processes acknowledgments and stores the data in the smart table columns, with the potential to use AI for processing acknowledgment PDFs. Users can finalize the pre-PO, which generates the actual NetSuite PO and updates the sales order accordingly. This solution enhances efficiency, improves data accuracy, and provides a centralized, user-friendly interface for managing the PO process.

**Solution Title** Provia Pre-PO Utility

**Solution Type** Utility (part of the Provia Navigator tool)

**User Stories**

1. As a project coordinator, I want to easily generate pre-POs directly from the sales order smart table, so that I can efficiently manage the purchasing process for multiple orders. I should be able to split POs based on criteria like vendors, ship addresses, and contract numbers, ensuring that the right items are grouped together for each PO.
    
2. As a project coordinator, I need to quickly generate and manage PDF versions of the pre-POs using the PDF composer utility. The generated PDFs should be automatically saved to the corresponding preliminary PO record and be easily accessible through a quick view in the smart table. This will allow me to review and share the pre-POs with vendors and other team members effortlessly.
    
3. As a project coordinator's manager, I want my team to be able to process acknowledgments directly within the sales order smart table, eliminating the need for a separate order adjustment solution. The system should store the acknowledgment data in the smart table columns, highlighting any discrepancies between the PO and the acknowledgment. My team should be able to accept pricing changes within a certain tolerance or create discrepancy records for lines that need further resolution. This streamlined process will help us maintain data accuracy and quickly identify and resolve any issues.
    

**Success Metrics**

1. Time savings: Measure the reduction in time spent on generating and managing POs, processing acknowledgments, and updating smart table data compared to the previous process. This metric will demonstrate the efficiency gains achieved through the pre-PO functionality.
    
2. Accuracy improvement: Track the reduction in errors and discrepancies between POs, acknowledgments, and smart table data. This metric will highlight the improved accuracy and data integrity resulting from the streamlined pre-PO process.
    
3. User adoption: Monitor the percentage of project coordinators and their managers actively using the pre-PO functionality within Provia. High user adoption rates will indicate the solution's ease of use and effectiveness in addressing user needs.
    
4. Successful line constitution: Measure the percentage of pre-PO lines that are successfully constituted on the NetSuite native PO and the sales order. This metric will ensure that the pre-PO data is accurately reflected in the final documents.
    
5. Financial accuracy: Verify that the combination of constituted lines and summary lines results in the appropriate total on the sales order. This metric will confirm that the financial data remains accurate throughout the pre-PO process and is correctly reflected in NetSuite.
    

**Design** The pre-PO functionality will be seamlessly integrated into the Provia Navigator tool, providing a user-friendly and intuitive interface for managing preliminary purchase orders. The design philosophy focuses on simplicity, efficiency, and ease of use, ensuring that project coordinators and their managers can quickly generate, process, and update pre-POs within the sales order smart table.

Key screens and user interactions:

1. Sales order smart table: The pre-PO functionality will be accessible through the sales order smart table, allowing users to select lines and generate pre-POs directly from this interface.
    
2. Pre-PO generation popup: Upon selecting the relevant lines and clicking the "Generate Pre-PO" button, a popup window will appear, enabling users to split POs based on criteria such as vendors, ship addresses, and contract numbers.
    
3. PDF composer utility: Users will have access to the PDF composer utility, which allows them to generate and manage PDF versions of the pre-POs. The generated PDFs will be automatically saved to the corresponding preliminary PO record and be easily accessible through a quick view in the smart table.
    
4. Acknowledgment processing: The sales order smart table will include columns for acknowledgment data, allowing users to process acknowledgments directly within this interface. Discrepancies between the PO and acknowledgment will be highlighted, and users can accept pricing changes within a specified tolerance or create discrepancy records for lines that require further resolution.
    
5. Line constitution: Once the pre-PO process is complete, users can finalize the pre-PO, which will constitute the lines on the NetSuite native PO and update the sales order accordingly.
    

UI screens: Chris Trumble, a member of the Provia team, is currently creating detailed UI screens for the pre-PO functionality. These screens will serve as a visual reference for the development team, ensuring that the final implementation aligns with the intended design and user experience. The UI screens will be linked to this design section once they are complete.

**Roles and Permissions**

1. Provia - Admin (Edit): As the main administrators of the Provia system, this role should have full edit access to the pre-PO functionality to manage and support the utility.
    
2. Provia - Sales Support (Edit): Sales Support users will need edit access to generate pre-POs, process acknowledgments, and update smart table data to assist the sales team effectively.
    
3. Provia - Purchasing (Edit): Purchasing users will require edit access to the pre-PO functionality to generate and manage POs, process acknowledgments, and update smart table data as part of their core responsibilities.
    
4. Provia - Procurement (Edit): Similar to Purchasing, Procurement users will need edit access to the pre-PO utility to fulfill their roles in managing POs and related tasks.
    
5. Provia - Ops Manager (View): Operations Managers should have view access to the pre-PO functionality to oversee the purchasing process and monitor performance without needing to make edits.
    
6. Provia - Project Manager (Edit): Project Managers will need edit access to generate pre-POs, process acknowledgments, and update smart table data for their specific projects.
    
7. Provia - Operations Admin/ Support (Edit): Operations Admin and Support users will require edit access to assist with pre-PO tasks and provide support to other users.
    
8. Provia - Controller/CFO (View): Controllers and CFOs should have view access to the pre-PO functionality to monitor financial data and ensure accuracy without needing to make edits.
    
9. Provia - A/P Analyst (View): Accounts Payable Analysts will need view access to the pre-PO data to reconcile invoices and process payments.
    

All other Provia user roles not mentioned above will have view access to the pre-PO functionality by default, allowing them to access relevant information without the ability to make edits.

**Features and Functionality**

- User-friendly interface integrated into the Provia Navigator tool
    
- Ability to select lines from the sales order smart table and generate pre-POs
    
- Custom UI for generating pre-POs and splitting them based on criteria such as vendors, ship addresses, contract numbers, and one more factor (not specified in the transcript)
    
- Creation of a custom record called "preliminary purchase order" with a PO number generated using a custom record
    
- Population of transaction lines in the smart table with the appropriate pre-PO number and a PO line number, with the line number in sequential order based on the line number of that item in the sales order smart table
    
- PDF composer utility to generate PDFs of pre-POs, with the ability to save the PDFs to the customer preliminary PO record and view them in a quick view in the smart table
    
- Handling of acknowledgments in the sales order smart table, eliminating the need for a separate order adjustment solution
    
- Processing of acknowledgments by saving data from the acknowledgment into columns in the sales order smart table
    
- Potential AI-based processing of acknowledgment PDFs by allowing users to drag and drop the PDF into a widget on the SO, convert it to JSON, and view it in the smart table
    
- Comparison view in the smart table to display line data with PO info and acknowledgment line data directly below it, highlighting cells with discrepancies
    
- Ability for users to accept pricing changes within a certain tolerance or create discrepancy records for lines that need resolution, with discrepancies available in a quick view in the smart table
    
- Additional views in the smart table to view POs and lines on an individual PO, allowing users to verify that lines have been sufficiently acknowledged
    
- Finalization of the PO by the user once lines have been sufficiently acknowledged, generating the actual NetSuite PO based on the reserved PO number and constituting the lines on the sales order and PO item sublists
    
- Automatic adjustment of summary lines on the sales order to ensure accurate total cost and sell amounts
    
- Creation of a JSON file for the finalized PO to enable smart table display, even though the NetSuite line items exist on the PO
    
- Synchronization of changes made to the smart table or the NetSuite transaction lines going forward
    

**Technical Considerations**

1. Integration with the Provia Navigator tool and sales order smart table
    
2. Custom record creation for preliminary purchase orders and PO number generation
    
3. Handling of large data volumes and ensuring optimal performance
    
4. Integration with OpenAI for processing acknowledgment PDFs and emails, converting them to JSON, and displaying the data in the smart table for comparison with pre-PO data
    

**Testing and Quality Assurance**

_Test Script Title_ "Provia Pre-PO Utility Test Script"

_Test Objectives_

1. Verify that users can generate pre-POs, process acknowledgments, update smart table data, and constitute lines accurately and efficiently.
    
2. Ensure that the pre-PO functionality is seamlessly integrated with the Provia Navigator tool and provides a user-friendly experience.
    
3. Validate that the AI-based acknowledgment processing accurately converts PDFs and emails to JSON and displays the data correctly in the smart table for comparison.
    

_Test Environment_

- Testing will be conducted in both the NetSuite Sandbox and Production environments.
    

_Test Data_

- A comprehensive set of test cases will be created, covering various scenarios such as generating pre-POs with different criteria, processing acknowledgments with discrepancies, and constituting lines.
    
- Test data will include sample sales orders, vendor information, acknowledgment PDFs, and emails.
    

_Test Steps_

1. Generate pre-POs from the sales order smart table using different splitting criteria and verify that the custom records are created accurately.
    
2. Process acknowledgments by uploading PDFs and emails, and ensure that the data is correctly converted to JSON and displayed in the smart table.
    
3. Update smart table data based on acknowledgment discrepancies and validate that the changes are reflected accurately in the pre-PO records.
    
4. Finalize the pre-PO by constituting lines and verify that the NetSuite native PO and sales order are updated correctly.
    
5. Verify that the summary lines on the sales order are adjusted accurately to reflect the total cost and sell amounts.
    

_Test Assertions_

1. The pre-PO number and PO line numbers are generated correctly and assigned to the corresponding transaction lines in the smart table.
    
2. Acknowledgment data is accurately captured and displayed in the smart table, highlighting any discrepancies between the pre-PO and the acknowledgment.
    
3. Users can accept pricing changes within the specified tolerance or create discrepancy records for lines that require further resolution.
    
4. The finalized PO and sales order contain the correct constituted lines and summary lines, with accurate total amounts.
    
5. Changes made to the smart table or NetSuite transaction lines are synchronized correctly.
    

_Test Metrics_

1. Percentage of test cases passed successfully.
    
2. Time taken to generate pre-POs, process acknowledgments, and constitute lines compared to the previous process.
    
3. User satisfaction rating for the ease of use and functionality of the pre-PO utility.
    

_Test Execution_

- Testing will be performed by the QA team using manual and automated testing tools.
    
- Detailed test cases will be executed, and results will be recorded in the test Utility.
    

_Test Results_

- Actual results will be compared against expected results for each test case.
    
- Any discrepancies or issues will be logged and investigated.
    

_Defect Reporting_

- Defects will be reported using the standard defect tracking system.
    
- Severity levels will be assigned based on the impact of the defect on the functionality and usability of the pre-PO utility.
    

_Test Script Approval_

- The test script will be reviewed and approved by the project manager, development lead, and key stakeholders.
    
- Acceptance criteria will be based on the successful execution of all test cases and the resolution of any critical or high-severity defects.
    

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