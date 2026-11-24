# Product Requirements Documents (PRD)
  
  Project Title: Netpulse
  Course: BU-COS 209


  ## 1. Problem Statement & Overview

### 1.1 The Problem 
 Students over the university normally deal with slow connection ,dead zones when trying to acess the portal or submit an assignment and also during online classes
 - *. Wasted time and movement :  when students have to do an assignment and the network is slow it wastes a lot of time and start having to move around the vicinity .
 - *. Waste of money : when students keeps buying data and the connection is slow or none it is never used to the fullest which puts the students at a lost.


 ### 1.2 Who has this problem 
- . Students :  we need the reliable connection for classes, portal and assignment and to play games sometimes
- . Staffs:  Need structured and good connectivity to send out messages, assignments and hold classes.


## 2. Surveys and Interviews 

### 2.1 Survey Statistics
-  Total people Interviewed: ** 23 students interviewed
-  Most common failed network windows: ** During very hot afternoons around 3pm and hostels like samuel akande 
-  Sharing disrupted work : not able to join classes or submitting an assignment and it doesn't submit.

### 2.2 Interview Notes
-  Student 1: the connection is speed is very frustating at times and unbearable but we adapt
-  Student 2: it didnt allow me submit assignment sometimes and do some transfers which was very frustating 
-  Staff : we don't like it even the wifi isn't that reliable but we just have to go with it



### 2.3 Why Current Solutions Fall Short
- ** WhatsApp & Group Chats: Questions get buried quickly, lack verified timestamps, and rarely confirm whether a fix has happened.
- ** Walking Around: Signal bars do not guarantee usable throughput or low latency, while walking around trying to ground the network.
-  Repeated Retries & Mobile Data Fallbacks: Retrying on flaky connections wastes time and can cause duplicate actions, while mobile data is costly and still struggles in dead zones.



## 3. Proposed Solution & MVP Scope

A simple backend hub that collects time-stamped connectivity reports for campus locations, aggregates recent signals into a clear current status, and lets authorized support staff post official updates.   (Note: Software cannot repair physical network hardware or increase upstream bandwidth, so this system focuses on visibility, getting problems across to the top easier.) 




### Core Features
1.  Quick Connectivity Reporting: Authenticated users submit a short report for a campus location by picking the  Location, Connection Type  (Campus Wi-Fi, Mobile Data, Other),  Status ( Good ,Slow/Lagging , ), and an optional short note.
2.  Location Status Lookup: Users check a campus location to see its current status summary, how many recent reports came in, when the latest update occurred, and whether data is fresh or stale.
3. Clear 3-State Issue Lifecycle: Reported location issues move through three clear states:
  -  1. Reported: Users have submitted recent slowdown or outage reports for the location.
  -  2. Investigating: ICT staff have acknowledged the issue and are checking it.
  - 3. Resolved: ICT staff mark the issue as resolved or post an all-clear update.





## 4. User Roles & What They Can Do

The system keeps access straightforward with three main roles:

-  Student:
  - Can view current connectivity status summaries for campus locations.
  - Can submit a connectivity report for a campus location.
  - 

-  ICT  Staff:
  - Can view location status summaries and clustered recent reports.
  - Can post official status notices and move location issues from ** Reported** to ** Investigating** to  Resolved.
  - Can remove invalid or test reports.

-  Administrator:
  - Can manage university  locations, user roles, and moderation rules.
  - Can review audit logs of official status changes.






## 5. Backend Logic & Data Design (Language-Agnostic)

### 5.1 What Data We Store
- Users: User ID, Account Identifier, Full Name, Role ( Student,  ICT_Staff, Admin), Account Status
- Locations: Location ID, Name, Zone/Building Type, Current Aggregated Status, Issue State ( Reported, Investigating,  Resolved), Last Updated Timestamp
-  Connectivity Reports: Report ID, User ID, Location ID, Connection Type, Usability, Optional Note, Client Request ID, Timestamp.
- Status Logs:Log ID, Location ID, Updated By, Previous State, New State, Official Note, Timestamp.




### 5.2 Key Rules the Backend Enforces
-  Staleness Rule: Only reports within the agreed freshness window count toward live status; older reports are marked stale rather than treated as active conditions.
-  Idempotent Submissions : If a user's connection drops and retries the same report submission with the same request identifier, the system ignores the duplicate rather than creating multiple identical entries.
- Role & State Enforcement: Only authorized ICT/support or admin users can publish official status updates or change an issue state to ** Investigating** or ** Resolved**, recording who made the change and when.



## 6. Benefits
- Clearer, time-stamped visibility into which campus spots are working before students move or start time-sensitive tasks.
- Faster, more structured issue awareness for ICT staff instead of scattered chat complaints.
- Lightweight, reliable status checks and safe retries suited for unstable campus connections.

