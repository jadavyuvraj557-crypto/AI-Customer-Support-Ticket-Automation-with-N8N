# AI Customer Support Ticket Automation

## Project Overview

AI Customer Support Ticket Automation is an automated workflow designed to process customer support requests using AI. The system analyzes incoming customer complaints, extracts important ticket information, classifies the issue, assigns the appropriate support team, identifies high-priority cases, sends escalation notifications, defines an expected response time, and stores ticket details in Google Sheets.

The goal of this project is to reduce manual ticket handling and help support teams route and manage customer issues more efficiently.

## Features

### 1. AI-Powered Ticket Classification

The workflow uses an AI Agent and Information Extractor to analyze customer support requests and identify:

* Category
* Priority
* Sentiment
* Complexity
* Escalation requirement
* Suggested response
* Ticket summary

### 2. Category-Based Routing

Tickets are automatically routed based on their category:

| Category             | Assigned Team     |
| -------------------- | ----------------- |
| Billing and Payments | Billing Support   |
| Technical Issue      | Technical Support |
| Order and Delivery   | Order Support     |
| Account Issue        | Account Support   |
| Other                | General Support   |

### 3. Automatic Ticket ID Generation

Each ticket receives a unique ticket ID and creation timestamp for tracking and management.

### 4. High-Priority Escalation

The workflow checks the ticket priority automatically.

* **High Priority** → Ticket Status: `Escalated`
* **Other Priority** → Ticket Status: `Normal Support`

High-priority tickets also trigger an automatic escalation notification email to the responsible manager or support team.

### 5. Response SLA / Expected Response Time

The workflow assigns an expected response time based on ticket priority:

* **High Priority** → Respond within 1 hour
* **Other Priority** → Respond within 24 hours

### 6. Automated Email Notifications

The workflow sends ticket information through Gmail, including:

* Ticket ID
* Customer details
* Category
* Priority
* Sentiment
* Complexity
* Assigned team
* Ticket status
* Response SLA
* Customer message
* AI-generated suggested response

### 7. Google Sheets Ticket Storage

All processed ticket information is automatically stored in Google Sheets for record keeping and future reporting.

## Workflow Architecture

```text
Customer Support Request
        ↓
Edit Fields
        ↓
 ┌───────────────────────────────┐
 │                               │
 ↓                               ↓
Merge Input 1                AI Agent
(Customer Details)               ↓
                           Information Extractor
                                   ↓
                            Add Ticket Detail
                                   ↓
                              Merge Input 2
 └───────────────────────────────┘
                 ↓
      Merge (Combine by Position)
                 ↓
          Switch (Category)
                 ↓
     ┌───────────┼───────────┬───────────┬───────────┐
     ↓           ↓           ↓           ↓           ↓
 Billing     Technical     Order       Account      Other
 Support      Support      Support      Support      Support
     └───────────┴───────────┴───────────┴───────────┘
                 ↓
           IF (Priority)
            ↙           ↘
        High Priority   Other Priority
             ↓               ↓
        Escalated        Normal Support
             ↓               ↓
        Response SLA     Response SLA
             ↓               ↓
       Email Alert       Email Notification
             ↓               ↓
             └───────┬───────┘
                     ↓
              Google Sheets
```

## Technologies Used

* n8n
* Google Gemini AI
* Google Generative AI
* Gmail
* Google Sheets
* AI Agent
* Information Extractor

## How the Workflow Works

1. A customer support request enters the workflow.
2. Customer information such as name, email, subject, and message is prepared.
3. The AI Agent analyzes the customer request.
4. The Information Extractor extracts structured information from the AI response.
5. A unique ticket ID and creation timestamp are added.
6. The original customer details and AI-generated ticket information are combined using a Merge node.
7. The Switch node routes the ticket based on its category.
8. The appropriate support team is automatically assigned.
9. The IF node checks whether the ticket is high priority.
10. High-priority tickets are marked as **Escalated** and trigger an escalation notification.
11. Other tickets are marked as **Normal Support**.
12. A Response SLA is assigned.
13. Ticket details are sent through automated email notifications.
14. The complete ticket information is stored in Google Sheets.

## Example Ticket Data

```text
Category: Account Issue
Priority: High
Sentiment: Frustrated
Complexity: Simple
Escalation Required: No
Assigned Team: Account Support
Ticket Status: Escalated
Response SLA: Respond within 1 hour
```

## Key Benefits

* Reduces manual ticket classification
* Automatically routes tickets to the appropriate team
* Identifies urgent customer issues
* Provides faster handling of high-priority tickets
* Defines expected response times
* Generates AI-based suggested responses
* Maintains centralized ticket records
* Improves consistency in customer support operations

## Future Enhancements

* Build a Power BI or Google Looker Studio dashboard for ticket analytics
* Track SLA performance and response times
* Add automatic ticket assignment to individual support agents
* Integrate a database for large-scale ticket storage
* Add ticket resolution and closure tracking
* Send follow-up notifications for unresolved tickets
* Analyze ticket trends and recurring customer issues



The AI Customer Support Ticket Automation workflow successfully processes customer requests from classification and routing through escalation, notification, SLA assignment, and centralized ticket storage.
