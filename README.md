# automated_daily_business_kpi_reporting
n8n workflow for automated business KPI calculation, validation, reporting, and email alerts.


## Project Architecture

### 1. Main KPI Reporting Workflow

The main workflow automates the business KPI reporting process.

**Workflow steps:**

1. Schedule Trigger starts the workflow at the configured time.
2. HTTP Request nodes fetch Orders and Payments data from Beeceptor mock APIs.
3. Merge combines both API responses.
4. AddReportDate prepares the reporting date.
5. CalculateAndValidateKPIs validates the input data and calculates business metrics.
6. ValidationGate routes valid results to report generation and invalid results to a validation alert.
7. Generate_KPI_HTML_Report formats the validated KPIs into an HTML report.
8. Gmail sends the report to the configured recipient.


### 2. Dedicated Error Handler Workflow

A separate workflow named `KPI_Report_Error_Handler`
provides centralized failure notifications.

**Workflow steps:**

1. Error Trigger receives failure information from a configured
   n8n workflow execution.
2. SendErrorHandlerMail sends an email notification through Gmail.
3. The notification can include the workflow name, failed node,
   error details, and execution information when available.

**Configuration:** Select the dedicated error-handler workflow
in the main workflow's Error Workflow setting. Ensure the main
workflow is configured to stop on errors that should trigger
the error handler.

### Screenshots

#### Main KPI Reporting Workflow
<img width="1237" height="435" alt="image" src="https://github.com/user-attachments/assets/bfa0a6b1-9e21-497d-9837-2280be946ca5" />

Shows the scheduled API calls, data merging, KPI calculation,
validation, HTML report generation, and email delivery.



#### Error Handler Workflow
<img width="696" height="337" alt="image" src="https://github.com/user-attachments/assets/c2b183ef-57e1-4323-b73d-39ce17fca2f1" />

Shows the Error Trigger connected to Gmail for automated
failure notifications.



## Technologies Used

- n8n workflow automation
- REST API integration
- Beeceptor mock APIs
- Python
- KPI calculation and data validation
- HTML report generation
- Gmail integration
- Error handling and notifications

## Setup

1. Import the sanitized main workflow JSON into n8n.
2. Import the error-handler workflow JSON.
3. Configure your own API endpoints and Gmail credentials.
4. Select the error-handler workflow in the main workflow's
   Error Workflow setting.
5. Test successful reporting, validation failures, and execution
   errors before enabling the schedule.

## Security

- Never commit passwords, API keys, OAuth tokens, or secrets.
- Remove personal email addresses and unnecessary credential
  references from exported workflow JSON.
- Configure credentials securely inside n8n.
