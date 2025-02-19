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
    - 8.3 [Scripts and Automations](#Scripts-and-Automations)
- 9 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
- 10 [Time Estimate](#Time-Estimate)
- 11 [Changes And Revisions](#Changes-And-Revisions)

## Overview

The Roles and Permissions component of Provia is designed to streamline and standardize user access management across the MillerKnoll Dealer network within NetSuite. By implementing a set of pre-defined user roles, each with specific permissions tailored to their job responsibilities, this solution ensures that users have access to the necessary functionality and data while maintaining appropriate security and control.

The main purpose of this component is to provide a default set of roles that can be configured during a dealer implementation if needed.

Key benefits for contract furniture dealers include:

1. Improved efficiency in user access management
    
2. Enhanced data security and compliance
    
3. Reduced administrative overhead
    
4. Streamlined onboarding and training processes
    
5. Better alignment between job responsibilities and system access
    

## Solution Type

·       Configurations  -NetSuite features to be enabled, configured or installed

## User Stories

- As a Dealership Administrator, I want to quickly assign pre-defined user roles to new employees so that they have access to the necessary functionality and data based on their job responsibilities.
    
- As a Sales Manager, I want to ensure that my team members have access to customer data and sales tools while restricting access to sensitive financial information.
    
- As a Project Manager, I want to have permissions that allow me to manage order acknowledgments, add cost lines, and generate delivery tickets and work orders.
    

## Success Metrics

- Reduction in time spent on user access management tasks
    
- Increased user satisfaction with role-based access and permissions
    
- Decreased number of access-related security incidents
    
- Improved audit results for user access controls
    
- Faster onboarding of new employees
    

## Design

The Roles and Permissions component will leverage NetSuite's native user role and permission management capabilities. Each of the pre-defined user roles will be created within NetSuite, with specific permissions assigned based on the job responsibilities outlined in the requirements document. The user interface for managing roles and permissions will be the standard NetSuite interface, ensuring familiarity and ease of use for administrators.

## ==Features and Functionality==

1. Administrator – System Administrator responsible for upkeep of system (Suite Centric and Dealership IT)
    
2. Daily Administrator – Managers?
    
3. Controller/CFO – Accounting Manager?
    
4. AR Clerk
    
5. AP Clerk
    
6. Salesperson/Account Manager – Requests, CRM, Quote, Sales Order, Commissions
    
    1. Sales Admin/Sales Support – Requests, CRM, Quote, Sales Order
        
7. Project Coordinator/Project Manager – Requests, Quote, Sales Order, Approved Sales Orders, PO, Acks, WO, Receiving, Time Entry
    
    1. Procurement - Requests, Sales Order, PO, Acknowledgement, Vendor Bills
        
    2. Operations Admin/Support - process Warranty and Service orders -
        
        1. _Warranty Coordinator: **specialized Warranty dashboard elements needed_
            
    3. Estimator (Is this person also a PM or same permissions as a PM? - does the Request assignment remove the need for a separate role?)
        
8. Designer – Requests, Time Entry
    
    **Only for dealers with Internal Operations or who give Subcontractors access to NetSuite
    
9. Estimator – Requests, Time Entry
    
10. Scheduler – Requests, Work Orders, Receiving, Time Entry
    
    (2 roles from the original 25) _**Lead Installer AND Installer - Access thru Joe's apps only and not a Netsuite role???_
    
    **Only for dealers who require these functions - more standardized NetSuite roles**
    
11. Executive
    
12. HR/Payroll
    
13. Marketing – All Marketing functions
    
14. Warehouse Manager/Warehouse ![Question Mark](https://pf-emoji-service--cdn.us-east-1.prod.public.atl-paas.net/atlassian/productivityEmojis/question-64px.png)
    
    _**Are these just a filter set determined by the Supervisor details in the NetSuite employee record??**_
    
15. Accounting Manager
    
16. Sales Leadership/Manager
    
17. PC/PM Manager
    
18. Warehouse Manager
    
19. Ops Manager
    
20. Design Manager
    

Features and Functionality:

- Creation of pre-defined user roles within NetSuite based on the updated list provided
    
- Assignment of specific permissions to each user role based on job responsibilities and requirements
    
- Ability to assign users to one or more roles based on their duties and organizational structure
    
- Restriction of sensitive data and functionality based on user roles to ensure data security and compliance
    
- Integration with custom apps or features to ensure appropriate access to custom functionality
    
- Automated role-based workflows to streamline processes and improve efficiency
    
- Regular auditing and monitoring of user roles and permissions to maintain the integrity of the system
    
- Comprehensive reporting capabilities to track user activity, detect anomalies, and support compliance requirements
    
- Flexibility to accommodate future changes in organizational structure, job responsibilities, or business requirements
    
- User-friendly interface for managing roles and permissions, with clear documentation and training materials
    

## Technical Considerations

Technical Considerations:

1. Blended roles and overlapping permissions:
    
    - Identify common responsibilities and permissions across different roles
        
    - Create a matrix to map out the overlapping permissions and minimize redundancy
        
    - Develop a hierarchy of roles to ensure proper access control and avoid conflicts
        
    - Implement a role-based security model that allows for flexible assignment of permissions
        
2. Configuring dashboards for complex roles:
    
    - Identify key metrics and data points relevant to each complex role
        
    - Design modular dashboard components that can be easily customized and combined
        
    - Develop a framework for creating role-specific dashboards with appropriate access controls
        
    - Ensure dashboards are optimized for performance and user experience
        
3. Dashboard management and publishing:
    
    - Assign dashboard management responsibilities to department/role managers
        
    - Provide training and documentation on dashboard creation, customization, and publishing
        
    - Establish a review and approval process for dashboard updates and modifications
        
    - Implement version control and auditing mechanisms to track dashboard changes
        
4. Manager roles and dashboard access:
    
    - Define manager roles as separate from individual contributor roles
        
    - Grant managers additional permissions to view and manage team-related data
        
    - Configure manager dashboards with "Show All" access to relevant team data
        
    - Set individual contributor dashboards to "Show Mine" by default, limiting access to personal data
        
    - Allow managers to customize and publish dashboards for their team members
        
5. Scalability and performance:
    
    - Optimize NetSuite scripts and customizations to ensure efficient role and permission management
        
    - Regularly monitor and assess the performance impact of role-based customizations
        
    - Implement caching mechanisms to improve dashboard loading times
        
    - Conduct load testing to ensure the system can handle concurrent users and data volume
        
6. Maintenance and updates:
    
    - Establish a process for reviewing and updating roles and permissions based on organizational changes
        
    - Regularly audit user assignments and remove obsolete or unnecessary permissions
        
    - Stay informed about NetSuite updates and patches that may affect role-based functionality
        
    - Develop a plan for testing and deploying updates to minimize disruption to users
        

## Technical Specifications

## Object Definitions

## Data Design

## Scripts and Automations

## Testing and Quality Assurance

1. Test Objectives:
    
    - Validate the proper creation and assignment of user roles and permissions
        
    - Ensure the security and integrity of sensitive data based on role-based access control
        
    - Verify the seamless integration of Provia SuiteApps with the role-based functionality
        
2. Test Environment:
    
    - NetSuite Sandbox account with Provia SuiteApps installed
        
    - Test data representing various user roles, permissions, and organizational scenarios
        
3. Test Data:
    
    - Sample user accounts with different roles and permissions
        
    - Dummy data for transactions, records, and custom fields related to each role
        
    - Test cases covering common user actions, edge cases, and potential security risks
        
4. Test Steps:
    
    - Create and configure user roles based on the predefined list and requirements
        
    - Assign permissions to each role, ensuring proper access control and data security
        
    - Test user login and access to NetSuite features, records, and dashboards based on assigned roles
        
    - Validate role-based restrictions on sensitive data and actions
        
    - Verify the functionality of role-specific dashboards and reports
        
5. Test Assertions:
    
    - Users can only access features and data allowed by their assigned roles and permissions
        
    - Sensitive information is properly secured and accessible only to authorized users
        
    - Dashboards and reports display accurate and relevant data based on user roles
        
    - Provia SuiteApps integrate seamlessly with the role-based access control system
        
    - Performance and scalability meet the expected standards for concurrent users and data volume
        
6. Test Metrics:
    
    - User acceptance rate for role-based access control and dashboards
        
    - Time taken to create, assign, and modify user roles and permissions
        
    - Number of security incidents or unauthorized access attempts detected and prevented
        
7. Test Execution:
    
    - Assign testing tasks to the quality assurance team or dedicated testing resources
        
    - Perform manual and automated testing using predefined test scripts and scenarios
        
    - Document test results, including any issues, bugs, or performance bottlenecks
        
    - Collaborate with the development team to resolve identified issues and optimize the system
        
8. Test Results:
    
    - Compare actual test results with expected outcomes defined in the test cases
        
    - Analyze and summarize test findings, highlighting any discrepancies or areas for improvement
        
    - Provide recommendations for remediation or enhancement based on the test results
        
9. Defect Reporting:
    
    - Categorize and prioritize defects based on severity and impact on user experience
        
    - Create detailed defect reports, including steps to reproduce, expected behavior, and actual results
        
    - Assign defects to the appropriate development or support teams for resolution
        
    - Track and monitor the progress of defect resolution until closure
        
10. Test Script Approval:
    
    - Review and refine the test script based on feedback from stakeholders and subject matter experts
        
    - Obtain sign-off from the project manager, development lead, and key business stakeholders
        
    - Ensure the test script aligns with the overall project goals and requirements
        
    - Maintain version control and update the test script as needed throughout the project lifecycle
        

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