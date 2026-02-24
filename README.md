# Olympic Games Relational Database System

## Team Name and Members

**Team Name:** Group 4
**Course Section:** MIST 4610 (9:55 AM - 11:15 AM)

**Team Members:**

* **Taylor Keller** - [GitHub Repository Link Here]
* **Josie Bowden** - [GitHub Repository Link Here]
* **Tyler Pawlowski** - [GitHub Repository Link Here]
* **Connor Hofmann** - [GitHub Link](https://github.com/conhof27/MIST-4610-Olympic-Data/tree/main)
* **Dean Wadud** - [GitHub Repository Link Here]

## Scenario Description

The Olympic Games represent one of the most logistically complex events in the world, requiring precise coordination across a vast network of people, locations, and schedules.  Our team modeled a comprehensive relational database designed to manage the core operations of the Olympic Games.

This database tracks the hierarchical structure of global competition, starting from the participating **Countries** down to the individual **Athletes** and **Staff** members (such as coaches and medical trainers).  It efficiently schedules competitive **Events** (linked to their broader **Sports**) across various time blocks (**Sessions**) and physical **Venues**.  Furthermore, the model handles fan engagement by tracking **Spectators** and their **Ticket** purchases for specific sessions.  Finally, it securely logs the ultimate outcomes of the games by recording athlete **Results**, including scores, placements, disqualifications, and the specific **Medals** awarded.

## Data Model

*[Olympic Relational Model](https://github.com/conhof27/MIST-4610-Olympic-Data/blob/e5f453e66a5f891ac2c6cf40e96e7217e7493232/Olympic%20Relational%20Model.pdf)*

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

*(Below is a sample of our data dictionary.  Please see the full PDF/Excel file in the repository for all 14 tables).*

### Table: `Result`

| **Column Name** | **Data Type** | **Key** | **Description** | 
| :--- | :--- | :--- | :--- |
| ResultID | INT | PK | Unique identifier for a specific outcome record. | 
| AthleteID | INT | FK | References `Athlete.AthleteID`. Identifies the competitor. | 
| EventID | INT | FK | References `Event.EventID`. Identifies the competition. | 
| MedalID | INT | FK | References `Medal.MedalID`. Indicates Gold, Silver, Bronze, or None. | 
| ScoreOrTime | DECIMAL(10,3) |  | The objective metric achieved (e.g., 9.58 seconds or 15.400 points). | 
| Placement | INT |  | The final rank (1, 2, 3, etc.). NULL if disqualified. | 
| IsDisqualified | TINYINT(1) |  | 0 = False, 1 = True. Flags if the score was invalidated. | 

### Table: `Athlete`

| **Column Name** | **Data Type** | **Key** | **Description** | 
| :--- | :--- | :--- | :--- |
| AthleteID | INT | PK | Unique identifier for the athlete. | 
| CountryID | INT | FK | References `Country.CountryID`. The nation they represent. | 
| FirstName | VARCHAR(50) |  | Athlete's first name. | 
| LastName | VARCHAR(50) |  | Athlete's last name. | 
| Gender | VARCHAR(10) |  | Gender of the athlete (Male, Female). | 
| DateOfBirth | DATE |  | Used to dynamically calculate the athlete's age. | 
| Hometown | VARCHAR(100) |  | City of origin. | 
| DayJob | VARCHAR(100) |  | Their real-world profession outside of sports. | 

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

### Query 1: 

**Description:** 

### Query 2: 

**Description:** 

### Query 3: 

**Description:** 

### Query 4: 

**Description:** 

### Query 5: 

**Description:** 

### Query 6: 

**Description:** 

### Query 7: 

**Description:** 

### Query 8: 

**Description:** 

### Query 9: 

**Description:** 

### Query 10: 

**Description:**
