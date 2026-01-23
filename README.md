## SQL-Database-Analysis
Worked with the Northwind sample database to perform end-to-end data analysis using SQL. 
The project focused on extracting meaningful business insights from sales, customers, orders, and products data.
What I did:
1️⃣ Basic SELECT & Filtering
-- Fetch all records from a table
SELECT * FROM flights;

-- Fetch distinct departure airports
SELECT DISTINCT departure_airport FROM flights;

-- Filter records using WHERE
SELECT * FROM tickets
WHERE passenger_name LIKE 'A%';

-- Using AND / OR
SELECT * FROM flights
WHERE status = 'Scheduled' AND aircraft_code = '320';

2️⃣ Aggregation Functions
-- Count total number of tickets
SELECT COUNT(*) AS total_tickets FROM tickets;

-- Total bookings per flight
SELECT flight_id, COUNT(ticket_no) AS bookings
FROM ticket_flights
GROUP BY flight_id;

-- Flights having more than 100 bookings
SELECT flight_id, COUNT(ticket_no) AS bookings
FROM ticket_flights
GROUP BY flight_id
HAVING COUNT(ticket_no) > 100;

3️⃣ Sorting & Limiting Results
-- Order flights by scheduled departure
SELECT * FROM flights
ORDER BY scheduled_departure DESC;

-- Fetch top 10 most expensive tickets
SELECT * FROM ticket_flights
ORDER BY amount DESC
LIMIT 10;

4️⃣ JOIN Operations
-- INNER JOIN
SELECT t.ticket_no, f.flight_no
FROM tickets t
INNER JOIN ticket_flights tf ON t.ticket_no = tf.ticket_no
INNER JOIN flights f ON tf.flight_id = f.flight_id;

-- LEFT JOIN
SELECT a.airport_name, f.flight_no
FROM airports_data a
LEFT JOIN flights f
ON a.airport_code = f.departure_airport;

-- FULL OUTER JOIN
SELECT b.book_ref, t.ticket_no
FROM bookings b
FULL OUTER JOIN tickets t
ON b.book_ref = t.book_ref;

5️⃣ Subqueries & IN Operator
-- Tickets for specific flights
SELECT * FROM ticket_flights
WHERE flight_id IN (
  SELECT flight_id FROM flights
  WHERE status = 'Cancelled'
);

6️⃣ CASE & Conditional Logic
-- Categorize flights based on duration
SELECT flight_id,
CASE
  WHEN scheduled_arrival - scheduled_departure < INTERVAL '2 hours'
    THEN 'Short'
  ELSE 'Long'
END AS flight_type
FROM flights;

7️⃣ Date & Time Functions
-- Extract year from booking date
SELECT EXTRACT(YEAR FROM book_date) AS booking_year
FROM bookings;

-- Format timestamp
SELECT TO_CHAR(book_date, 'DD-Mon-YYYY')
FROM bookings;

8️⃣ String Functions
-- Convert passenger names to uppercase
SELECT UPPER(passenger_name) FROM tickets;

-- Find passengers with last name starting with 'S'
SELECT * FROM tickets
WHERE passenger_name LIKE '% S%';

9️⃣ Window Functions
-- Rank flights based on ticket amount
SELECT flight_id,
amount,
RANK() OVER (PARTITION BY flight_id ORDER BY amount DESC) AS price_rank
FROM ticket_flights;

🔟 UNION & UNION ALL
-- Combine airports from departures and arrivals
SELECT departure_airport FROM flights
UNION
SELECT arrival_airport FROM flights;

1️⃣1️⃣ DDL & DML (Practiced in Course)
-- Create table
CREATE TABLE sample_table (
  id INT PRIMARY KEY,
  name VARCHAR(50)
);

-- Insert data
INSERT INTO sample_table VALUES (1, 'Test');

-- Update data
UPDATE sample_table SET name = 'Updated' WHERE id = 1;

-- Delete data
DELETE FROM sample_table WHERE id = 1;


