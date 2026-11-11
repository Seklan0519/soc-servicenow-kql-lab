# SOC KQL and ServiceNow Lab

I am investigating suspicious logins with KQL. I am documenting the case in ServiceNow. This is lab practice to get ready for a SOC analyst role. It is not a real breach. All the logs are fake training data.

I did this lab on my MacBook. I used my browser. I did not need Windows.

## What I did

Step 1.1 is done. I created my Azure Data Explorer environment. I made a free cluster called SOC-Lab. I made a database called SecurityLab.

Step 1.2 is not done yet. I will upload the security logs. I will search them with KQL.

Step 2 is not done yet. I will investigate the suspicious account. I will build a timeline.

Step 3 is not done yet. I will make a ServiceNow ticket. I will write up what I found.

## Step 1.1

I did Step 1.1 step by step. Each step has a small note. The note shows what is happening and why I did it.

Step 1. I opened Google Chrome on my MacBook. I went to dataexplorer.azure.com. I signed in with my Microsoft account. Azure Data Explorer is the tool where I will search the logs. It runs in the browser. I do not need to install anything.

Step 2. I found My Cluster in the left menu. I clicked Create cluster. I picked the free cluster. The free cluster does not need a credit card. It does not need an Azure subscription.

Step 3. I set Cluster display name to SOC-Lab. A cluster is the computer that runs my searches. It is the workspace for the whole lab.

Step 4. I set Database name to SecurityLab. A database is a place to store my investigation data. It is like a filing cabinet inside the cluster.

Step 5. I set Location to North America. I reviewed the terms. I clicked Create. That made the cluster and the database.

Step 6. I checked the cluster page. I saw SOC-Lab at the top. I saw SecurityLab under Databases at the bottom. That proved the cluster and the database were made.

That is Step 1.1 done.

## What I am learning

A log is a record of what a computer did. A failed login is Event ID 4625. A successful login is Event ID 4624. A group change is Event ID 4728.

KQL is the language I use to ask questions about the logs. I will use it to find the failed logins. I will use it to find the successful login after them. I will use it to build a timeline.

ServiceNow is the ticketing system where I will write up the case. Another analyst should be able to read my ticket and understand what happened.

## Screenshots

Screenshots for this lab are in the screenshots folder in this repository. The Step 1.1 screenshot is screenshots 01 azure cluster database.png. It shows the SOC-Lab cluster and the SecurityLab database.

## Source

Lab steps are based on the ServiceNow KQL Complete Beginner Project Guide. The logs are synthetic training data. The IP addresses are reserved for documentation only.

## Tools

I used Azure Data Explorer. I used KQL. I used ServiceNow. I used my MacBook.
