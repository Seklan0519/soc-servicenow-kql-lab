# SOC KQL and ServiceNow Lab

I am investigating suspicious logins with KQL. I am documenting the case in ServiceNow. This is lab practice to get ready for a SOC analyst role. It is not a real breach. All the logs are fake training data.

I did this lab on my MacBook. I used my browser. I did not need Windows.

## What I did

Step 1.1 is done. I created my Azure Data Explorer environment. I made a free cluster called SOC-Lab. I made a database called SecurityLab.

Step 1.2 is done. I created my ServiceNow instance. I made a Personal Developer Instance called dev268526. I logged in to ServiceNow.

Step 1.3 is done. I opened my ServiceNow instance. I saw the ServiceNow homepage.

Step 2 is not done yet. I will upload the security logs. I will search them with KQL. I will investigate the suspicious account. I will build a timeline.

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

## What I am learning

A log is a record of what a computer did. A failed login is Event ID 4625. A successful login is Event ID 4624. A group change is Event ID 4728.

KQL is the language I use to ask questions about the logs. I will use it to find the failed logins. I will use it to find the successful login after them. I will use it to build a timeline.

ServiceNow is the ticketing system where I will write up the case. Another analyst should be able to read my ticket and understand what happened.

## Screenshots

Screenshots for this lab are in the screenshots folder in this repository. The Step 1.1 screenshot is screenshots 01 azure cluster database.png. It shows the SOC-Lab cluster and the SecurityLab database. The Step 1.3 screenshot is screenshots 02 servicenow environment.png. It shows the ServiceNow homepage after login.

## Source

Lab steps are based on the ServiceNow KQL Complete Beginner Project Guide. The logs are synthetic training data. The IP addresses are reserved for documentation only.

## Tools

I used Azure Data Explorer. I used KQL. I used ServiceNow. I used my MacBook.
