- 1 [Overview](#Overview)
- 2 [Success Metrics](#Success-Metrics)
- 3 [Design](#Design)
- 4 [Features and Functionality](#Features-and-Functionality)
- 5 [Technical Specifications](#Technical-Specifications)
    - 5.1 [Object Definitions](#Object-Definitions)
    - 5.2 [Data Design](#Data-Design)
    - 5.3 [Scripts and Automations](#Scripts-and-Automations)
- 6 [Testing Process](#Testing-Process)
    - 6.1 [Unit Tests](#Unit-Tests)
    - 6.2 [Process Tests](#Process-Tests)
- 7 [Time Estimate](#Time-Estimate)

## Overview

The Orion Online Lead Capture Form is a NetSuite-based solution designed to streamline and optimize the lead generation process for contract furniture dealers. By leveraging NetSuite's native online form module and integrating it with external websites, this solution enables dealers to efficiently capture, track, and manage potential opportunities.

Key benefits of the Orion Online Lead Capture Form include:

1. Seamless integration with external websites, allowing for easy embedding of the form and a user-friendly experience for potential leads.
    
2. Automatic data synchronization between the online form and NetSuite, ensuring that all lead information is accurately captured and readily available for follow-up.
    
3. Customizable form fields and layouts, enabling dealers to tailor the form to their specific requirements and gather relevant information from prospects.
    
4. Real-time notifications and alerts for new lead submissions, allowing sales teams to promptly engage with potential customers and improve conversion rates.
    
5. Enhanced reporting and analytics capabilities, providing dealers with valuable insights into lead generation performance and helping identify areas for improvement.
    

By simplifying and automating the lead capture process, this solution aims to help contract furniture dealers efficiently acquire new prospects, improve lead quality, and ultimately drive business growth.

Solution Title: Orion Online Lead Capture Form

Solution Type: Customization

User Stories:

1. As a customer, I want to enter my contact info into an external site so that a knowledgeable sales rep will contact me promptly.
    
2. As a sales representative, I want to receive real-time notifications when a new lead submits their contact information through the online form so that I can quickly engage with the potential customer and improve conversion rates.
    
3. As a marketing manager, I want to have access to detailed reports and analytics on lead generation performance through the online form so that I can identify areas for improvement and optimize our marketing strategies.
    

## Success Metrics

1. Lead Volume: Track the number of leads generated through the online form on a weekly, monthly, and quarterly basis to measure the effectiveness of the lead generation process.
    
2. Lead Quality: Monitor the conversion rate of leads generated through the online form, from initial contact to qualified opportunities and closed deals, to assess the quality of the leads captured.
    
3. Response Time: Measure the average time taken by sales representatives to follow up with new leads submitted through the online form, ensuring prompt engagement and improved chances of conversion.
    
4. Customer Satisfaction: Conduct surveys or gather feedback from customers who submitted their information through the online form to gauge their satisfaction with the experience and the subsequent follow-up process.
    
5. Marketing ROI: Analyze the return on investment (ROI) for marketing campaigns that drive traffic to the online lead capture form, comparing the cost of the campaigns to the revenue generated from the resulting leads.
    

## Design

The Orion Online Lead Capture Form will be designed to seamlessly integrate with the client's existing website design, ensuring a consistent and professional look and feel. The form will be responsive and optimized for various devices, including desktop computers, tablets, and mobile phones, to provide a user-friendly experience across all platforms.

The form will include the following fields:

1. First Name (required)
    
2. Last Name (required)
    
3. Email (required)
    
4. Phone Number (required)
    
5. Company Name (required)
    
6. Role/Title (optional)
    
7. Message (optional)
    

The form will feature a clean and intuitive layout, with clearly labeled input fields and a prominent submit button. The use of placeholders and input validation will guide users through the form completion process and minimize the risk of errors or incomplete submissions.

Upon successful submission of the form, users will receive a confirmation message thanking them for their interest and informing them that a sales representative will be in touch shortly. The confirmation message will be displayed on the same page as the form, maintaining the client's website design consistency.

To ensure the form aligns with the client's website design, custom CSS styles will be applied to match the color scheme, typography, and overall aesthetics of the existing site. The form will be tested thoroughly to guarantee compatibility with various web browsers and devices.

## Features and Functionality

- Record Type: The form will be created as an Online Customer Form in NetSuite.
    
- Form Type: The form will use a Custom HTML Template.
    
- Form Title: The form will be titled "Orion External Customer Form."
    
- Online Availability: The "Enable Online" checkbox will be checked (set to true) to ensure the form is accessible via an external URL.
    
- NetSuite Fields: The form will include the following fields:
    
    - First Name
        
    - Last Name
        
    - Phone Number
        
    - Email
        
    - Company Name
        
    - Comments
        
- Lead Creation:
    
    - In NetSuite, under the Online Customer Form record, you'll find the "Setup Workflow" sublist. Here's how the fields in this sublist should be set up for the Orion Online Lead Capture Form:
        
        1. Create Leads: Checked
            
            - This ensures that a new lead record is created in NetSuite when a form is submitted.
                
        2. Create Customers as Companies: Checked
            
            - This option automatically creates a new company record in NetSuite when a lead is submitted, associating the lead with the company.
                
        3. Create Contacts: Unchecked
            
            - Since the focus is on lead generation, creating contact records is not necessary at this stage.
                
        4. Workflow to Execute on Record Creation: (Optional)
            
            - If there are any specific workflows that need to be triggered upon lead creation, select the appropriate workflow from the dropdown list.
                
            - For example, you might have a workflow that sends an email notification to the sales team or assigns the lead to a specific sales representative based on certain criteria.
                
        5. Workflow to Execute on Record Update: (Optional)
            
            - Similar to the previous field, select a workflow to be executed when the lead record is updated, if applicable.
                
        6. Set Sales Rep: (Optional)
            
            - If you want to automatically assign a sales representative to the newly created lead, you can select a specific sales rep or choose a custom formula to determine the assignment.
                
            - For example, you might use a formula that assigns leads based on their geographic location or industry.
                
        7. Set Lead Status: Lead-Unqualified
            
            - This field sets the default status for newly created leads.
                
            - In this case, we'll set it to "Lead-Unqualified" to indicate that the lead needs to be qualified by the sales team.
                
        8. Set Lead Source: (Custom)
            
            - Set the lead source to the appropriate campaign name or source that corresponds to the Orion Online Lead Capture Form.
                
            - This allows for accurate tracking and attribution of leads generated through this specific form.
                
        9. Set Sales Team: (Optional)
            
            - If your organization uses sales teams, you can assign the newly created lead to a specific team.
                
            - Leave this field blank if sales teams are not applicable or if the assignment will be handled manually.
                
        10. Sales Team Selection: (Optional)
            
            - If you chose to set a sales team in the previous field, select the appropriate team from the dropdown list.
                
        
        Make sure to save the Online Customer Form record after configuring the "Setup Workflow" sublist fields according to your specific requirements.
        
        Keep in mind that some of these fields may have dependencies or require prior configuration in NetSuite, such as setting up lead statuses, lead sources, sales representatives, and workflows. Ensure that these dependencies are addressed before finalizing the Online Customer Form setup.
        
- Lead Source: The "Lead Source" field will be set to the appropriate campaign name. (Dependency: Lead Sources need to be configured for the client.)
    
- Automations:
    
    - Upon form submission, a new lead record will be automatically created in NetSuite with the data provided by the user.
        
    - The lead record will be associated with a new or existing company record based on the company name provided.
        
    - The lead status will be set to "Lead-Unqualified" by default.
        
    - The lead source will be set to the specified campaign name.
        
- User Actions:
    
    - Users will fill out the form fields with their information and submit the form.
        
    - Users will receive a confirmation message upon successful submission, thanking them for their interest and informing them that a sales representative will be in touch shortly.
        

## Technical Specifications

Technical Considerations:

- Custom HTML Template:
    
    - The form will be built using a custom HTML template to ensure flexibility in design and functionality.
        
    - The HTML template will be hosted and referenced on the Online Customer Form record in NetSuite.
        
- CSS Styling:
    
    - CSS will be used to style the form, ensuring it seamlessly integrates with the customer-facing webpage.
        
    - The CSS styles will be included within the HTML template file.
        
    - The form's appearance will be customized to match the client's website design, including colors, typography, and layout.
        
- JavaScript for URL Parameter:
    
    - JavaScript will be used to capture a URL parameter that identifies the specific customer on the form.
        
    - The URL parameter will be appended to the form's submission URL, allowing for proper tracking and association of the submitted data with the corresponding customer record.
        
- Cross-Browser Compatibility:
    
    - The form will be thoroughly tested across various web browsers (e.g., Chrome, Firefox, Safari, Edge) to ensure consistent functionality and appearance.
        
    - Any browser-specific issues will be addressed and resolved during the development process.
        
- Responsive Design:
    
    - The form will be designed to be responsive, adapting to different screen sizes and devices (desktop, tablet, mobile).
        
    - Media queries and flexible layouts will be used to ensure optimal user experience across devices.
        
- Performance Optimization:
    
    - The HTML, CSS, and JavaScript code will be optimized for performance, minimizing file sizes and loading times.
        
    - Proper code minification and compression techniques will be applied to improve the form's loading speed.
        
- Security Considerations:
    
    - The form will be developed with security best practices in mind, protecting against common web vulnerabilities such as cross-site scripting (XSS) and SQL injection.
        
    - User input will be properly validated and sanitized to prevent any malicious data from being submitted.
        
    - CAPTCHA functionality will be implemented to prevent automated form submissions and protect against spam.
        
- NetSuite Integration:
    
    - The form will be integrated with NetSuite using the Online Customer Form functionality.
        
    - The submitted form data will be mapped to the appropriate NetSuite fields and records, ensuring accurate data transfer and storage.
        

Assumptions and Constraints: Assumptions:

- The client's website has a suitable location to embed the online lead capture form.
    
- The client will provide access to their website's HTML, CSS, and JavaScript files for form integration.
    
- The client has an active NetSuite account with the necessary permissions to create and manage Online Customer Forms.
    
- The client will provide the necessary branding assets (e.g., logos, color schemes) to ensure the form aligns with their website's design.
    

Constraints:

- The form's design and functionality must adhere to the client's website design guidelines and brand standards.
    
- The form must be compatible with the latest versions of popular web browsers (e.g., Chrome, Firefox, Safari, Edge).
    
- The form should be optimized for performance, ensuring fast loading times and minimal impact on the website's overall speed.
    
- The form must comply with relevant data privacy and security regulations (e.g., GDPR, CCPA) based on the client's jurisdiction and target audience.
    
- The form's integration with NetSuite must follow NetSuite's Online Customer Form guidelines and best practices.
    

Dependencies:

- The client must configure lead statuses in their NetSuite account before the form can be properly integrated.
    
- The client must set up the appropriate lead sources (campaign names) in NetSuite for accurate tracking and attribution.
    
- The client's IT team or website administrators must be available to assist with the form's integration and deployment on their website.
    

## Object Definitions

## Data Design

## Scripts and Automations

## Testing Process

Test Script Title: Orion Online Lead Capture Form Test Script

Test Objectives:

1. Verify that the Orion Online Lead Capture Form is properly embedded and displayed on the client's website.
    
2. Ensure that all form fields are functional and accept the appropriate data input.
    
3. Confirm that form submissions successfully create new lead records in NetSuite with accurate data mapping.
    

Test Environment:

- Client's website (staging or development environment)
    
- NetSuite Sandbox account
    

Test Data:

- Valid and invalid input data for each form field
    
- Sample lead data for form submissions
    

Test Steps:

1. Access the client's website and navigate to the page containing the Orion Online Lead Capture Form.
    
2. Verify that the form is displayed correctly and aligns with the website's design.
    
3. Test each form field with valid and invalid input data, ensuring proper validation and error handling.
    
4. Submit the form with complete and accurate sample lead data.
    
5. Check the NetSuite Sandbox account to confirm that a new lead record has been created with the submitted data.
    

Test Assertions:

1. The Orion Online Lead Capture Form is visually integrated with the client's website and matches the provided design guidelines.
    
2. All form fields accept the appropriate data input and display relevant error messages for invalid data.
    
3. Form submissions create new lead records in NetSuite with accurate data mapping and field population.
    
4. The CAPTCHA functionality effectively prevents automated form submissions.
    
5. The form remains functional and accessible across different devices and web browsers.
    

Test Metrics:

1. Form load time: The form should load within 2-3 seconds on average internet speed.
    
2. Submission success rate: 100% of form submissions with valid data should successfully create new lead records in NetSuite.
    

Test Execution:

- Perform manual testing by accessing the client's website and interacting with the Orion Online Lead Capture Form.
    
- Use various devices (desktop, tablet, mobile) and web browsers to ensure consistent functionality and accessibility.
    
- Automate form submissions using tools like Selenium or Puppeteer to test the form's performance under high-volume scenarios.
    

Test Results:

- Document the actual results of each test step and compare them with the expected results.
    
- Record any discrepancies, errors, or issues encountered during the testing process.
    

Defect Reporting:

- Report any defects or issues found during testing in the designated issue tracking system (e.g., JIRA, Trello).
    
- Assign appropriate priority and severity levels to each defect based on its impact on form functionality and user experience.
    

Test Script Approval:

- Review the test script with the project stakeholders, including the client and development team.
    
- Obtain approval and sign-off from all relevant parties before proceeding with the testing phase.
    

## Unit Tests

## Process Tests

## Time Estimate

|   |   |
|---|---|
||**Hours**|
|==Development==|32|
|NetSuite Setup|2|
|QA|4|
|**Total**|**38**|

Be the first to add a reaction