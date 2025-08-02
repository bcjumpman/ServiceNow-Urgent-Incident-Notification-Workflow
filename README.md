# ServiceNow Urgent Incident Notification Workflow

## System Overview

This project implements an automated notification system for critical network incidents at Uber's IT Operations team. The solution addresses a critical gap where network outages weren't triggering email notifications, preventing incidents like the 2-hour unnoticed San Francisco data center outage that caused widespread service disruptions.

The system automatically sends email alerts to the Network Operations team whenever critical network incidents are created, ensuring rapid response and preventing SLA breaches.

## Problem Statement

**Business Impact:** A critical network outage in San Francisco went unnoticed for 2 hours, causing:
- Widespread service disruptions affecting thousands of riders and drivers
- Significant revenue loss
- Regulatory scrutiny
- SLA breaches due to delayed response times

**Root Cause:** Critical network incidents weren't triggering email notifications to the Network Operations team. Urgency condition was set to Medium, and assignment group was empty.
![Original conditional notification](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/original_klworkflow.png) 


## Solution Implementation

### Flow Designer Workflow
- **Name:** Critical Network Incidents Notification
- **Trigger:** Incident Created
- **Conditions:** 
  - Urgency = 1 (High) OR Urgency = 2 (Medium)
  - Category = Network
  - Priority = 1 (Critical)
- **Action:** Send email notification to Network Operations team
![New flow designer workflow ](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/updated%20workflow%20conditions.png) 


### Notification
- **Name:** Incident Assignment Notification  
- **Purpose:** Provides redundant notification capability
- **Recipients:** Networking Operations group
- **Template:** Structured email with incident details
![New notification ](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/new%20notification%20.png)
![Recipients ](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/new%20notification%20recipients.png)
![Email setup ](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/what%20will%20it%20contain.png) 

### Email Configuration
- **Recipients:** Networking Operations Group
- **Group Members:** 11 active Network Operations team members
- **Content:** Incident number, description, priority, and response instructions
![Members ](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/group%20members.png) 

## Implementation Steps

### 1. Flow Designer Configuration
1. Created "Critical Network Incidents Notification" flow
2. Set trigger conditions for critical network incidents
3. Configured Send Notification action with proper recipients
4. Added error handling and testing capabilities

### 2. Group Setup
1. Ensured "Networking Operations" was created
2. Ensured all 11 members had valid emails


### 3. Notification Templates
1. Designed email templates with incident details
2. Included priority information and response urgency
3. Added incident links for quick access
4. Configured HTML formatting for readability

### 4. Testing and Validation
1. Created test incidents with Network category and Critical priority
2. Verified email delivery to all 11 members
3. Confirmed workflow execution through Flow Designer logs
4. Validated notification content and formatting

## Architecture Diagram

![System Architecture](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/incident%20workflow.drawio.png)

The workflow follows this sequence:
1. **Incident Creation** - User creates incident with Network category
2. **Trigger Evaluation** - System checks if urgency is High/Medium and category is Network
3. **Priority Calculation** - ServiceNow calculates priority based on Impact + Urgency matrix
4. **Flow Execution** - If Priority = Critical, flow triggers notification action
5. **Email Delivery** - System sends formatted email to Network Operations team
6. **Response** - Team receives alert and responds within SLA timeframes

## Update Set Contents
- **Flow Designer Workflow:** Critical Network Incidents Notification with triggers and actions
- **User Group:** Networking Operations with 11 active members
- **Email Templates:** Formatted notification templates with incident details
- **Test Records:** Sample incidents demonstrating the working system
- **Email Evidence:** Actual email records from sys_email table proving delivery
- **Configuration:** Trigger conditions, recipient lists, and message formatting
![Update set contents](https://github.com/bcjumpman/ServiceNow-Urgent-Incident-Notification-Workflow/blob/main/Images/update_set_final.png)


## Testing Results

### Successful Test Cases
- **Test Incident:** INC0010008 - "NETWORK IS OUT"
- **Trigger Conditions Met:** Category=Network, Priority=1-Critical
- **Email Delivered:** Successfully sent
- **Response Time:** Notification sent within seconds of incident creation
- **Content Validation:** All required fields included (incident number, description, priority)
  

### Performance Metrics
- **Email Delivery Time:** < 30 seconds from incident creation
- **Success Rate:** 100% for incidents meeting trigger conditions
- **Coverage:** All critical network incidents now generate notifications
- **Team Response:** Network Operations team receives immediate alerts

## AI Scenario: Enhanced Intelligent Incident Routing

Current notification systems send alerts to entire teams without considering individual expertise, availability, or workload. An AI-centric system could improve incident routing by matching incidents to the most qualified and available responders.

**Smart Expert Matching:** AI would analyze incident descriptions and automatically route database connectivity issues to database specialists rather than general network engineers, improving resolution speed by matching expertise to problem types.

**Dynamic Availability Intelligence:** The system would consider real-time factors including time zones, current workloads, vacation schedules, and calendar availability. Instead of alerting sleeping engineers, it would route 3 AM incidents to available team members in different time zones.

**Predictive Learning:** Machine learning algorithms would analyze historical resolution patterns, for example, learning that Maria resolves database issues 40% faster than average, or that weekend network problems typically require Level 2 escalation. This data would inform future routing decisions, continuously improving response efficiency and reducing mean time to resolution.

## Benefits Achieved

### Immediate Impact
- **Faster Response Times:** Network Operations team alerted within 30 seconds
- **SLA Compliance:** Prevents future 2-hour delays that breach service agreements

### Long-term Value
- **Scalable Solution:** Flow Designer approach supports future enhancements
- **Audit Trail:** Complete logging of notification delivery and timing

## Future Enhancements
1. **Mobile Push Notifications:** Extend alerts to mobile devices for 24/7 coverage
2. **Escalation Workflows:** Automatic escalation if no response within defined timeframes
