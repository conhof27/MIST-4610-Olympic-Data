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
| **1** | **X** |  |  | **X** |  |  | **X** |  |  | 
| **2** | **X** |  |  | **X** |  |  | **X** |  |  | 
| **3** |  |  |  |  |  |  |  | **X** |  | 
| **4** |  |  |  |  |  | **X** |  |  |  | 
| **5** | **X** |  |  | **X** | **X** |  | **X** |  |  | 
| **6** | **X** | **X** |  | **X** | **X** |  | **X** |  |  | 
| **7** | **X** |  |  | **X** | **X** |  | **X** |  |  | 
| **8** |  | **X** | **X** |  |  | **X** | **X** |  |  | 
| **9** | **X** | **X** | **X** |  |  | **X** | **X** |  |  | 
| **10** | **X** |  |  | **X** |  |  | **X** |  |  | 

## Ten Advanced Queries

### Query 1: Total Medals by Country (Simple)

**Description:** 
Query 1 lists the total number of medals won by each country while ordering the from highest amount to lowest. This query joins together the Country, Athlete, and Results tables in order to count the number of medals associated with each country's athletes. The results are filtered to only include rows where a medal was awardded. Then that data is grouped by country name and ordered in descending order of total medals won.
<br>
<img width="581" height="107" alt="Screenshot 2026-03-30 at 1 01 52 PM" src="https://github.com/user-attachments/assets/221683af-c035-40e1-b682-72830c30c22a" /> 
<br>
<img width="158" height="198" alt="Screenshot 2026-03-30 at 1 02 19 PM" src="https://github.com/user-attachments/assets/922fbfc8-1ad6-4116-a6d6-adbbab706703" />

**Justification:**
Query 1 allows managers or olympic fans to conscisely view the number of medals each country has been awarded. This is useful to assess which countries are in the lead by number of medals won. This allows country's olympic success to be compared and ranked in a simple manner, exlcuding factors other than event results. Query 1  allows a manager to analyze a country as a whole, including every event. This compares countries regardless of how many events they compete in but rather how they have competed in the olympics in its entirety.

### Query 2: Average Ticket Price per Sport (Simple)

**Description:** 
Query 2 lists the average ticket price per sport while ordering them from highest price to lowest. The query joins together the Sport, Event, EventSession, Session, and Ticket tables in order to calculate tge average price of tickets associated with each sport. The results are then grouped by sport and ordered in descending order of average ticket price.
<br>
<img width="550" height="148" alt="Screenshot 2026-03-30 at 1 19 47 PM" src="https://github.com/user-attachments/assets/2a370085-8498-4c9d-b4a2-8e33008f71bd" />
<br>
<img width="250" height="258" alt="Screenshot 2026-03-30 at 1 20 19 PM" src="https://github.com/user-attachments/assets/b1dedcfd-492d-47f1-ab5a-2c47310b6037" />

**Justification:**
Query 2 gives a manager perspective on event sporting event's ticket pricing. This query provides conglomerated data on the varying ticket prices across events. This provides comparable pricing data, displaying which events are more costly than others. It could also indicate which event's tickets may be in higher demand- indicated by a higher ticket price. This could provide insight into why certain events are attended more or less than others and which events that spectators would pay a higher ticket price for. 

### Query 3: Total Athletes Registered per Country (Simple)

**Description:** 
Query 3 lists the disctinct event names, gender categories, and associated sport name for all events that are short-to-mid distance races (500m, 1000m, 1500m). The query joins the Event and Sport table and then filters the results using a regulat expression to match only events with those distances in their names. The results are ordered alphabetically by event name and then by event gender. 
<br>
<img width="487" height="86" alt="Screenshot 2026-03-30 at 4 51 40 PM" src="https://github.com/user-attachments/assets/8f279e4a-8e2a-486b-ab01-322508db8479" />
<br>
<img width="361" height="133" alt="Screenshot 2026-03-30 at 4 51 57 PM" src="https://github.com/user-attachments/assets/e5a72ec1-549e-4960-8c90-699f606a8de5" />

**Justification:**

### Query 4: Staff Distribution by Role (Simple) 

**Description:** 
Query 4 lists the first name, last name, country, and date of birth of all athletes born aftre January 1, 2002, who are representing Japan, France, or Austria. This query joins the Athlete and Country tables and filters the results by both date of birth and country name. The results are ordered alphabetically by country name and then by last name.
<br>
<img width="555" height="105" alt="Screenshot 2026-03-30 at 4 57 14 PM" src="https://github.com/user-attachments/assets/9fb8029f-851d-468e-a2a3-cbab9524bd93" />
<br>
<img width="352" height="165" alt="Screenshot 2026-03-30 at 4 55 54 PM" src="https://github.com/user-attachments/assets/854aaf2f-4e4e-4e99-8afb-5d400f7a4318" />

**Justification:**

### Query 5: Athletes Competing in Multiple Sports (Comp.)
<img width="773" height="127" alt="Screenshot 2026-03-30 at 2 02 45 PM" src="https://github.com/user-attachments/assets/b0067bac-c7f4-4326-a6b5-ded96930e6d7" />
<br>
<img width="280" height="214" alt="Screenshot 2026-03-30 at 2 03 11 PM" src="https://github.com/user-attachments/assets/c47ed7ea-8563-4f0d-9a94-a0160d27c352" />

**Description:** 
A composite list of every athlete that competes in more than one sport. (In this scenario, we modified to only include Atheletes that are in 3 or more sports because the original output would've been to long to display)
<br>
**Justification:**

### Query 6: Events with Above-Average Ticket Prices (Comp.)
<img width="651" height="168" alt="Screenshot 2026-03-30 at 3 54 48 PM" src="https://github.com/user-attachments/assets/861b8bdb-dc54-4db3-91c3-d3b5844757f2" />
<br>
<img width="411" height="444" alt="Screenshot 2026-03-30 at 3 55 47 PM" src="https://github.com/user-attachments/assets/a106f671-8d86-400d-a1ef-85f0ec7068d3" />

**Description:** 
Identifies "Premium" events by calculating the average ticket price for each event and using a subquery to only list those that are strictly higher than the overall global average ticket price.
<br>
**Justification:**

### Query 7: Staff Managing Multiple Athletes (Comp.)
<img width="816" height="127" alt="Screenshot 2026-03-30 at 4 01 29 PM" src="https://github.com/user-attachments/assets/928b154f-e2e0-499c-b10c-e3d3280f5175" />
<br>
<img width="333" height="250" alt="Screenshot 2026-03-30 at 4 01 42 PM" src="https://github.com/user-attachments/assets/bb185563-90d4-4cee-99b5-cb5d61851f44" />

**Description:** 
Uses the AthleteStaff bridge table to identify high-level staff members who are individually assigned to manage or care for three or more different athletes, alongside their specific role.
<br>
**Justification:**

### Query 8: Countries with More Medals than Staff (Comp.)
<img width="896" height="86" alt="Screenshot 2026-03-30 at 2 25 15 PM" src="https://github.com/user-attachments/assets/9a3a2479-c7a8-47ef-954d-82b0280fac1e" />
<br>
<img width="156" height="96" alt="Screenshot 2026-03-30 at 2 25 38 PM" src="https://github.com/user-attachments/assets/385101ed-333d-4f20-b858-207179f9624d" />

**Description:** 
Determine and list the countries that have a greater number of medals than staff members relative to that country. 
<br>
**Justification:**

### Query 9: Oldest Medalists per Sport (Comp.)
<img width="849" height="211" alt="Screenshot 2026-03-30 at 2 36 37 PM" src="https://github.com/user-attachments/assets/13d232a7-1fac-4f5a-a93d-4dc0d41c6e11" />
<br>
<img width="285" height="257" alt="Screenshot 2026-03-30 at 2 36 59 PM" src="https://github.com/user-attachments/assets/00728937-ae87-4d56-82c3-31007bec8e62" />

**Description:** 
List the oldest medalists for each sport and include their name, age, and host country. 
<br>
**Justification:**

### Query 10: The Staff Hierarchy (Comp.)
<img width="745" height="128" alt="Screenshot 2026-03-30 at 3 08 30 PM" src="https://github.com/user-attachments/assets/227c83ff-60be-4d87-ab1c-45c54c759bec" />
<br>
<img width="372" height="497" alt="Screenshot 2026-03-30 at 3 08 55 PM" src="https://github.com/user-attachments/assets/32802725-1dbb-4320-9d90-b6684a087c55" />

**Description:**
Utilizes a recursive self-join and an aggregate function to list every Supervisor alongside the exact count of how many subordinate staff members report directly to them.
<br>
**Justification:**
