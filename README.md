# SOC KQL and ServiceNow Lab

I am investigating suspicious logins with KQL. I am documenting the case in ServiceNow. This is lab practice to get ready for a SOC analyst role. It is not a real breach. All the logs are fake training data.

I did this lab on my MacBook. I used my browser. I did not need Windows.

## What I did

Step 1.1 is done. I created my Azure Data Explorer environment. I made a free cluster called SOC-Lab. I made a database called SecurityLab.

Step 1.2 is done. I created my ServiceNow instance. I made a Personal Developer Instance called dev268526. I logged in to ServiceNow.

Step 1.3 is done. I opened my ServiceNow instance. I saw the ServiceNow homepage.

Step 2.1 is done. I created the SecurityEvent table. I picked the CSV file SOC_Lab_SecurityEvent.csv.

Step 2.2 is done. I checked the column mapping. I finished the upload. I verified 63 events in the SecurityEvent table.

Step 3 is done. I searched the logs with KQL. I investigated the suspicious account. I built a timeline.

Step 4 is not done yet. I will assess how bad the suspicious activity is. I will make a ServiceNow ticket. I will write up what I found.

The whole project has 10 steps. I am on Step 3 of 10.

## Step 1.1

I did Step 1.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I opened Google Chrome on my MacBook. I went to dataexplorer.azure.com. I signed in with my Microsoft account. Azure Data Explorer is the tool where I will search the logs. It runs in the browser. I do not need to install anything.

Step 2. I found My Cluster in the left menu. I clicked Create cluster. I picked the free cluster. The free cluster does not need a credit card. It does not need an Azure subscription.

Step 3. I set Cluster display name to SOC-Lab. A cluster is the computer that runs my searches. It is the workspace for the whole lab.

Step 4. I set Database name to SecurityLab. A database is a place to store my investigation data. It is like a filing cabinet inside the cluster.

Step 5. I set Location to North America. I reviewed the terms. I clicked Create. That made the cluster and the database.

Step 6. I checked the cluster page. I saw SOC-Lab at the top. I saw SecurityLab under Databases at the bottom. That proved the cluster and the database were made.

That is Step 1.1 done.

## Step 1.2

I did Step 1.2 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I went to developer.servicenow.com. I signed in with my ServiceNow account. The ServiceNow Developer Program is where I get a free practice instance.

Step 2. I clicked Request Instance. I picked Brazil. Brazil is the newest ServiceNow release. It is a software version name. It is not a place.

Step 3. I clicked Setup Brazil instance. ServiceNow started making my instance. This takes a few minutes. I waited for it to finish.

Step 4. I checked the instance page. I saw Release Brazil. I saw Instance dev268526. I saw Status Online. I saw Username admin. I saw Setup Ready to use. That proved my instance was made and ready.

That is Step 1.2 done.

## Step 1.3

I did Step 1.3 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I clicked Start building. That opened my ServiceNow instance in a new tab. A Personal Developer Instance is my own practice copy of ServiceNow. It is like a simulated company incident system.

Step 2. I logged in with the admin account from my Developer Program dashboard. I did not share the password. I did not put it in a screenshot.

Step 3. I saw the ServiceNow homepage. I saw the top navigation. That proved I was inside ServiceNow and it was working.

That is Step 1.3 done.

## Step 2.1

I did Step 2.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I went back to dataexplorer.azure.com. I opened my SOC-Lab cluster. I picked Ingest data. I picked Local file. Ingestion means importing the file into a database table so I can search it.

Step 2. I picked SecurityLab as the database. I picked New table. I typed SecurityEvent exactly. I clicked the checkmark. A table is the filing cabinet inside the database. Each row will be one security event.

Step 3. I clicked Browse for files. I picked SOC_Lab_SecurityEvent.csv from my data folder. I saw a green checkmark beside the file. That meant Azure accepted the file. It did not mean the logs were imported yet.

That is Step 2.1 done.

## Step 2.2

I did Step 2.2 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I clicked Next. I went to the Inspect stage. I checked the column types before I finished the upload. A column is one field in each record. TimeGenerated is when it happened. EventID is what type of event it was. Account is which user was involved. IpAddress is which IP was recorded. Computer is which computer made the event. LogonType is how the login happened.

Step 2. I checked that TimeGenerated was datetime. I checked that EventID and LogonType were numbers. I checked that the first row was the header. If Azure read a date as text my searches would fail later. So I checked first.

Step 3. I clicked Finish. Azure imported the CSV file into the SecurityEvent table. I ran SecurityEvent | count. The count was 63. That proved all 63 events were in the table.

That is Step 2.2 done.

## Step 3.1

I did Step 3.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran SecurityEvent | take 10. Take 10 means show me 10 rows. That is my first look at the data. It shows me what the logs look like before I search them.

Step 2. I read the results. I saw TimeGenerated and EventID and Account and IpAddress and Computer and LogonType and EventDescription. I saw a 4624 success for jamie.lee at 1:00 PM on Oct 20 on WIN-HR-03. I saw a 4625 failure for jamie.lee at 1:11 PM on the same computer. One failure alone does not mean an attack. It can be a wrong password.

That is Step 3.1 done.

## Step 3.2

I did Step 3.2 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran SecurityEvent | summarize TotalEvents = count() by EventID | order by EventID asc. Summarize means group the rows and count them. By EventID means make one group for each event type. Order by EventID asc means sort from smallest to largest.

Step 2. I read the results. I saw 49 successful logins with EventID 4624. I saw 13 failed logins with EventID 4625. I saw 1 group change with EventID 4728. The total was 63. The failed logins were worth a closer look. The group change was worth a closer look too.

That is Step 3.2 done.

## Step 3.3

I did Step 3.3 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran SecurityEvent | where EventID == 4625 | summarize FailedAttempts = count() by Account, IpAddress, Computer | order by FailedAttempts desc. Where means keep only the rows that match. The double equals means is equal to. So I kept only failed logins.

Step 2. I read the results. I saw 4 accounts with failed logins. Alex.morgan had 8 failures from 203.0.113.77 on WIN-FINANCE-07. Jamie.lee had 2 failures from 198.51.100.21 on WIN-HR-03. Priya.patel had 2 failures from 198.51.100.18 on WIN-MKT-02. Sam.chen had 1 failure from 192.0.2.14 on WIN-SALES-04. The total was 13.

Step 3. I picked alex.morgan to investigate first. 8 failures is 62 percent of all 13 failures. 8 failures from one IP is a pattern. One failure is normal. 8 failures in a short time is worth a closer look.

That is Step 3.3 done.

## Step 3.4

I did Step 3.4 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran a query for alex.morgan from 203.0.113.77 for EventID 4624 and 4625 and 4728. I used project to pick the columns I needed. I used order by TimeGenerated asc to sort from earliest to latest. That builds a timeline. The order matters. 8 failures then a success is more worrying than 8 failures spread out.

Step 2. I read the results. I saw 10 events. I saw 8 failures with EventID 4625 from 14:00 to 14:07 UTC on Oct 20. I saw 1 success with EventID 4624 at 14:09 UTC on WIN-FINANCE-07. LogonType 10 means a remote interactive login. That is RDP. RDP lets someone use a Windows computer from far away. It is normal for IT work. It is a problem if someone uses it without permission.

Step 3. I saw 1 group change with EventID 4728 at 14:11 UTC on DC-LAB-01. Alex.morgan was added to SOC-LAB-Admins. That could mean more access than before. That is called privilege escalation. I do not know yet if it was allowed. I will check that next.

That is Step 3.4 done.

## Step 3.5

I did Step 3.5 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran SecurityEvent | where EventID == 4728 | project TimeGenerated, EventID, Account, MemberName, TargetAccount, Computer, IpAddress, EventDescription | order by TimeGenerated asc. I wanted to check the group change on its own. MemberName is the account added to the group. TargetAccount is the group that was changed.

Step 2. I read the result. I saw 1 event. EventID 4728 at 14:11 UTC on Oct 20. MemberName alex.morgan. TargetAccount SOC-LAB-Admins. Computer DC-LAB-01. IP 203.0.113.77. That confirmed the group change from Step 3.4.

Step 3. I wrote down what I do not know yet. I do not know who made the change. I do not know if it was allowed. The dataset does not show that. So I will not call it a confirmed attack. I will call it possible unauthorized access. It needs a ServiceNow ticket next.

That is Step 3.5 done.

## What I am learning

A log is a record of what a computer did. A failed login is Event ID 4625. A successful login is Event ID 4624. A group change is Event ID 4728.

KQL is the language I use to ask questions about the logs. I used it to find the failed logins. I used it to find the successful login after them. I used it to build a timeline.

I learned three KQL ideas. Where is a filter. It keeps only the rows I want. Summarize is grouping and counting. Project picks the columns I want to see. Order by TimeGenerated asc sorts from earliest to latest.

My main finding is a timeline on Oct 20. 8 failed logins for alex.morgan from 203.0.113.77 from 14:00 to 14:07 UTC. 1 successful RDP login at 14:09 UTC. 1 group change at 14:11 UTC. Alex.morgan was added to SOC-LAB-Admins. That is suspicious. It is not proof of a real attack. All the logs are fake training data.

ServiceNow is the ticketing system where I will write up the case. Another analyst should be able to read my ticket and understand what happened.

## Screenshots

Screenshots for this lab are in the screenshots folder in this repository. The Step 1.1 screenshot is screenshots 01 azure cluster database.png. It shows the SOC-Lab cluster and the SecurityLab database. The Step 1.3 screenshot is screenshots 02 servicenow environment.png. It shows the ServiceNow homepage after login. The Step 2 screenshot is screenshots 03 security logs uploaded.png. It shows the logs imported and 63 events in the table. The Step 3.1 screenshot is screenshots 04 first kql data exploration.png. It shows SecurityEvent | take 10 and the first 10 results. The Step 3.2 screenshot is screenshots 05 event type summary.png. It shows 49 successes and 13 failures and 1 group change. The Step 3.3 screenshot is screenshots 05 suspicious failed logins.png. It shows 8 failures for alex.morgan from 203.0.113.77. The Step 3.4 screenshot is screenshots 06 suspicious login timeline.png. It shows the 10 event timeline from 14:00 to 14:11 UTC. The Step 3.5 screenshot is screenshots 07 security group change.png. It shows the 4728 event for alex.morgan added to SOC-LAB-Admins.

## Source

Lab steps are based on the ServiceNow KQL Complete Beginner Project Guide. The logs are synthetic training data. The IP addresses are reserved for documentation only.

## Tools

I used Azure Data Explorer. I used KQL. I used ServiceNow. I used my MacBook.
