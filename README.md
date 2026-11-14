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

Step 4 is done. I assessed how bad the suspicious activity is. I compared alex.morgan activity from two IP addresses. I set the severity to Medium.

Step 5.1 is done. I opened the Incidents page in ServiceNow.

Step 5.2 is done. I opened the new incident form. The incident number is INC0010001.

Step 5.3 is done. I filled in the short description. I set Urgency to 2 Medium. I kept State as New. I have not clicked Submit yet.

Step 5.4 is done. I submitted the ticket. I switched to the full Default view. I set Impact to 2 Medium. I set State to In Progress.

Step 5.8 is done. I added Work notes with my investigation. I clicked Update. ServiceNow saved them.

Step 5.10 is done. I attached 4 KQL screenshots to INC0010001. I verified all 4 files.

Step 6.1 is not done yet. I will open Resolution Information. I will review the final outcome. I will not click Resolve yet.

The whole project has 10 steps. I am on Step 6 of 10.

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

## Step 4.1

I did Step 4.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I ran SecurityEvent | where Account == "alex.morgan" | summarize TotalEvents = count() by IpAddress, EventID, LogonType | order by IpAddress asc, EventID asc. Where means keep only alex.morgan. Summarize means group and count. By IpAddress and EventID and LogonType means make one group for each mix of IP and event and logon type.

Step 2. I read the results. I saw 5 groups. From 198.51.100.40 I saw 12 successes and no failures. 4 were LogonType 10 and 8 were LogonType 3. LogonType 3 means a network logon. From 203.0.113.77 I saw 8 failures and 1 success and 1 group change. All 9 logins from that IP were LogonType 10.

Step 3. I compared the two IPs. The first IP looks like normal use. It has only successes. The second IP has 8 failures then a success then a group change. That pattern is worth a closer look. I cannot call the first IP normal for sure. This dataset is small. It is not enough to build a real baseline.

That is Step 4.1 done.

## Step 4.2

I did Step 4.2 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I assessed the severity. Severity means how serious the incident could be. I looked at three things. Likelihood means how strongly the evidence points to bad activity. Impact means what could happen if it was not allowed. Confidence means how sure I am.

Step 2. I set the severity to Medium. The evidence is worrying. I saw 8 failures then a success then a group change. But I have not confirmed unauthorized access. I have not confirmed what SOC-LAB-Admins can do. So it is not High yet.

Step 3. I noted that severity can change. If more evidence shows unauthorized admin access I would raise it to High. That is normal in a real investigation. New evidence changes the rating.

That is Step 4.2 done.

## Step 5.1

I did Step 5.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I switched to my ServiceNow tab. I opened All in the top navigation. I searched for Incidents. I opened the Incidents page.

Step 2. I saw the Incidents View Self Service page. I saw Number and Opened and Short description. I saw a sample incident INC0008111. I did not change it. That is a sample record.

That is Step 5.1 done.

## Step 5.2

I did Step 5.2 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I clicked the blue New button in the upper right. That opened a new incident form. ServiceNow gave it the number INC0010001. I did not change the number.

Step 2. I saw the form fields. I saw Caller and Short description and Impact and Urgency and Assignment group. The form was in View Self Service. That is a simple view. It has fewer fields than the full analyst view. I will switch to the full view later to add my evidence.

That is Step 5.2 done.

## Step 5.3

I did Step 5.3 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I set Urgency to 2 Medium. Urgency means how fast this needs attention. Medium means it needs timely work. I did not pick High. I have not confirmed a compromise yet.

Step 2. I typed the Short description. I typed [SOC LAB] Suspicious RDP Login Followed by Security Group Change. The short description tells another analyst what happened without opening the whole ticket. [SOC LAB] shows this is a lab case. It is not a real breach.

Step 3. I kept State as New. New means the incident was just made. It is not resolved yet. I kept Caller as System Administrator. That is the default in my practice instance. In a real company the Caller would be the person who reported it.

Step 4. I left Comments blank for now. I will add my investigation notes in the full form later. I did not click Submit yet.

That is Step 5.3 done.

## Step 5.4 to 5.8

I did Steps 5.4 to 5.8 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I clicked Submit. ServiceNow saved INC0010001. I switched from Self Service view to Default view. Default view is the full analyst form. It has more fields for investigation notes.

Step 2. I set Impact to 2 Medium. Impact means how much this could affect the business. Medium fits my Medium severity rating. I set State to In Progress. In Progress means I am working on the case. It is no longer New.

Step 3. ServiceNow asked for Work notes before it would save. Work notes are what I did in the investigation. Description says what happened. Work notes say what I checked and what I found. That helps another analyst take over my case without starting again.

Step 4. I pasted my Work notes. I wrote that I checked 63 events. I wrote 49 successes and 13 failures and 1 group change. I wrote the timeline for alex.morgan. I wrote 8 failures from 14:00 to 14:07 UTC. I wrote the RDP success at 14:09 UTC. I wrote the group change at 14:11 UTC. I wrote that I compared two IPs. I wrote my assessment. I wrote that I have not confirmed bad activity. I wrote that I have not confirmed a stolen password. I wrote that I have not confirmed privilege escalation. I wrote my severity is Medium. I wrote my next steps. I wrote to check if the login was allowed. I wrote to check MFA records. I wrote to check if the group change was approved. I wrote to check what SOC-LAB-Admins can do.

Step 5. I clicked Update. ServiceNow saved the Work notes. I saw them in the Activities section. I saw State In Progress. I saw Impact 2 Medium. I saw Urgency 2 Medium. I saw Priority 3 Moderate. Priority comes from Impact and Urgency together. I saw 3 entries in the Activity history.

That is Steps 5.4 to 5.8 done.

## Step 5.10 to 5.12

I did Steps 5.10 to 5.12 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I clicked the paperclip icon at the top of INC0010001. That opened the Attachments window. It said There are no attachments. That meant I had not uploaded evidence yet.

Step 2. I clicked Choose file. I picked 05-Suspicious-Failed-Logins.png. I clicked Open. ServiceNow attached it. I saw Image uploaded in the Activity history. That file proves the 8 failures for alex.morgan.

Step 3. I uploaded the other 3 files one by one. I uploaded 06-Suspicious-Login-Timeline.png. That file proves the failures then the success then the group change. I uploaded 07-Security-Group-Change.png. That file proves the 4728 group change. I uploaded 08-Account-Activity-Comparison.png. That file proves the two IP comparison.

Step 4. I opened the paperclip window again. I saw all 4 files attached. I saw 7 entries in the Activity history. That is 3 entries before plus 4 image uploads. That proved all 4 files were attached.

That is Steps 5.10 to 5.12 done.

## Step 6.1

Step 6.1 is not done yet. I will open Resolution Information. I will review the final outcome. My verdict is Inconclusive. I found suspicious activity. I cannot prove it was allowed. I cannot prove it was not allowed. I will not call it a confirmed attack. I will not call it a real fix. I will write down what I found and what is still not known.

That is Step 6.1 in progress.

## What I am learning

A log is a record of what a computer did. A failed login is Event ID 4625. A successful login is Event ID 4624. A group change is Event ID 4728.

KQL is the language I use to ask questions about the logs. I used it to find the failed logins. I used it to find the successful login after them. I used it to build a timeline.

I learned three KQL ideas. Where is a filter. It keeps only the rows I want. Summarize is grouping and counting. Project picks the columns I want to see. Order by TimeGenerated asc sorts from earliest to latest.

My incident is INC0010001. My State is In Progress. My Impact is 2 Medium. My Urgency is 2 Medium. My Priority is 3 Moderate. My verdict is Inconclusive. I found suspicious activity. I did not confirm a compromise.

My severity rating is Medium. The pattern is 8 failures then a success then a group change. I have not confirmed compromise. Severity can change if new evidence comes in.

My main finding is a timeline on Oct 20. 8 failed logins for alex.morgan from 203.0.113.77 from 14:00 to 14:07 UTC. 1 successful RDP login at 14:09 UTC. 1 group change at 14:11 UTC. Alex.morgan was added to SOC-LAB-Admins. That is suspicious. It is not proof of a real attack. All the logs are fake training data.

ServiceNow is the ticketing system where I will write up the case. Another analyst should be able to read my ticket and understand what happened.

## Screenshots

Screenshots for this lab are in the screenshots folder in this repository. The Step 1.1 screenshot is screenshots 01 azure cluster database.png. It shows the SOC-Lab cluster and the SecurityLab database. The Step 1.3 screenshot is screenshots 02 servicenow environment.png. It shows the ServiceNow homepage after login. The Step 2 screenshot is screenshots 03 security logs uploaded.png. It shows the logs imported and 63 events in the table. The Step 3.1 screenshot is screenshots 04 first kql data exploration.png. It shows SecurityEvent | take 10 and the first 10 results. The Step 3.2 screenshot is screenshots 05 event type summary.png. It shows 49 successes and 13 failures and 1 group change. The Step 3.3 screenshot is screenshots 05 suspicious failed logins.png. It shows 8 failures for alex.morgan from 203.0.113.77. The Step 3.4 screenshot is screenshots 06 suspicious login timeline.png. It shows the 10 event timeline from 14:00 to 14:11 UTC. The Step 3.5 screenshot is screenshots 07 security group change.png. It shows the 4728 event for alex.morgan added to SOC-LAB-Admins. The Step 4.1 screenshot is screenshots 08 account activity comparison.png. It shows alex.morgan activity from 198.51.100.40 with 12 successes and from 203.0.113.77 with 8 failures and 1 success and 1 group change. The Step 5.3 screenshot is screenshots 09 servicenow incident draft.png. It shows INC0010001 with the short description and Urgency 2 Medium and State New before Submit. The Step 5.9 screenshot is screenshots 10 servicenow investigation details.png. It shows INC0010001 with Work notes saved and State In Progress and Priority 3 Moderate. The Step 5.12 screenshot is screenshots 11 servicenow evidence attached.png. It shows all 4 KQL screenshots attached to INC0010001.

## Source

Lab steps are based on the ServiceNow KQL Complete Beginner Project Guide. The logs are synthetic training data. The IP addresses are reserved for documentation only.

## Tools

I used Azure Data Explorer. I used KQL. I used ServiceNow. I used my MacBook.
