## Introduction

- In modern organizations, employee independence has increased significantly. It is now common for workers to divide their time across multiple projects and report to several managers. As a result, managers have fewer informal interactions with their team members and find it increasingly difficult to monitor and manage vacation schedules effectively.

- This lack of centralized visibility often leads to overlapping absences, manual tracking errors, and administrative delays. The Vacation Tracking System (VTS) is intended to address these challenges by providing a unified digital platform for managing employee leave efficiently and transparently.

## Vision Statement

- The Vacation Tracking System (VTS) will empower employees to manage their own vacation time, sick leave, and personal time off without needing detailed knowledge of company or facility policies. It will streamline HR operations, reduce non-core administrative tasks for managers, and foster a greater sense of autonomy and transparency across the organization.

## Business Goals

- Automate the vacation request process to replace the existing manual approach.
- Accelerate approval workflows to reduce processing time from several days to near real-time.
- Simplify the process for employees to submit vacation requests, including urgent cases.
- Ensure reliability by preventing loss or mismanagement of submitted requests.
- Provide visibility for employees into their time-off history and upcoming leave plans.
- Enable managers to easily view team availability and plan resource allocation.
- Reduce operational costs and increase HR department efficiency through automation and digital record-keeping.

## Scope

- The Vacation Tracking System (VTS) will focus on automating and streamlining the vacation and leave management process within the organization. The system aims to provide web-based access for employees and managers to handle vacation requests, approvals, and tracking efficiently.

### In Scope

- Develop a web-based application accessible through standard browsers.
- Integrate with existing legacy and HR systems to retrieve employee information and update leave balances.
- Provide functionality for employees to request vacation, sick leave, and personal time off.
- Enable managers to review, approve, or reject vacation requests.
- Maintain leave history and provide visibility of team availability.

### Out of Scope

- Development of a mobile application.
- Automatic leave approval or decision-making using AI or predictive logic.
- Payroll management and other HR functions not directly related to leave tracking.

## Major Features

The Vacation Tracking System (VTS) will include the following key features:

### Rules-Based Validation

- Implements a flexible, rules-driven system to validate and verify employee leave requests according to company policy.

### Manager Approval Workflow

- Supports optional manager approval before finalizing vacation requests, ensuring proper oversight.

### Historical and Future Requests

- Provides access to vacation records from the previous calendar year and allows employees to submit requests up to 18 months in advance.

### Email Notifications

- Sends automated emails to notify managers of pending approvals and employees of status updates.

### Integration with Existing Infrastructure

- Uses the organization’s existing hardware, middleware, and intranet portal for deployment and authentication (via single sign-on).

### Comprehensive Logging

- Maintains detailed activity logs for all transactions and approvals to support auditing and traceability.

### Administrative Overrides

- Allows HR and system administrators to override restrictions when necessary, with all overrides logged.

### Manager-Granted Leave

- Enables managers to directly award personal leave time to employees within predefined system limits.

### Web Service Interface

- Exposes a service endpoint for internal systems to query an employee’s vacation summary programmatically.

### HR System Integration

- Interfaces with legacy HR systems to synchronize employee details, leave balances, and updates in real time.

## Assumption

The following assumptions are considered true for the successful development and deployment of the Vacation Tracking System (VTS):

- All employees and managers have access to the company intranet and valid login credentials.
- An existing HR system and employee database are available for integration.
- Email infrastructure is already configured and supports automated notifications.
- Company leave policies are already defined and can be represented as system rules.
- Each employee has a unique identifier (e.g., Employee ID) in the HR database.
- Users will access the system using modern browsers (Chrome, Edge, Firefox).
- The organization has sufficient server resources to host the web application.

## Constraints

- The following constraints define the limitations and conditions under which the Vacation Tracking System (VTS) will be designed, developed, and deployed:
- The system must be developed using the existing organizational infrastructure and middleware — no new hardware or major software acquisitions are permitted.
- The solution must integrate seamlessly with the existing HR system and other legacy systems already in use.
- The system must send automated email notifications to employees and managers regarding request status changes.
- The initial release will be web-based only; mobile platforms are excluded from the first phase.
- User authentication must utilize the organization’s existing Single Sign-On (SSO) mechanism.
- All data must comply with organizational privacy, security, and data retention policies.
- The project must be delivered within the approved timeline and allocated budget.
