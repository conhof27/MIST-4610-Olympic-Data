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
<img width="581" height="107" alt="Screenshot 2026-03-30 at 1 01 52 PM" src="https://github.com/user-attachments/assets/221683af-c035-40e1-b682-72830c30c22a" /> 
<br>
<img width="158" height="198" alt="Screenshot 2026-03-30 at 1 02 19 PM" src="https://github.com/user-attachments/assets/922fbfc8-1ad6-4116-a6d6-adbbab706703" />

**Description:** 
Identifies which countries are performing the best overall by calculating the total number of medals won by their athletic delegation.
**Justification:**
Query 1 allows managers or olympic fans to conscisely view the number of medals each country has been awarded. This is useful to assess which countries are in the lead by number of medals won. This allows country's olympic success to be compared and ranked in a simple manner, exlcuding factors other than event results. Query 1  allows a manager to analyze a country as a whole, including every event. This compares countries regardless of how many events they compete in but rather how they have competed in the olympics in its entirety.

### Query 2: Average Ticket Price per Sport (Simple)
<img width="550" height="148" alt="Screenshot 2026-03-30 at 1 19 47 PM" src="https://github.com/user-attachments/assets/2a370085-8498-4c9d-b4a2-8e33008f71bd" />
<br>
<img width="250" height="258" alt="Screenshot 2026-03-30 at 1 20 19 PM" src="https://github.com/user-attachments/assets/b1dedcfd-492d-47f1-ab5a-2c47310b6037" />

**Description:** 
Determine the average ticket price per sport by looking at every event that has occurred and the ticket price. 
**Justification:**
Query 2 gives a manager perspective on event sporting event's ticket pricing. This query provides conglomerated data on the varying ticket prices across events. This provides comparable pricing data, displaying which events are more costly than others. It could also indicate which event's tickets may be in higher demand- indicated by a higher ticket price. This could provide insight into why certain events are attended more or less than others and which events that spectators would pay a higher ticket price for. 

### Query 3: Total Athletes Registered per Country (Simple)
<img width="567" height="67" alt="Screenshot 2026-03-30 at 1 31 28 PM" src="https://github.com/user-attachments/assets/939ec8e6-828b-4f8f-a55e-d1036e494308" />
<br>
<img width="166" height="199" alt="Screenshot 2026-03-30 at 1 31 53 PM" src="https://github.com/user-attachments/assets/46ebf993-4a44-4a9e-960c-e58b7387698e" />

**Description:** 
Lists every country alongside the total count of athletes they sent to the Olympics.
**Justification:**
Query 3 provides a manager with a list of each country and the number of athletes present at the Olympics. This allows a manager to readily view which country sent the most athletes and which country sent the least. This may provide insight into a country's population size or their investment in Olympic athletes. Query 3 gives Olympic analysts insight into which country may produce more representation across sports. For example, a country with a low number of athletes present at the Olympic Games may not compete in as many events as a country with a higher number of athletes present.

### Query 4: Staff Distribution by Role (Simple) 
<img width="582" height="85" alt="Screenshot 2026-03-30 at 1 36 42 PM" src="https://github.com/user-attachments/assets/5c580324-992d-491f-9c73-8cf65463e13c" />
<br>
<img width="226" height="95" alt="Screenshot 2026-03-30 at 1 37 17 PM" src="https://github.com/user-attachments/assets/29344edd-66bb-4385-9c6f-9a2554405104" />

**Description:** 
Calculates the total number of registered staff members assigned to each specific job role (e.g., Head Coach, Assistant Coach, Medical).
**Justification:**

### Query 5: Athletes Competing in Multiple Sports (Comp.)
<img width="773" height="127" alt="Screenshot 2026-03-30 at 2 02 45 PM" src="https://github.com/user-attachments/assets/b0067bac-c7f4-4326-a6b5-ded96930e6d7" />
<br>
<img width="280" height="214" alt="Screenshot 2026-03-30 at 2 03 11 PM" src="https://github.com/user-attachments/assets/c47ed7ea-8563-4f0d-9a94-a0160d27c352" />

**Description:** 
A composite list of every athlete that competes in more than one sport. (In this scenario, we modified to only include Atheletes that are in 3 or more sports because the original output would've been to long to display)
**Justification:**

### Query 6: Events Operating Below 50% Capacity (Comp.)

**Description:** 
 List which event’s attendance was below 50% full or the events where only half the seats were filled by spectators.
**Justification:**

### Query 7: Gold Medal Countries with No Registered Staff (Comp.)

**Description:** 
List the countries that have been awarded a Gold medal but do not have any registered staff to their country. 
**Justification:**

### Query 8: Countries with More Medals than Staff (Comp.)
<img width="896" height="86" alt="Screenshot 2026-03-30 at 2 25 15 PM" src="https://github.com/user-attachments/assets/9a3a2479-c7a8-47ef-954d-82b0280fac1e" />
<br>
<img width="156" height="96" alt="Screenshot 2026-03-30 at 2 25 38 PM" src="https://github.com/user-attachments/assets/385101ed-333d-4f20-b858-207179f9624d" />

**Description:** 
Determine and list the countries that have a greater number of medals than staff members relative to that country. 
**Justification:**

### Query 9: Oldest Medalists per Sport (Comp.)

**Description:** 
List the oldest medalists for each sport and include their name, age, and host country. 
**Justification:**

### Query 10: The Staff Hierarchy (Comp.)

**Description:**
Utilizes a recursive self-join to list all "Assistant Coaches" alongside the specific First and Last name of the "Head Coach" they report to.
**Justification:**
