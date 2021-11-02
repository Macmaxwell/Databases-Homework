# Class Database

## Submission

Below you will find a set of tasks for you to complete to set up a databases of students and mentors.

To submit this homework write the correct commands for each question here:

```sql


```

When you have finished all of the questions - open a pull request with your answers to the `Databases-Homework` repository.

## Task

1. Create a new database called `cyf_classes` (hint: use `createdb` in the terminal

2. Create a new table `mentors`, for each mentor we want to save their name, how many years they lived in Glasgow, their address and their favourite programming language.
```sql
-- Mentors table
create TABLE Mentors (
  id       SERIAL PRIMARY KEY,
  name     VARCHAR(30) NOT NULL,
  years_living_in_Glasgow   INT NOT NULL,
  address  VARCHAR(120),
  favorite_programming_language    VARCHAR(30)

);

```
3. Insert 5 mentors in the `mentors` table (you can make up the data, it doesn't need to be accurate ;-)).
```sql
INSERT INTO mentors (id,name,years_living_in_Glasgow,favorite_programming_language) VALUES (1,'Bishop David Oyedepo','10','Javascript');
INSERT INTO mentors (id,name,years_living_in_Glasgow,favorite_programming_language)  VALUES (2,'Melinda Marsh','20','Javasript');
INSERT INTO mentors (id,name,years_living_in_Glasgow,favorite_programming_language) VALUES (3,'Martin Sommer','30','Python');
INSERT INTO mentors (id,name,years_living_in_Glasgow,favorite_programming_language) VALUES (4,'Laurence Lebihan','40','CSS');
INSERT INTO mentors (id,name,years_living_in_Glasgow,favorite_programming_language) VALUES (5,'Keith Stewart','50','Java');
```
4. Create a new table `students`, for each student we want to save their name, address and if they have graduated from Code Your Future.
```sql
--Students table
Create Table Students (
  id       SERIAL PRIMARY KEY,
  name     VARCHAR(30) NOT NULL,
  address  VARCHAR(120) Not null,
  graduated_from_cyf boolean Not null  
  )
```

5. Insert 10 students in the `students` table.

```sql
 INSERT INTO Students (id,name,address,graduated_from_cyf) Values(1,'Maxwell Max','street one','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(2,'Juan Carlos','street two','false');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(3,'Peter Brown','street three','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(4,'Charlotte Stone','street ten','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(5,'Alex Bobby','street five','false');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(6,'Sanchez Eva','street two','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(7,'Don Pedro','street ten','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(8,'Bobby Brown','street six','true');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(9,'Toyota Prado','street seven','false');
INSERT INTO Students (id,name,address,graduated_from_cyf) Values(10,'Billy Obama','street four','true');
```
6. Verify that the data you created for mentors and students are correctly stored in their respective tables (hint: use a `select` SQL statement).
```sql
select * from mentors
select * from students
```
7. Create a new `classes` table to record the following information:

   - A class has a leading mentor
   - A class has a topic (such as Javascript, NodeJS)
   - A class is taught at a specific date and at a specific location
```sql
Create TABLE Classes (
  id        SERIAL PRIMARY KEY,
  mentor     Int references mentors(id),
  topic      VARCHAR(120) NOT NULL,
  date       Date not null,
  location   VARCHAR(120)
 );
```
8. Insert a few classes in the `classes` table
```sql
Insert into classes (mentor, topic, date, location) values (1, 'Javascript', '2021-02-10', 'location2');
Insert into classes (mentor, topic, date, location) values (2, 'Python', '2021-05-10', 'location1');
Insert into classes (mentor, topic, date, location) values (3, 'CSS', '2021-04-10', 'location2');
Insert into classes (mentor, topic, date, location) values (4, 'Javascript', '2021-06-10', 'location1');
Insert into classes (mentor, topic, date, location) values (5, 'Database', '2021-08-10', 'location1');
```
9. We now want to store who among the students attends a specific class. How would you store that? Come up with a solution and insert some data if you model this as a new table.
```sql
Create Table student_attendance (
id				   serial primary key,
student_id		Int references students(id),
class_id		   Int references classes(id)
);


Insert into student_attendance (student_id, class_id) values (1,2);
Insert into student_attendance (student_id, class_id) values (2,3);
Insert into student_attendance (student_id, class_id) values (3,4);
Insert into student_attendance (student_id, class_id) values (4,5);
Insert into student_attendance (student_id, class_id) values (5,1);
```
10. Answer the following questions using a `select` SQL statement:
    - Retrieve all the mentors who lived more than 5 years in Glasgow
    - Retrieve all the mentors whose favourite language is Javascript
    - Retrieve all the students who are CYF graduates
    - Retrieve all the classes taught before June this year
    - Retrieve all the students (retrieving student ids only is fine) who attended the Javascript class (or any other class that you have in the `classes` table).
```sql
select * from mentors where years_living_in_Glasgow > 5;
select * from mentors where favorite_programming_language = 'Javascript';
select * from students where graduated_from_cyf = true; 
select * from classes where date < '2021-06-01';  
select student_id from student_attendance where class_id = 1 or class_id = 2;

```