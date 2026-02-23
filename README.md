# MIST-4610-Olympic-Data
Contains over 2,500 unique entries of fictional Olympic data for an SQL database that also contains a relational model for Group Project #1

Olympic Games Relational Database System

Team Name and Members

Team Name: Group 4
Course Section: MIST 4610 (9:55 AM - 11:15 AM)

Team Members:

Taylor Keller - [GitHub Repository Link Here]

Josie Bowden - [GitHub Repository Link Here]

Tyler Pawlowski - [GitHub Repository Link Here]

Connor Hofmann - [GitHub Repository Link Here]

Dean Wadud - [GitHub Repository Link Here]

Scenario Description

The Olympic Games represent one of the most logistically complex events in the world, requiring precise coordination across a vast network of people, locations, and schedules. Our team modeled a comprehensive relational database designed to manage the core operations of the Olympic Games.

This database tracks the hierarchical structure of global competition, starting from the participating Countries down to the individual Athletes and Staff members (such as coaches and medical trainers). It efficiently schedules competitive Events (linked to their broader Sports) across various time blocks (Sessions) and physical Venues. Furthermore, the model handles fan engagement by tracking Spectators and their Ticket purchases for specific sessions. Finally, it securely logs the ultimate outcomes of the games by recording athlete Results, including scores, placements, disqualifications, and the specific Medals awarded.

Data Model

(Note: Replace Path_To_Your_PNG_File_Here.png with the actual file path of your image when uploading to GitHub)

Explanation of the Data Model

Our data model is in 3rd Normal Form and consists of 14 entities:

Core Reference Data: Country, Venue, Sport, Medal, and Staff_Role. These lookup tables ensure data consistency and prevent entry anomalies (e.g., standardizing the 4 types of medals or standardizing IOC codes).

People & Roles: The Athlete and Staff tables are linked to their respective Country. To account for the reality that an athlete might have multiple coaches and a coach might train multiple athletes, we resolved this M:N relationship with the Athlete_Staff bridge table.

Scheduling Logistics: Because an Event (like the 100m Sprint) spans multiple time blocks (heats, semi-finals, finals), and a Session can host multiple events, they are connected via the Event_Session bridge table. Sessions are physically hosted at a single Venue.

Fan Access: Fans (Spectators) purchase Tickets that grant them a specific seat and price point for a specific Session.

Outcomes: The Result table acts as the ultimate transactional hub. It connects an Athlete, an Event, and a Medal to record a finalized ScoreOrTime, Placement, and IsDisqualified flag.

What our database supports: Tracking current game rosters, managing multi-day event schedules, processing ticket revenue, and tallying current medal leaderboards.
What our database does NOT support: It does not store historical Olympic data from previous years, financial payroll for staff/athletes, or highly detailed in-game statistics (like possession time or individual lap splits).

Data Dictionary

(Below is a sample of our data dictionary. Please see the full PDF/Excel file in the repository for all 14 tables).

Table: Result

Column Name

Data Type

Key

Description

ResultID

INT

PK

Unique identifier for a specific outcome record.

AthleteID

INT

FK

References Athlete.AthleteID. Identifies the competitor.

EventID

INT

FK

References Event.EventID. Identifies the competition.

MedalID

INT

FK

References Medal.MedalID. Indicates Gold, Silver, Bronze, or None.

ScoreOrTime

DECIMAL(10,3)



The objective metric achieved (e.g., 9.58 seconds or 15.400 points).

Placement

INT



The final rank (1, 2, 3, etc.). NULL if disqualified.

IsDisqualified

TINYINT(1)



0 = False, 1 = True. Flags if the score was invalidated.

Table: Athlete

Column Name

Data Type

Key

Description

AthleteID

INT

PK

Unique identifier for the athlete.

CountryID

INT

FK

References Country.CountryID. The nation they represent.

FirstName

VARCHAR(50)



Athlete's first name.

LastName

VARCHAR(50)



Athlete's last name.

Gender

VARCHAR(10)



Gender of the athlete (Male, Female).

DateOfBirth

DATE



Used to dynamically calculate the athlete's age.

Hometown

VARCHAR(100)



City of origin.

DayJob

VARCHAR(100)



Their real-world profession outside of sports.

Query Complexity Matrix

Query

Multi-Join

Subquery

Correlated

GROUP BY

HAVING

Multi-WHERE

Built-In/Calc

REGEXP

NOT EXISTS

1

X





X





X





2

X

X



X





X





3

X





X

X



X





4

















X

5















X



6

X





X

X



X





7

X









X







8

X





X



X

X





9

X









X







10

X



X







X





Ten Advanced Queries

Query 1: Top Medal Producing Nations

Description: Lists the top 10 countries by the total number of medals they have won.
Managerial Justification: This query is vital for the IOC and marketing executives to determine which countries have the most dominant sporting programs, driving broadcasting rights negotiations and global marketing campaigns.

SELECT 
    c.CountryName, 
    COUNT(r.MedalID) AS Total_Medals
FROM Country c
JOIN Athlete a ON c.CountryID = a.CountryID
JOIN Result r ON a.AthleteID = r.AthleteID
JOIN Medal m ON r.MedalID = m.MedalID
WHERE m.MedalType != 'None' AND r.IsDisqualified = 0
GROUP BY c.CountryName
ORDER BY Total_Medals DESC
LIMIT 10;


Results: (Copy Execute to Text here)

Query 2: Percentage of Ticket Revenue by Sport

Description: Calculates the total ticket revenue generated by each sport, alongside the percentage of the overall Olympic ticket revenue it represents.
Managerial Justification: Identifying revenue distribution is critical for financial planning. Organizers use this to allocate future budget resources, adjust ticket pricing tiers, and decide which sports warrant construction of larger stadiums.

SELECT 
    sp.SportName,
    SUM(t.Price) AS Total_Revenue,
    CONCAT(ROUND((SUM(t.Price) / (SELECT SUM(Price) FROM Ticket)) * 100, 2), '%') AS Revenue_Percentage
FROM Sport sp
JOIN Event e ON sp.SportID = e.SportID
JOIN Event_Session es ON e.EventID = es.EventID
JOIN Session s ON es.SessionID = s.SessionID
JOIN Ticket t ON s.SessionID = t.SessionID
GROUP BY sp.SportName
ORDER BY Total_Revenue DESC;


Results: (Copy Execute to Text here)

Query 3: Most Heavily Utilized Venues

Description: Identifies venues that are hosting more than 5 distinct sessions, along with their average ticket price.
Managerial Justification: Helps logistical managers pinpoint which stadiums are experiencing the most wear-and-tear and require the highest concentration of security, sanitation, and event management staff.

SELECT 
    v.Name AS Venue_Name, 
    COUNT(s.SessionID) AS Total_Sessions,
    ROUND(AVG(t.Price), 2) AS Avg_Ticket_Price
FROM Venue v
JOIN Session s ON v.VenueID = s.VenueID
JOIN Ticket t ON s.SessionID = t.SessionID
GROUP BY v.VenueID, v.Name
HAVING COUNT(s.SessionID) > 5
ORDER BY Total_Sessions DESC;


Results: (Copy Execute to Text here)

Query 4: Athletes Without Medals

Description: Returns a list of all athletes who competed but did not win any medals.
Managerial Justification: Useful for national Olympic committees to identify athletes who require more developmental resources, funding, or coaching interventions for the next Olympic cycle.

SELECT 
    a.FirstName, 
    a.LastName, 
    a.Hometown
FROM Athlete a
WHERE NOT EXISTS (
    SELECT 1 
    FROM Result r 
    JOIN Medal m ON r.MedalID = m.MedalID
    WHERE r.AthleteID = a.AthleteID AND m.MedalType != 'None'
);


Results: (Copy Execute to Text here)

Query 5: Identifying Corporate/Edu Spectator Accounts

Description: Finds all spectators who registered for tickets using a .edu or .org email address.
Managerial Justification: Allows marketing departments to segment their customer base. Identifying educational or organizational email addresses enables targeted email campaigns offering bulk discounts or corporate hospitality packages.

SELECT 
    FirstName, 
    LastName, 
    Email
FROM Spectator
WHERE Email REGEXP '\\.(edu|org)$'
ORDER BY LastName ASC;


Results: (Copy Execute to Text here)

Query 6: Overworked Staff Members

Description: Lists the names and roles of staff members who are responsible for managing 3 or more athletes.
Managerial Justification: Human resource managers need to ensure that medical trainers and head coaches are not spread too thin. This identifies bottlenecks where a country might need to hire additional staff to support their athletes safely.

SELECT 
    s.FirstName, 
    s.LastName, 
    sr.RoleName, 
    COUNT(ast.AthleteID) AS Athletes_Managed
FROM Staff s
JOIN Staff_Role sr ON s.RoleID = sr.RoleID
JOIN Athlete_Staff ast ON s.StaffID = ast.StaffID
GROUP BY s.StaffID, s.FirstName, s.LastName, sr.RoleName
HAVING COUNT(ast.AthleteID) >= 3
ORDER BY Athletes_Managed DESC;


Results: (Copy Execute to Text here)

Query 7: Premium Indoor Events

Description: Retrieves a list of all 'Women's' or 'Mixed' events that are taking place in an indoor venue.
Managerial Justification: Assists broadcasting teams in planning camera setups. Indoor venues require different lighting packages and acoustic considerations compared to outdoor stadiums, specifically for high-profile female and mixed events.

SELECT DISTINCT 
    e.EventName, 
    e.GenderCategory, 
    v.Name AS Venue_Name, 
    v.City
FROM Event e
JOIN Event_Session es ON e.EventID = es.EventID
JOIN Session s ON es.SessionID = s.SessionID
JOIN Venue v ON s.VenueID = v.VenueID
WHERE v.IsIndoor = 1 
  AND (e.GenderCategory = 'Women' OR e.GenderCategory = 'Mixed');


Results: (Copy Execute to Text here)

Query 8: Afternoon Swimming and Gymnastics Capacity Check

Description: Calculates the total potential ticket revenue if the venue sells out, specifically for Swimming and Gymnastics sessions that start after 12:00 PM (noon).
Managerial Justification: Prime-time afternoon sessions for popular sports are massive revenue drivers. This query gives financial managers the maximum theoretical gross revenue for these specific high-demand blocks to measure against actual sales.

SELECT 
    sp.SportName, 
    s.SessionDate, 
    s.StartTime,
    (v.Capacity * AVG(t.Price)) AS Max_Potential_Revenue
FROM Sport sp
JOIN Event e ON sp.SportID = e.SportID
JOIN Event_Session es ON e.EventID = es.EventID
JOIN Session s ON es.SessionID = s.SessionID
JOIN Venue v ON s.VenueID = v.VenueID
JOIN Ticket t ON s.SessionID = t.SessionID
WHERE sp.SportName IN ('Swimming', 'Gymnastics') 
  AND s.StartTime >= '12:00:00'
GROUP BY sp.SportName, s.SessionDate, s.StartTime, v.Capacity;


Results: (Copy Execute to Text here)

Query 9: Disqualified North American Athletes

Description: Identifies athletes from North America who were disqualified from any event.
Managerial Justification: Disqualifications can result from false starts, doping violations, or technical rule breaks. Regional compliance officers use this to audit specific continents for rule-breaking trends and enforce stricter pre-game training.

SELECT 
    a.FirstName, 
    a.LastName, 
    c.CountryName, 
    e.EventName
FROM Athlete a
JOIN Country c ON a.CountryID = c.CountryID
JOIN Result r ON a.AthleteID = r.AthleteID
JOIN Event e ON r.EventID = e.EventID
WHERE c.Continent = 'North America' 
  AND r.IsDisqualified = 1;


Results: (Copy Execute to Text here)

Query 10: Elite Over-Performers (Correlated Subquery)

Description: Finds all athletes whose score in a specific event was higher than the average score recorded for that exact same event across all competitors.
Managerial Justification: This isolates true statistical outliers and "elite" performers. Talent scouts, national coaches, and sports analysts use this exact type of correlated data to track athletes who perform significantly above the baseline average of their peers.

SELECT 
    a.FirstName, 
    a.LastName, 
    e.EventName, 
    r.ScoreOrTime
FROM Result r
JOIN Athlete a ON r.AthleteID = a.AthleteID
JOIN Event e ON r.EventID = e.EventID
WHERE r.ScoreOrTime > (
    SELECT AVG(r2.ScoreOrTime)
    FROM Result r2
    WHERE r2.EventID = r.EventID
) AND r.IsDisqualified = 0;


Results: (Copy Execute to Text here)
