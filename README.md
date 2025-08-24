📘 Assignment: BookMyShow – Theatre Show Listing

P1 – Entities, Attributes & Table Structures

1. Theatre
   
Attributes:

theatre_id (Primary Key)
name
location

SQL Query:

CREATE TABLE Theatre (
    theatre_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    location VARCHAR(100) NOT NULL
);

Sample Data:

INSERT INTO Theatre (name, location) 
VALUES 
('PVR Cinemas', 'Delhi'),
('INOX', 'Mumbai');

Example Rows:

<img width="161" height="41" alt="image" src="https://github.com/user-attachments/assets/b234035b-08c2-470e-ae1e-6fe80c69245a" />


2. Movie

Attributes:

movie_id (Primary Key)
title
language
genre
duration_minutes
certificate_rating

SQL Query:

CREATE TABLE Movie (
    movie_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    language VARCHAR(50),
    genre VARCHAR(50),
    duration_minutes INT,
    certificate_rating VARCHAR(10)
);

Sample Data:

INSERT INTO Movie (title, language, genre, duration_minutes, certificate_rating) 
VALUES
('Inception', 'English', 'Sci-Fi', 148, 'PG-13'),
('3 Idiots', 'Hindi', 'Comedy/Drama', 170, 'U/A'),
('Avengers: Endgame', 'English', 'Action', 181, 'PG-13');

Example Rows:

<img width="391" height="53" alt="image" src="https://github.com/user-attachments/assets/d6de3d3e-f754-4b0d-8f0e-b55de150e103" />


3. Show
   
Attributes:

show_id (Primary Key)
theatre_id (FK → Theatre)
movie_id (FK → Movie)
show_date
show_time

SQL Query:

CREATE TABLE Show (
    show_id INT AUTO_INCREMENT PRIMARY KEY,
    theatre_id INT NOT NULL,
    movie_id INT NOT NULL,
    show_date DATE NOT NULL,
    show_time TIME NOT NULL,
    FOREIGN KEY (theatre_id) REFERENCES Theatre(theatre_id),
    FOREIGN KEY (movie_id) REFERENCES Movie(movie_id)
);

Sample Data:

INSERT INTO Show (theatre_id, movie_id, show_date, show_time)
VALUES
(1, 1, '2025-08-25', '18:00:00'),  -- Inception at PVR
(1, 2, '2025-08-25', '21:00:00'),  -- 3 Idiots at PVR
(2, 2, '2025-08-26', '19:00:00'),  -- 3 Idiots at INOX
(2, 3, '2025-08-26', '22:00:00');  -- Avengers at INOX

Example Rows:

<img width="272" height="64" alt="image" src="https://github.com/user-attachments/assets/faf3b41a-023f-467a-84eb-f5e82b0e372c" />



<img width="807" height="518" alt="Untitled" src="https://github.com/user-attachments/assets/36202255-5a4c-48d1-b08e-9961c7050bcc" />

P2 – Query to List Shows at a Given Theatre on a Given Date

SELECT 
    m.title AS Movie,
    s.show_time AS ShowTime
FROM Show s
JOIN Theatre t ON s.theatre_id = t.theatre_id
JOIN Movie m ON s.movie_id = m.movie_id
WHERE t.name = 'PVR Cinemas'
  AND s.show_date = '2025-08-25'
ORDER BY s.show_time;

Output

<img width="142" height="49" alt="image" src="https://github.com/user-attachments/assets/dbe90486-70aa-48fc-aab3-4a4f8513890e" />

