# Olympic Games Relational Database System

## Team Name and Members

**Team Name:** Group 4
**Course Section:** MIST 4610 (9:55 AM - 11:15 AM)

**Team Members:**

* **Taylor Keller** - [@taylorkeller3](https://github.com/taylorkeller3)
* **Josie Bowden** - [GitHub Link](https://github.com/JosieBowden/MIST-4610-Olympic-Data)
* **Tyler Pawlowski** - [GitHub Link](https://github.com/tdpaw11/MIST-4610-Olympic-Data)
* **Connor Hofmann** - [GitHub Link](https://github.com/conhof27/MIST-4610-Olympic-Data/tree/main)
* **Dean Wadud** - [GitHub Link](https://github.com/dean-wadud?tab=repositories)

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
Query 1 lists the total number of medals won by each country while ordering them from highest amount to lowest. This query joins together the Country, Athlete, and Results tables in order to count the number of medals associated with each country's athletes. The results are filtered to only include rows where a medal was awarded. Then that data is grouped by country name and ordered in descending order of total medals won.
<br>
<img width="581" height="107" alt="Screenshot 2026-03-30 at 1 01 52 PM" src="https://github.com/user-attachments/assets/221683af-c035-40e1-b682-72830c30c22a" /> 
<br>
<img width="158" height="198" alt="Screenshot 2026-03-30 at 1 02 19 PM" src="https://github.com/user-attachments/assets/922fbfc8-1ad6-4116-a6d6-adbbab706703" />

**Justification:**
Query 1 allows managers or olympic fans to concisely view the number of medals each country has been awarded. This is useful to assess which countries are in the lead by number of medals won. This allows a country's olympic success to be compared and ranked in a simple manner, excluding factors other than event results. Query 1  allows a manager to analyze a country as a whole, including every event. This compares countries regardless of how many events they compete in but rather how they have competed in the Olympics in its entirety.

### Query 2: Average Ticket Price per Sport (Simple)

**Description:** 
Query 2 lists the average ticket price per sport while ordering them from highest price to lowest. The query joins together the Sport, Event, EventSession, Session, and Ticket tables in order to calculate the average price of tickets associated with each sport. The results are then grouped by sport and ordered in descending order of average ticket price.
<br>
<img width="550" height="148" alt="Screenshot 2026-03-30 at 1 19 47 PM" src="https://github.com/user-attachments/assets/2a370085-8498-4c9d-b4a2-8e33008f71bd" />
<br>
<img width="250" height="258" alt="Screenshot 2026-03-30 at 1 20 19 PM" src="https://github.com/user-attachments/assets/b1dedcfd-492d-47f1-ab5a-2c47310b6037" />

**Justification:**
Query 2 gives a manager perspective on event sporting event's ticket pricing. This query provides conglomerated data on the varying ticket prices across events. This provides comparable pricing data, displaying which events are more costly than others. It could also indicate which event's tickets may be in higher demand- indicated by a higher ticket price. This could provide insight into why certain events are attended more or less than others and which events that spectators would pay a higher ticket price for. 

### Query 3: 500m, 1000m, and 1500m Events by Gender (Simple)

**Description:** 
Query 3 lists the distinct event names, gender categories, and associated sport name for all events that are short-to-mid distance races (500m, 1000m, 1500m). The query joins the Event and Sport table and then filters the results using a regular expression to match only events with those distances in their names. The results are ordered alphabetically by event name and then by event gender.
<br>
<img width="487" height="86" alt="Screenshot 2026-03-30 at 4 51 40 PM" src="https://github.com/user-attachments/assets/8f279e4a-8e2a-486b-ab01-322508db8479" />
<br>
<img width="361" height="133" alt="Screenshot 2026-03-30 at 4 51 57 PM" src="https://github.com/user-attachments/assets/e5a72ec1-549e-4960-8c90-699f606a8de5" />

**Justification:**
Query 3 allows a manager to view the names of events, genders, and sport names for events that are short-to-mid distance races. This is useful to aggregate the data of distance-based races. Many events in the Olympics are defined by distance and this query provides descriptive data of each of these events. This is useful for a broadcaster to neatly organize each event and be sure of accurately sharing information for each event. Furthermore, the alphabetical organization is helpful for quick retrieval of information. 

### Query 4: Post-2002 Athlete Demographics by Country (Simple)

**Description:** 
Query 4 lists the first name, last name, country, and date of birth of all athletes born after January 1, 2002, who are representing Japan, France, or Austria. This query joins the Athlete and Country tables and filters the results by both date of birth and country name. The results are ordered alphabetically by country name and then by last name.
<br>
<img width="555" height="105" alt="Screenshot 2026-03-30 at 4 57 14 PM" src="https://github.com/user-attachments/assets/9fb8029f-851d-468e-a2a3-cbab9524bd93" />
<br>
<img width="352" height="165" alt="Screenshot 2026-03-30 at 4 55 54 PM" src="https://github.com/user-attachments/assets/854aaf2f-4e4e-4e99-8afb-5d400f7a4318" />

**Justification:**
Query 4 lists out Gen Z athletes from Japan, France, and Austria. This could be potentially useful data for the Olympics to understand which athletes younger audiences from those countries are more likely to know, so that they can include those athletes in some form of targeted marketing. This data can also be used to better understand these specific athletes’ preferences from these countries to make higher quality accommodations in terms of dietary preferences, living preferences, etc.

### Query 5: Athletes Competing in Multiple Sports (Comp.)

**Description:** 
Query 5 lists all athletes who have competed in more than 1 distinct sports, their country, and number of unique sports that they competed in. The query joins the Athlete, Country, Results, and Events tables to count the number of distinct sports associated with each athlete. The results are grouped by athlete and filtered using a HAVING clause to include those with more than 1 unique sports. In this scenario, the threshold was modified from more than 1 sport to 3 sports or more so that output could display well on the site. 
<br>
<img width="773" height="127" alt="Screenshot 2026-03-30 at 2 02 45 PM" src="https://github.com/user-attachments/assets/b0067bac-c7f4-4326-a6b5-ded96930e6d7" />
<br>
<img width="280" height="214" alt="Screenshot 2026-03-30 at 2 03 11 PM" src="https://github.com/user-attachments/assets/c47ed7ea-8563-4f0d-9a94-a0160d27c352" />

**Justification:**
Query 5 is useful for managers to have a list of athletes that compete in more than one sport (limited to 3). This is useful for broadcasters to provide insight to listeners on an Olympian’s experience or skill level. This information is useful for coordinators to understand which olympian may require additional accommodations such as transportation between their various events. Additionally, it could be useful for analysts to compare the performance of Olympians who compete in more or less sports than other given Olympians. 

### Query 6: Events with Above-Average Ticket Prices (Comp.)

**Description:** 
Query 6 identifies the "Premium" events by listing all events whose average ticket price is above the overall average ticket price across all tickets. The query joins the Event, Sport, EventSession, Session and Tickets tables to calculate the average ticket price per event. A subquery is used in a HAVING clause to calculate the global average ticket price. Only events with average ticket prices exceeding that threshold are included. The results are ordered by average event price in descending order and then by gender in ascending order.
<br>
<img width="651" height="168" alt="Screenshot 2026-03-30 at 3 54 48 PM" src="https://github.com/user-attachments/assets/861b8bdb-dc54-4db3-91c3-d3b5844757f2" />
<br>
<img width="411" height="444" alt="Screenshot 2026-03-30 at 3 55 47 PM" src="https://github.com/user-attachments/assets/a106f671-8d86-400d-a1ef-85f0ec7068d3" />

**Justification:**
Query 6 gives managers a view of which events are "premium," meaning their ticket price is higher than the average ticket price among all events. This would be useful to managers who want to know who their audience is when it comes to creating promotions, ads, etc. It also puts those events that are in higher demand into one table, making it more convenient for managers to access that information. These are important events for the managers to focus on, as these are their highest spending customers.

### Query 7: Staff Managing Multiple Athletes (Comp.)

**Description:** 
Query 7 lists all staff members who are assigned to manage 3 or more athletes, their role, and the total number of athletes assigned to them. The query joins the Staff, StaffRole, and AthleteStaff tables to count the number of athletes associated with each staff member. The results are grouped by staff member and filtered using a HAVING clause to only include staff members with 3 or more athletes. Then, the data is ordered in descending order by the number of athletes assigned.
<br>
<img width="816" height="127" alt="Screenshot 2026-03-30 at 4 01 29 PM" src="https://github.com/user-attachments/assets/928b154f-e2e0-499c-b10c-e3d3280f5175" />
<br>
<img width="333" height="250" alt="Screenshot 2026-03-30 at 4 01 42 PM" src="https://github.com/user-attachments/assets/bb185563-90d4-4cee-99b5-cb5d61851f44" />

**Justification:**
Query 7 is useful for both managers and staff members, as it displays the names of high-level staff members and the athletes that they’re assigned to, along with their specific roles. This allows managers to easily access which high-level trainers are working with which athletes, helping them assess how valuable these trainers are to the team. It also shows which trainers have the highest workload, and may result in them needing help tending to their athletes or having other jobs picked up by other trainers. 

### Query 8: Countries with More Medals than Staff (Comp.)

**Description:** 
Query 8 lists all countries where the total number of medals won is greater than the total number of staff members associated with that country. Two correlated subqueries are used within the WHERE clause. One to count the staff members per country and another to count the medal-winning results for the country's athletes by joining the Results and Athletes tables. That is filtered for gold, silver, and bronze medals. Only countries where the medal count exceeds the staff count are returned. 
<br>
<img width="896" height="86" alt="Screenshot 2026-03-30 at 2 25 15 PM" src="https://github.com/user-attachments/assets/9a3a2479-c7a8-47ef-954d-82b0280fac1e" />
<br>
<img width="156" height="96" alt="Screenshot 2026-03-30 at 2 25 38 PM" src="https://github.com/user-attachments/assets/385101ed-333d-4f20-b858-207179f9624d" />

**Justification:**
Query 8 is useful for managers to view a concise list of the countries that have produced more medals than the staff number- in relation to that country, itself. This is useful for analysts to compare how staff size may relate to performance. The short list of 3 countries that have achieved a larger medal output than hired staff exemplifies that this is a rare occurrence. Analysts may use this information from Query 9 to further research these given countries and create an in-depth analysis on how each of these country’s staff operates. 

### Query 9: Oldest Medalists per Sport (Comp.)

**Description:** 
Query 9 lists the oldest medal-winning athlete for each sport, their name, and age as of March 31, 2026. The query joins the Sport, Event, Results, and Athlete tables and filters for medal-winning results only. A correlated subquery in the WHERE clause finds the earliest date of birth among the medalist in each sport and only athletes matching that minimum birth date will be returned. The results are ordered alphabetically by sport name.
<br>
<img width="954" height="230" alt="Screenshot 2026-03-31 at 11 00 31 AM" src="https://github.com/user-attachments/assets/47937f92-7f0b-459a-b211-0d22d75d6a88" />
<br>
<img width="433" height="254" alt="Screenshot 2026-03-31 at 11 00 51 AM" src="https://github.com/user-attachments/assets/f0ef3a3d-be39-42ca-9d88-5e5b040efefe" />

**Justification:**
Query 9 shows a manager an itemized list by sport, the oldest olympian’s name, age and host country. This could be useful for coordinators or broadcasters to recognize by name and host country the oldest Olympian competing in each sport. Using this query, each sport could be compared to determine which sport has the oldest competing olympian or to determine how many countries have the same aged oldest olympian. 

### Query 10: The Staff Hierarchy (Comp.)

**Description:**
Query 10 lists every staff member who acts as a supervisor, along with their country, and number of subordinates that report to them. The query performs as a self-join on the Staff table. It treats one instance as the supervisor and the other as the subordinate. It also joins with the Country table to collect the supervisor's country. The results are grouped by supervisor and ordered alphabetically by country name. 
<br>
<img width="745" height="128" alt="Screenshot 2026-03-30 at 3 08 30 PM" src="https://github.com/user-attachments/assets/227c83ff-60be-4d87-ab1c-45c54c759bec" />
<br>
<img width="372" height="497" alt="Screenshot 2026-03-30 at 3 08 55 PM" src="https://github.com/user-attachments/assets/32802725-1dbb-4320-9d90-b6684a087c55" />

**Justification:**
Query 10 allows a manager to view how many subordinates report to each supervisor. This is useful for an Olympic analyst to consider or compare the size of each supervisor’s staff. This is also useful for Olympic coordinators to provide accommodations for staff that may differ from elite accommodations provided to supervisors. Additionally, for Olympic analysts- correlations between staff sizes and winning teams could be easily compared with this query. 


## Database Information 
Name of the database: al_Group_21482_G8

Additional information: Each query listed above is marked in the database using stored procedures which can be called using the following format: CALL TP_Qx();
