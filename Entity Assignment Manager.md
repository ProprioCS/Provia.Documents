**Solution Design: Orion Entity Assignment Utility**

**Overview**  
The Orion Entity Assignment Utility is a custom NetSuite solution designed to streamline the process of assigning different record types, such as Influencers (Contacts or Vendors), Order Team Members (Employees), Sales Team Members (Employees), Competitors, and Contacts, to transactions and projects within the Orion software suite. This utility will provide contract furniture dealers with a user-friendly interface to efficiently manage and organize various individuals involved in different aspects of their business operations.

The primary purpose of the Orion Entity Assignment Utility is to enhance project management and improve collaboration among team members across different record types. By allowing users to assign specific roles to transactions and projects based on their record type, contract furniture dealers can ensure that the right individuals are involved at the appropriate stages of each process. This will lead to improved communication, increased efficiency, and better overall project outcomes.

**Solution Type**  
Utility

**User Stories**

1. As a Sales Manager, I want to assign a sales team to an opportunity or quote and subsequent transactions and project record so that I can ensure the right people are working on each potential sale throughout the entire process.
    
2. As a Resource Manager, I want to assign order team members to an opportunity or quote and subsequent transactions and project record so that I can effectively allocate resources and manage workload across the entire project lifecycle.
    
3. As a user in the system, I want to assign an existing contact to a transaction and subsequent transactions and project record so that I can maintain accurate records of customer interactions and involvement throughout the project.
    
4. As a user in the system, I want to create a new contact and assign it to a transaction and subsequent transactions and project record so that I can efficiently capture new customer information and associate it with the relevant transactions and project.
    
5. As a Sales Rep, I want to identify influencers on my opportunity or quote and subsequent transactions and project record so that I can track their effectiveness in helping me close deals and manage the relationship throughout the project.
    
6. As a Sales Rep, I want to assign competitors to an opportunity and subsequent transactions and project record so that I can track who I win and lose against throughout the sales process.
    
7. As a user in the system, I want to assign multiple people with the same role to a transaction and subsequent transactions and project record so that I can accurately represent all individuals involved in the process.
    

**Success Metrics**

1. Time Reduction: The Orion Entity Assignment Utility should reduce the time required to assign entities (Order Team Members, Sales Team Members, Influencers, Competitors, and Contacts) to transactions and projects.
    
2. Increased Visibility: The Orion Entity Assignment Utility should provide users with a clear overview of assigned entities across all relevant transactions and projects, increasing visibility into resource allocation and team involvement.
    
3. Intuitive Multiple Assignments: The utility should allow users to easily assign multiple people with the same role to a transaction and subsequent transactions and project record, with at least 90% of users reporting that the process is intuitive and straightforward.
    

**Design**  
The user interface for the Orion Entity Assignment Utility will be implemented using React and the Shadcn library, following the design provided in the Figma URL: [https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=1-1340&mode=design](https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=1-1340&mode=design)

The utility will be accessed through a custom user interface within NetSuite, providing a seamless and intuitive experience for users. It will integrate with relevant NetSuite records and transactions, such as employees, customers, vendors, and projects, allowing users to fetch and update data in real-time.

**Roles and Permissions**  
View Permissions (All roles can view assigned entities on transactions and projects):

- Orion – Executive leadership
    
- Orion – Marketing Specialist
    
- Orion - Sales Leadership
    
- Orion – Sales
    
- Orion - Salesperson/ Account Manager
    
- Orion - Sales
    
- Orion - Admin
    
- Orion - Sales Support
    
- Orion - Design Manager
    
- Orion - Designer
    
- Orion - Purchasing
    
- Orion - Procurement
    
- Orion - Ops Manager
    
- Orion - Project Manager
    
- Orion - Operations Admin/ Support
    
- Orion - Inventory Manager
    
- Orion - Warehouse Manager
    
- Orion - Accounting Manager
    
- Orion - Warehouse
    
- Orion - Controller/CFO
    
- Orion - A/P Analyst
    
- Orion - A/R Analyst
    
- Orion - Human Resources/ Payroll
    
- Orion - Employee Center
    
- Orion - Resource Manager
    
- Orion - Daily Administrator
    

Edit Permissions (Can add, remove, or modify entity assignments):

- Orion - Sales Leadership
    
- Orion – Sales
    
- Orion - Salesperson/ Account Manager
    
- Orion - Sales
    
- Orion - Admin
    
- Orion - Sales Support
    
- Orion - Ops Manager
    
- Orion - Project Manager
    
- Orion - Operations Admin/ Support
    
- Orion - Resource Manager
    
- Orion - Daily Administrator
    

All managers will have edit permissions, in addition to the sales and support roles specified above.

**Features and Functionality**

1. Order Team Assignment:
    
    - Filter: Employee (default), Vendor, Contact
        
    - Available Actions: Renotify, Start an Email, Start a Task, Start a Phone Call, Start Scheduling an Appointment, User Note
        
2. Sales Team Assignment:
    
    - Filter: None (employees only)
        
    - Available Actions: Renotify, Start an Email, Start a Task, Start a Phone Call, Start Scheduling an Appointment, User Note
        
3. Influencer Assignment:
    
    - Filter: Contact (default), Vendor, Customer
        
    - Available Actions: Renotify, Start an Email, Start a Task, Start a Phone Call, Start Scheduling an Appointment, User Note
        
4. Contact Assignment:
    
    - Filter: Contact or Vendor (based on the main line entity type)
        
        - If the main line entity is a customer or vendor, the corresponding filter will be selected by default
            
        - Users can uncheck the filter checkbox to search for any contact in the database
            
    - Available Actions: Renotify, Start an Email, Start a Task, Start a Phone Call, Start Scheduling an Appointment, User Note
        
5. Competitor Assignment:
    
    - Filter: None (competitors are their own entity type)
        
    - Available Actions: User Note
        

Common Features and Functionality:

- "Create new" option in the "Enter name" field drop-down for users with permission to create new entities
    
- Multi-select role field on the entity record, allowing supervisors to identify potential roles for each entity
    
- Only roles associated with the user are available in the "Role" column in the utility
    
- Comments section for users to enter free-form comments
    
- "Notify" checkbox to send a predefined email template to the entity upon assignment
    
- "Remove" button to remove the entity from the table
    
- Activity ellipsis (visible only if the entity is already attached) allows users to perform available actions
    
- Users can identify an entity by searching in the filterable "Name" field drop-down or using the search bar
    
- Once a role is identified, only entities associated with that role are visible in the "Name" field drop-down
    
- Table rows can be edited by clicking into the cell, making edits, and tabbing, entering, or clicking out of the cell
    

**Technical Considerations**  
2. Custom record and field creation:

- Create a configurable custom record for the Orion Entity Assignment Utility.
    
- Develop custom multi-select fields for the roles on the employee record for the Order Team assignment type.
    

3. React front-end using the Shadcn library:
    
    - Implement the user interface for the Orion Entity Assignment Utility using React and the Shadcn library, following the design provided in the Figma URL: [https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=1-1340&mode=design](https://www.figma.com/file/iQhEi7d7Q7ooMYwPC0HfdT/Smart-Table?type=design&node-id=1-1340&mode=design)
        
    - Ensure seamless integration between the React front-end and NetSuite's backend APIs.
        
4. Integration with existing NetSuite records and transactions:
    
    - Design the Orion Entity Assignment Utility to integrate with relevant NetSuite records and transactions, such as employees, customers, vendors, and projects.
        
    - Ensure that the utility can fetch and update data from these records and transactions in real-time.
        
5. Security and access control:
    
    - Implement robust security measures to protect sensitive data and prevent unauthorized access to the Orion Entity Assignment Utility.
        
    - Ensure that user roles and permissions are properly enforced based on the defined access levels.
        
    - Consider existing user permissions in NetSuite and ensure that the utility respects these permissions when granting access to features and data.
        
6. Error handling and logging:
    
    - Implement comprehensive error handling and logging mechanisms to facilitate debugging and troubleshooting.
        
    - Provide meaningful error messages to users and log detailed error information for developers.
        

**Testing and Quality Assurance**

- Test Script Title: Orion Entity Assignment Utility Test Script
    
- Test Objectives:
    
    1. Verify that users can successfully assign entities to transactions and projects based on their roles and permissions.
        
    2. Ensure that the utility integrates seamlessly with existing NetSuite records and transactions.
        
    3. Validate that the user interface is intuitive, responsive, and aligns with the provided design.
        
- Test Environment: Development Account
    
- Test Data: Prepare a comprehensive set of test cases covering various scenarios, including different entity types, roles, and permissions. Use realistic test data that closely resembles actual business cases.
    
- Test Steps:
    
    1. Log in to NetSuite with a user account having the appropriate permissions.
        
    2. Navigate to the Orion Entity Assignment Utility.
        
    3. Test each assignment type (Order Team, Sales Team, Influencer, Contact, Competitor) and verify that the expected filters, actions, and functionality are available.
        
    4. Assign entities to transactions and projects, and ensure that the assignments are accurately saved and reflected in the relevant records.
        
    5. Verify that the utility prevents unauthorized access and enforces role-based permissions correctly.
        
- Test Assertions:
    
    1. The Orion Entity Assignment Utility should allow authorized users to assign entities to transactions and projects successfully.
        
    2. The utility should integrate seamlessly with existing NetSuite records and transactions, fetching and updating data in real-time.
        
    3. The user interface should be intuitive, responsive, and aligned with the provided design.
        
    4. Role-based permissions should be strictly enforced, preventing unauthorized access and modifications.
        
    5. Error handling and logging mechanisms should be effective in capturing and reporting any issues or exceptions.
        
- Test Metrics:
    
    1. Percentage of test cases passed successfully.
        
    2. Average response time for entity assignments and data retrieval.
        
    3. User feedback on the intuitiveness and usability of the utility.
        
- Test Execution: Perform thorough testing of the Orion Entity Assignment Utility in both sandbox and production environments. Use manual testing techniques and automated testing tools, where applicable, to ensure comprehensive coverage.
    
- Test Results: Document the actual test results and compare them against the expected outcomes. Identify any discrepancies, bugs, or performance issues encountered during testing.
    
- Defect Reporting: Promptly report any defects or issues found during testing, prioritizing them based on severity and impact. Collaborate with the development team to track and resolve defects efficiently.
    
- Test Script Approval: Review and approve the test script with relevant stakeholders, including the project manager, development lead, and business analysts. Ensure that the test script adequately covers all critical aspects of the Orion Entity Assignment Utility.
    

Be the first to add a reaction