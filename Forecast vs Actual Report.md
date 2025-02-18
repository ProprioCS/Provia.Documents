- 1 [Budget vs Actual Report Solution Design](#Budget-vs-Actual-Report-Solution-Design)
    - 1.1 [Executive Summary](#Executive-Summary)
    - 1.2 [Overview](#Overview)
    - 1.3 [Solution Type](#Solution-Type)
    - 1.4 [User Stories](#User-Stories)
    - 1.5 [Success Metrics](#Success-Metrics)
    - 1.6 [Design](#Design)
        - 1.6.1 [UI/UX Overview](#UI%2FUX-Overview)
        - 1.6.2 [Supporting Documents](#Supporting-Documents)
    - 1.7 [Roles and Permissions](#Roles-and-Permissions)
    - 1.8 [Features and Functionality](#Features-and-Functionality)
    - 1.9 [Technical Considerations](#Technical-Considerations)
    - 1.10 [Terminology](#Terminology)
    - 1.11 [Calculation Examples](#Calculation-Examples)
    - 1.12 [Budget Lock Mechanism](#Budget-Lock-Mechanism)
    - 1.13 [Dynamic Blended Projection Calculation](#Dynamic-Blended-Projection-Calculation)
    - 1.14 [Variance Calculation](#Variance-Calculation)
        - 1.14.1 [Actualization Percentage Calculation](#Actualization-Percentage-Calculation)
    - 1.15 [Testing and Quality Assurance](#Testing-and-Quality-Assurance)
- 2 [Changes And Revisions](#Changes-And-Revisions)

## Budget vs Actual Report Solution Design

## Executive Summary

The Budget vs Actual Report is a critical financial tool designed to enhance project management and decision-making capabilities for contract furniture dealers. This solution addresses the unique challenges faced by dealers in tracking complex, often long-running projects with multiple components and potential changes over time.

## Overview

The Budget vs Actual Report implements a Dynamic Blended Projection method, providing real-time insights into project performance by comparing budgeted figures against actual and projected financial data as it becomes available. This approach allows dealers to accurately track project financials throughout the entire lifecycle, from initial quote to final delivery and installation.

The Dynamic Blended Projection now focuses on comparing the sum of extended selling costs and actual costs against the locked budget established at sales order creation. This method enables contract furniture dealers to make data-driven decisions, identify potential cost overruns or profit shortfalls early, and take corrective actions promptly.

## Solution Type

Utility

## User Stories

1. As a Project Manager, I want to view real-time financial data for my ongoing projects, so I can quickly identify any discrepancies between budgeted and actual costs.
    
2. As a Project Manager, I need to assess the financial health of a project at any given point, so I can make informed decisions about resource allocation and timeline adjustments.
    
3. As a Project Manager, I want to see the actualization percentage of my project's budget, so I can accurately report progress to stakeholders and forecast final project outcomes.
    

## Success Metrics

1. Improved Project Profitability: Measure the average increase in gross profit percentage for projects after implementing the Budget vs Actual Report.
    
2. Reduced Budget Overruns: Track the percentage decrease in projects exceeding their initial budget by more than 10%.
    
3. Faster Financial Reporting: Measure the reduction in time spent preparing project financial reports.
    
4. Increased Project Manager Efficiency: Survey Project Managers to assess improvement in their ability to make timely, data-driven decisions.
    
5. Enhanced Forecast Accuracy: Compare projected final costs at project midpoint to actual final costs, aiming for less than 5% variance.
    

## Design

### UI/UX Overview

1. Integration: The Budget vs Actual Report will be integrated directly into the NetSuite Project record interface.
    
2. Display: It will be presented as a table on the project record, providing immediate visibility of key financial data.
    
3. Styling: The report will utilize Orion styling for consistency with other Orion components, distinguishing it from native NetSuite elements.
    
4. Main Component: A dynamic table displaying key financial metrics, with columns for budgeted, projected, and variance figures.
    
5. Interactivity: Interactive elements will allow users to drill down into specific categories or line items for more detailed information.
    
6. Visualization: A graphical representation (e.g., bar chart or gauge) will visualize the actualization percentage for quick reference.
    
7. Quick Overview: Consider creating a visual component similar to CFI Suite's mini-table on the sales order for quick overview.
    

### Supporting Documents

- Detailed wireframes and mockups (to be linked)
    
- Technical documentation outlining integration points with NetSuite's existing Project Management module (to be linked)
    
- Orion style guide and component library references (to be linked)
    

## Roles and Permissions

The following Orion user roles will have access to the Budget vs Actual Report:

1. Orion - Executive Leadership
    
2. Orion - Sales Leadership
    
3. Orion - Ops Manager
    
4. Orion - Project Manager
    
5. Orion - Accounting Manager
    
6. Orion - Controller/CFO
    
7. Orion - Daily Administrator
    

## Features and Functionality

- Real-time financial data display
    
- Dynamic Blended Projection calculation (updated to reflect new logic)
    
- Locked Budget tracking
    
- Detailed financial breakdown
    
- Item Category analysis
    
- Variance calculation between current projections and locked budget
    
- Data Sources integration
    
- Calculation Logic (updated)
    
- Data caching mechanism
    
- JSON budget data storage
    
- User interface interactions
    

## Technical Considerations

1. Performance optimization
    
2. Data volume management
    
3. NetSuite API usage
    
4. Security and data integrity
    
5. Scalability
    
6. Cross-browser compatibility
    
7. Error handling and logging
    
8. Integration with existing Orion components
    
9. NetSuite version compatibility
    
10. Data Storage
    

## Terminology

- Budgeted Sell/Cost: The original estimated sell price and cost from the sales order, locked at the time of sales order creation.
    
- Extended Sell/Cost: The current sell price and cost on the sales order, which can be edited after budget lock.
    
- Projected Sell: A blend of actual invoiced amounts and extended sell amounts for non-invoiced items.
    
- Projected Cost: A blend of actual billed amounts and extended cost amounts for non-billed items.
    
- Actualization Percentage: The percentage of the locked budget that has been realized through invoices and bills.
    

## Calculation Examples

## Budget Lock Mechanism

When a quote is approved and a sales order is created:

1. Extended sell, cost, and list prices are copied to the budgeted fields.
    
2. Budgeted fields are locked and become non-editable.
    
3. Extended fields remain editable.
    
4. Any new lines added to the sales order after this point will not have a corresponding budget.
    

## Dynamic Blended Projection Calculation

Projected Sell = Σ(Invoiced Amounts) + Σ(Non-invoiced Extended Sell Amounts) Projected Cost = Σ(Billed Amounts) + Σ(Non-billed Extended Cost Amounts)

## Variance Calculation

Sell Variance = Projected Sell - Budgeted Sell Cost Variance = Projected Cost - Budgeted Cost GP Variance = (Projected Sell - Projected Cost) - (Budgeted Sell - Budgeted Cost)

### Actualization Percentage Calculation

Actualization % = Σ(Actual Revenue + Actual Costs) / Σ(Budgeted Sell + Budgeted Cost)

Example: Consider a sales order with a locked budget of:

- Budgeted Sell: $10,000
    
- Budgeted Cost: $7,000
    

Current status:

- Invoiced: $6,000
    
- Billed Costs: $4,500
    
- Non-invoiced Extended Sell: $4,500
    
- Non-billed Extended Cost: $3,000
    

Actualization % = ($6,000 + $4,500) / ($10,000 + $7,000) = $10,500 / $17,000 ≈ 61.76%

This shows that approximately 61.76% of the budgeted amount has been realized through invoicing and billing.

## Testing and Quality Assurance

## Changes And Revisions

Be sure to Tag Dev (Luke) any time a new change is made. Format will be

1. Change 1
    
    1. Details
        
2. Change 2
    
    1. Details
        

Be the first to add a reaction