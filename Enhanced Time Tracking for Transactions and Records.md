- 1 [Overview](#Overview)
    - 1.1 [Solution Title](#Solution-Title)
    - 1.2 [Solution Type](#Solution-Type)
    - 1.3 [User Stories](#User-Stories)
    - 1.4 [Success Metrics](#Success-Metrics)
    - 1.5 [Design](#Design)
    - 1.6 [Roles and Permissions](#Roles-and-Permissions)
    - 1.7 [Technical Considerations](#Technical-Considerations)
    - 1.8 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
- 2 [Technical Specifications](#Technical-Specifications)
    - 2.1 [Object Definitions](#Object-Definitions)
    - 2.2 [Data Design](#Data-Design)
    - 2.3 [Scripts and Automations](#Scripts-and-Automations)
- 3 [Testing and Quality Assurance](#Testing-and-Quality-Assurance.1)
    - 3.1 [Unit Tests](#Unit-Tests)
    - 3.2 [Process Tests](#Process-Tests)
- 4 [Time Estimate](#Time-Estimate)
- 5 [Changes And Revisions](#Changes-And-Revisions)

## Overview

The Time Tracking on Transactions and Other Record Types solution is a customization designed to extend NetSuite's native time tracking capabilities. Typically, time tracking in NetSuite is done on CRM tasks. This solution enables time tracking directly on transactions and other record types such as opportunities, quotes, and sales orders. By adding a custom field to the time tracking record that links it to these additional record types, contract furniture dealers can streamline their time tracking processes, avoiding the need to create tasks solely for time tracking purposes.

Another key benefit is that this solution allows all time tracking information to roll up to the project record. This enables furniture dealers to associate time tracking with employees, calculate rates and costs for various activities, and include this data in the project's overall gross profit calculation. During implementation, it will be important to determine how the dealer currently calculates costs, particularly if payroll is not managed within NetSuite. A blended rate field on the employee record may be used to address this need.

### Solution Title

**Enhanced Time Tracking for Transactions and Records**

### Solution Type

**Customization**

### User Stories

1. **Designer**
    
    - As a designer, I want to track time against the request for design record. I need the ability to log my hours directly on this record to ensure accurate tracking of my work.
        
2. **Installer**
    
    - As an installer, I need the ability to track time against the work order. This helps in accurately recording the time spent on installations and ensures that the project timeline and costs are properly managed.
        
3. **Project Manager**
    
    - As a project manager, I need the ability to track time against a quote. This allows me to monitor the time spent on quoting activities and roll up this information into the overall project record.
        
4. **Manager**
    
    - As a manager, I need the ability to track time against a quote to oversee the time allocation and ensure that all time tracking data is accurately rolled up into the project's gross profit calculation.
        

### Success Metrics

1. **Transaction and Record Type Time Tracking**
    
    - Users can track time against various transactions and record types, such as requests for design, work orders, and quotes.
        
2. **Accurate Job Costing**
    
    - The appropriate costs are allocated to jobs, and this impacts the gross profit calculations accurately, reflecting the true cost of the projects.
        
3. **Gross Profit Calculation**
    
    - Time tracking data accurately contributes to the project's overall gross profit calculation, ensuring comprehensive financial reporting.
        
4. **Opportunity Time Tracking**
    
    - Users, including sales reps and other employees, can track time against opportunities, providing insights into the labor and costs involved in trying to land deals, even if the deals are not won.
        
5. **Commission Calculations**
    
    - Commissions are calculated properly based on an accurate gross profit, which includes the cost of labor tracked by employees against the project. This ensures fair and accurate compensation, potentially decreasing the commissionable amount to the salesperson.
        

### Design

This solution is a straightforward customization with no additional design considerations beyond the outlined customizations.

### Roles and Permissions

**Track Time Permissions:**

- Marketing Specialist
    
- Sales Leadership
    
- Sales
    
- Salesperson/Account Manager
    
- Admin
    
- Sales Support
    
- Design Manager
    
- Designer
    
- Ops Manager
    
- Project Manager
    
- Operations Admin/Support
    
- Resource Manager
    

**View Time Permissions:**

- Executive Leadership
    
- Purchasing
    
- Procurement
    
- Inventory Manager
    
- Warehouse Manager
    
- Accounting Manager
    
- Warehouse
    
- Controller/CFO
    
- A/P Analyst
    
- A/R Analyst
    
- Human Resources/Payroll
    
- Employee Center
    
- Daily Administrator
    

**Special Permissions:**

- **Approved Time Management**: Once time is approved, it cannot be changed. This existing functionality may require verification or customization to ensure compliance.
    

### Technical Considerations

- **Implementation Method**: This customization will be implemented using point-and-click customizations in the NetSuite UI. No developer involvement is required.
    
- **Resources Required**: A technical functional consultant will handle the implementation.
    
- **Approval Workflow**: Ensure that once time is approved, it cannot be changed, using existing NetSuite functionality or minor adjustments as needed.
    

### Testing and Quality Assurance

**Test Script Title**

Time Tracking Solution Test Script

**Test Objectives**

1. Verify that users can create time records directly from transactions and other record types.
    
2. Confirm that the rate and cost flow correctly to the project record.
    
3. Ensure that the actual time entries are used appropriately for the project's gross profit calculation, pending confirmation with Catherine.
    

**Test Environment**

- SuiteCentric Dev Environment
    

**Test Data**

- Create test transactions (e.g., requests for design, work orders, quotes).
    
- Set up employee records with applicable rates.
    

**Test Steps**

1. **Create Time Record from Transaction**
    
    - Navigate to a transaction or appropriate record type (e.g., request for design, work order, quote).
        
    - Create a time record from that record type.
        
    - Confirm that the time record is created successfully.
        
2. **Verify Rate and Cost Flow to Project**
    
    - Check the project record to ensure the rate and cost from the time record flow correctly to the project.
        
    - Verify that the project's gross profit calculation includes the time-tracked costs.
        
3. **Budget vs. Actual Reporting**
    
    - Confirm with Catherine how the budget and actual reporting should be handled.
        
    - Verify that the actual time tracking entries are used for actualized costs and that forecasted selling costs are used for budgeted costs on the project record.
        

**Test Assertions**

1. Time records can be created directly from transactions and other record types.
    
2. Rate and cost from time records flow correctly to the project record.
    
3. Actual time-tracked costs are reflected in the project's gross profit calculation as confirmed by Catherine.
    

**Test Metrics**

1. **Accuracy of Time Tracking**
    
    - Confirm that time records are correctly linked to transactions and record types.
        
2. **Cost Allocation**
    
    - Ensure that costs are correctly allocated to the project and reflected in the gross profit calculation.
        
3. **Reporting Accuracy**
    
    - Verify the accuracy of budget vs. actual reporting on the project record.
        

**Test Execution**

- Follow the test steps outlined above in the SuiteCentric Dev Environment.
    
- Use appropriate tools to document the test results and any issues encountered.
    

**Test Results**

- Document actual results and compare them to the expected results.
    
- Note any discrepancies or defects.
    

**Defect Reporting**

- Report any defects found during testing, including severity levels and steps to reproduce.
    

**Test Script Approval**

- Reviewers: Project Manager, Ops Manager, Sales Leadership
    
- Acceptance Criteria: All test assertions must pass without any critical defects.
    

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