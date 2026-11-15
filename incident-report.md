# Incident Report

## Summary

I investigated suspicious logins with KQL. I documented the case in ServiceNow. This is lab practice to get ready for a SOC analyst role. It is not a real breach. All the logs are fake training data.

My incident is INC0010001. My short description is [SOC LAB] Suspicious RDP Login Followed by Security Group Change. My State is In Progress. My Impact is 2 Medium. My Urgency is 2 Medium. My Priority is 3 Moderate. My verdict is Inconclusive.

## What I used

I used Azure Data Explorer. I used KQL. I used ServiceNow. I used my MacBook. I used my browser. I did not need Windows.

My Azure Data Explorer cluster is SOC-Lab. My database is SecurityLab. My table is SecurityEvent. My ServiceNow instance is dev268526.

## Data

I uploaded SOC_Lab_SecurityEvent.csv to the SecurityEvent table. I verified 63 events in the table.

I saw 49 successful logins with EventID 4624. I saw 13 failed logins with EventID 4625. I saw 1 group change with EventID 4728.

## Findings

I checked the failed logins first. Alex.morgan had 8 failures from 203.0.113.77 on WIN-FINANCE-07. Jamie.lee had 2 failures from 198.51.100.21 on WIN-HR-03. Priya.patel had 2 failures from 198.51.100.18 on WIN-MKT-02. Sam.chen had 1 failure from 192.0.2.14 on WIN-SALES-04.

I picked alex.morgan to investigate first. 8 failures is 62 percent of all 13 failures. 8 failures from one IP is a pattern.

## Timeline

I built a timeline for alex.morgan from 203.0.113.77 on Oct 20 2026.

I saw 8 failed logins with EventID 4625 from 14:00 to 14:07 UTC. I saw 1 successful login with EventID 4624 at 14:09 UTC on WIN-FINANCE-07. LogonType 10 means a remote interactive login. That is RDP. I saw 1 group change with EventID 4728 at 14:11 UTC on DC-LAB-01. Alex.morgan was added to SOC-LAB-Admins.

## Comparison

I compared alex.morgan activity from two IP addresses.

From 198.51.100.40 I saw 12 successes and no failures. 4 were LogonType 10 and 8 were LogonType 3. LogonType 3 means a network logon.

From 203.0.113.77 I saw 8 failures and 1 success and 1 group change. All 9 logins from that IP were LogonType 10.

The first IP looks like normal use. It has only successes. The second IP has 8 failures then a success then a group change. That pattern is worth a closer look. I cannot call the first IP normal for sure. This dataset is small. It is not enough to build a real baseline.

## Assessment

My severity rating is Medium. The pattern is 8 failures then a success then a group change. I have not confirmed unauthorized access. I have not confirmed what SOC-LAB-Admins can do. So it is not High yet.

My verdict is Inconclusive. I found suspicious activity. I cannot prove it was allowed. I cannot prove it was not allowed. I will not call it a confirmed attack.

My Resolution code is None. None of the fix codes fit my case. I did not fix a real problem. I did not make a real Problem record. No resolution code has been selected. The investigation remains In Progress because the available evidence is insufficient to confirm or dismiss unauthorized activity. No separate ServiceNow Problem record has been created.

I did not click Resolve. My Activity history has 8 entries.

## What is still not known

I do not know who made the group change. I do not know if the login was allowed. I do not know if the group change was approved. I do not know what SOC-LAB-Admins can do. I do not know if the password was stolen.

In a real case I would check if the login was allowed. I would check MFA records. I would check if the group change was approved. I would check what SOC-LAB-Admins can do. I would check related endpoint and domain controller logs.

If more evidence shows unauthorized admin access I would raise the severity to High.

## Evidence

I attached 4 KQL screenshots to INC0010001. I attached 05 Suspicious Failed Logins. I attached 06 Suspicious Login Timeline. I attached 07 Security Group Change. I attached 08 Account Activity Comparison.

All 12 screenshots for this lab are in the screenshots folder in this repo. My KQL queries are in the queries folder. My sample data is in the sample-data folder.

## Lessons learned

A log is a record of what a computer did. A failed login is Event ID 4625. A successful login is Event ID 4624. A group change is Event ID 4728.

KQL is the language I use to ask questions about the logs. Where is a filter. It keeps only the rows I want. Summarize is grouping and counting. Project picks the columns I want to see. Order by TimeGenerated asc sorts from earliest to latest.

ServiceNow is the ticketing system where I write up the case. Another analyst should be able to read my ticket and understand what happened.

## Lab scope

This lab ends at Step 6.4. That is the last lab step. The logs are synthetic training data. The IP addresses are reserved for documentation only.
