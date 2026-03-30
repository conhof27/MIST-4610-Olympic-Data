# Olympic Games Relational Database System

## Team Name and Members

**Team Name:** Group 4
**Course Section:** MIST 4610 (9:55 AM - 11:15 AM)

**Team Members:**

* **Taylor Keller** - [@taylorkeller3]([url](https://github.com/taylorkeller3))
* **Josie Bowden** - [GitHub Repository Link Here]
* **Tyler Pawlowski** - [GitHub Repository Link Here]
* **Connor Hofmann** - [GitHub Link](https://github.com/conhof27/MIST-4610-Olympic-Data/tree/main)
* **Dean Wadud** - [GitHub Repository Link Here]

## Scenario Description

The Olympic Games represent one of the most logistically complex events in the world, requiring precise coordination across a vast network of people, locations, and schedules.  Our team modeled a comprehensive relational database designed to manage the core operations of the Olympic Games.

This database tracks the hierarchical structure of global competition, starting from the participating **Countries** down to the individual **Athletes** and **Staff** members (such as coaches and medical trainers).  It efficiently schedules competitive **Events** (linked to their broader **Sports**) across various time blocks (**Sessions**) and physical **Venues**.  Furthermore, the model handles fan engagement by tracking **Spectators** and their **Ticket** purchases for specific sessions.  Finally, it securely logs the ultimate outcomes of the games by recording athlete **Results**, including scores, placements, disqualifications, and the specific **Medals** awarded.

## Data Model

*[Olympic Relational Model](https://github.com/conhof27/MIST-4610-Olympic-Data/blob/5f5ecf40d849ed4d5f3df20fc15c5560b1c1ae6a/Olympic%20Relational%20Model.pdf)*

### Explanation of the Data Model

Our data model consists of 14 unique entities:

* **Core Reference Data:** `Country`, `Venue`, `Sport`, `Medal`, and `Staff_Role`.  These lookup tables ensure data consistency and prevent entry anomalies (e.g., standardizing the 4 types of medals or standardizing IOC codes).

* **People & Roles:** The `Athlete` and `Staff` tables are linked to their respective `Country`.  To account for the reality that an athlete might have multiple coaches and a coach might train multiple athletes, we resolved this M:N relationship with the `Athlete_Staff` bridge table.

* **Scheduling Logistics:** Because an `Event` (like the 100m Sprint) spans multiple time blocks (heats, semi-finals, finals), and a `Session` can host multiple events, they are connected via the `Event_Session` bridge table.  `Sessions` are physically hosted at a single `Venue`.

* **Fan Access:** Fans (`Spectators`) purchase `Tickets` that grant them a specific seat and price point for a specific `Session`.

* **Outcomes:** The `Result` table acts as the ultimate transactional hub.  It connects an `Athlete`, an `Event`, and a `Medal` to record a finalized `ScoreOrTime`, `Placement`, and `IsDisqualified` flag.

**What our database supports:** Tracking current game rosters, managing multi-day event schedules, processing ticket revenue, and tallying current medal leaderboards.
**What our database does NOT support:** It does not store historical Olympic data from previous years, financial payroll for staff/athletes, or highly detailed in-game statistics (like possession time or individual lap splits).

## Data Dictionary

*(Below is our data dictionary. This dictionary shows each of the 14 entities and every attribute within each entity in our database).*

<img width="616" height="190" alt="StaffRole" src="https://github.com/user-attachments/assets/1d091d8e-ccf5-4925-98de-227e50a1f11a" />

<img width="616" height="382" alt="Staff" src="https://github.com/user-attachments/assets/d0d2383a-aaa8-4db4-8ee2-47d06367e12a" />

<img width="616" height="194" alt="AthleteStaff" src="https://github.com/user-attachments/assets/891b2a2c-d49b-4a48-a01d-0be175053d52" />

<img width="614" height="355" alt="Country" src="https://github.com/user-attachments/assets/ff8206f5-92b4-4610-84fb-b564ee5fa208" />

<img width="618" height="438" alt="Athlete" src="https://github.com/user-attachments/assets/3d1a82aa-b078-49b9-9976-4775eeffed7b" />

<img width="619" height="475" alt="Results" src="https://github.com/user-attachments/assets/6a36cae3-36e3-449a-bda8-eb7b9c5b170e" />

<img width="617" height="195" alt="Medals" src="https://github.com/user-attachments/assets/6967b7aa-67df-49f9-b00c-a983def749b3" />

<img width="617" height="170" alt="Sport" src="https://github.com/user-attachments/assets/83aafcd0-2e10-4b34-9ed3-1c1748877eb4" />

<img width="612" height="272" alt="Event" src="https://github.com/user-attachments/assets/6b783793-c5dc-4c1c-b54f-719a38dcab73" />

<img width="623" height="184" alt="EventSession" src="https://github.com/user-attachments/assets/cfa71f9a-96cc-4007-95e4-b129b03eaa83" />

<img width="621" height="328" alt="Session" src="https://github.com/user-attachments/assets/0c8a9d41-6b91-4644-bcdc-5c1b91a8ac26" />

<img width="619" height="423" alt="Venue" src="https://github.com/user-attachments/assets/175509e1-d530-4ecf-8623-efafcdb0cf41" />

<img width="615" height="261" alt="Spectator" src="https://github.com/user-attachments/assets/71c471bc-4e15-472a-a201-0c83902d2e80" />

<img width="623" height="343" alt="Tickets" src="https://github.com/user-attachments/assets/37c4be93-328e-4c95-9a0d-8c0679a34699" />


## Query Complexity Matrix

| **Query** | **Multi-Join** | **Subquery** | **Correlated** | **GROUP BY** | **HAVING** | **Multi-WHERE** | **Built-In/Calc** | **REGEXP** | **NOT EXISTS** | 
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | 
| **1** |  |  |  |  |  |  |  |  |  | 
| **2** |  |  |  |  |  |  |  |  |  | 
| **3** |  |  |  |  |  |  |  |  |  | 
| **4** |  |  |  |  |  |  |  |  |  | 
| **5** |  |  |  |  |  |  |  |  |  | 
| **6** |  |  |  |  |  |  |  |  |  | 
| **7** |  |  |  |  |  |  |  |  |  | 
| **8** |  |  |  |  |  |  |  |  |  | 
| **9** |  |  |  |  |  |  |  |  |  | 
| **10** |  |  |  |  |  |  |  |  |  | 

## Ten Advanced Queries

### Query 1: Total Medals by Country (Simple)

**Description:** 
This query will show which country in each continent has won the most medals in the Olympics

### Query 2: Average Ticket Price per Sport (Simple)

**Description:** 
Determine the average ticket price per sport by looking at every event that has occurred and the ticket price. 

### Query 3: Total Athletes Registered per Country (Simple)

**Description:** 
Lists every country alongside the total count of athletes they sent to the Olympics.

### Query 4: Staff Distribution by Role (Simple) 

**Description:** 
Calculates the total number of registered staff members assigned to each specific job role (e.g., Head Coach, Assistant Coach, Medical).

### Query 5: Athletes Competing in Multiple Sports (Comp.)

**Description:** 
A composite list of every athlete that competes in more than one sport.

### Query 6: Events Operating Below 50% Capacity (Comp.)

**Description:** 
 List which event’s attendance was below 50% full or the events where only half the seats were filled by spectators.

### Query 7: Gold Medal Countries with No Registered Staff (Comp.)

**Description:** 
List the countries that have been awarded a Gold medal but do not have any registered staff to their country. 

### Query 8: Countries with More Staff than Medals (Comp.)

**Description:** 
Determine and list the countries that have a greater number of staff members than medals won relative to that country. 

### Query 9: Oldest Medalists per Sport (Comp.)

**Description:** 
List the oldest medalists for each sport and include their name, age, and host country. 

### Query 10: The Staff Hierarchy (Self-Join) (Comp.)

**Description:**
Utilizes a recursive self-join to list all "Assistant Coaches" alongside the specific First and Last name of the "Head Coach" they report to.
