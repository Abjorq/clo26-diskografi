# SQL-inlämning — Diskografi

**Namn:** Anton Björquist
**Artist:** Kanye West 
**Datum:** 18/10 26

---

> Lägg länk till eller bild på ditt ER-diagram här:
> <img width="2760" height="432" alt="er_diagram_enkel" src="https://github.com/user-attachments/assets/a2e3b0b1-7b0c-4e1f-8580-883a21f9ba31" />

> `[ER-diagram](er_diagram.png)`

---

## 1. Skapa databasen — CREATE TABLE

```sql
DROP TABLE IF EXISTS SONG_CONTRIBUTORS;
DROP TABLE IF EXISTS SONGS;
DROP TABLE IF EXISTS CONTRIBUTORS;
DROP TABLE IF EXISTS ALBUMS;

	CREATE TABLE "ALBUMS" (
	"albumid"	INTEGER PRIMARY KEY AUTOINCREMENT,
	"name"	TEXT NOT NULL,
	"releasedate" DATE NOT NULL
);
	CREATE TABLE "CONTRIBUTORS" (
	"contributorid" INTEGER PRIMARY KEY AUTOINCREMENT,
	"name"	TEXT NOT NULL,
	"role"	TEXT NOT NULL
);
	CREATE TABLE "SONGS" (
    "songid" INTEGER PRIMARY KEY AUTOINCREMENT,
	"name" TEXT NOT NULL,
	"playTime"	INTEGER NOT NULL,
	"albumid" INTEGER NOT NULL,
	FOREIGN KEY ("albumid") REFERENCES ALBUMS("albumid")
);
	CREATE TABLE "SONG_CONTRIBUTORS" ( 
	"contributorid" INTEGER NOT NULL,
	"songid" INTEGER NOT NULL,
	PRIMARY KEY ("contributorid", "songid"),
	FOREIGN KEY ("contributorid") REFERENCES CONTRIBUTORS("contributorid"),
	FOREIGN KEY ("songid") REFERENCES SONGS("songid")
);


```

---

## 2. Seeda med data — INSERT

```sql
INSERT INTO ALBUMS (name, releasedate) VALUES
('The College Dropout', '2006-02-27'),
('Graduation', '2009-01-13'),
('ye', '2015-08-28');

INSERT INTO CONTRIBUTORS (name, role) VALUES
('Kanye West', 'Artist & producent'),
('John Legend', 'Gästartist'),
('Miri Ben-Ari', 'Violinist'),
('Ludacris', 'Gästartist'),
('Mos Def', 'Gästartist'),
('Freeway', 'Gästartist'),
('Ty Dolla Sign', 'Gästartist'),
('Ant Clemons', 'Gästartist'),
('PartyNextDoor', 'Gästartist');

INSERT INTO SONGS (name, playTime, albumid) VALUES
('Intro (Skit)', 19, 1),
('We Don''t Care', 239, 1),
('Graduation Day', 82, 1),
('Lil Jimmy (Skit)', 53, 1),
('Good Morning', 195, 2),
('Champion', 168, 2),
('Stronger', 312, 2),
('I Thought About Killing You', 274, 3),
('Yikes', 188, 3),
('All Mine', 145, 3);

--minskade listan av låtar och plockade ut vissa, blir för många annars.


INSERT INTO SONG_CONTRIBUTORS (contributorid, songid) VALUES
(1, 1),
(1, 2),
(1, 3),
(2, 3),
(3, 3),
(1, 4),
(4, 4),
(1, 5),
(1, 6),
(5, 6),
(6, 6),
(1, 7);

```

---

## 3. Söka — SELECT

```sql
--1
SELECT * FROM ALBUMS 
ORDER BY releasedate ASC;

--2
SELECT * FROM SONGS
WHERE albumid = "1";

--3
SELECT a.name AS ALBUMS, COUNT(*) AS songs_per_album
FROM SONGS s
JOIN ALBUMS a ON a.albumid = s.albumid 
GROUP BY a.name;

--4
SELECT name, playTime
FROM SONGS 
ORDER BY playTime DESC
LIMIT 1;

--5
SELECT * FROM SONGS
ORDER BY name;
```

---

## 4. Lägg till en ny rad — INSERT

```sql
INSERT INTO SONGS (name, playTime, albumid) VALUES
('Holiday', 185, 1),
```

---

## 5. Ta bort en rad — DELETE

```sql
DELETE FROM SONGS
WHERE name = 'Intro (Skit)';

```

---

## 6. Uppdatera en rad — UPDATE

```sql
UPDATE CONTRIBUTORS
SET role = 'Gästartist'
WHERE name = 'Miri Bin-Ari';

```

---

## 7. VG-queries (om du siktar på VG)

```sql
--- query 6: Snittlängd på låtar per album ---


--- query 7: Albumet med flest låtar ---


--- query 8: Alla låtar längre än 4 minuter (240 sekunder), med albumtitel ---

```
