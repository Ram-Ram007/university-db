# University database


CREATE TABLE university (
    university_id SERIAL PRIMARY KEY,
    university_name VARCHAR
);

CREATE TABLE college (
    college_id SERIAL PRIMARY KEY,
    college_name VARCHAR,
    university_id INTEGER REFERENCES university(university_id)
);

CREATE TABLE course (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR
);


CREATE TABLE college_course (
    college_course_id SERIAL PRIMARY KEY,
    college_id INTEGER REFERENCES college(college_id),
    course_id INTEGER REFERENCES course(course_id)
);

create table subject(
subject_id serial primary key not null , subject_name VARCHAR not null);
CREATE TABLE course_subject (
    course_subject_id SERIAL PRIMARY KEY NOT NULL,
    college_course_id INTEGER REFERENCES college_course (college_course_id),
    subject_id INTEGER REFERENCES subject(subject_id)
);

create table semester(semester_id  SERIAL PRIMARY KEY NOT NULL, month VARCHAR NOT null,year INTEGER NOT null);
create table student(student_id serial primary key not null,student_name VARCHAR not null, course_subject_id INTEGER REFERENCES course_subject (course_subject_id));
create table marks(mark_id serial primary key not null,student_id integer references student(student_id),semester_id integer references semester(semester_id),marks integer)




alter table marks add subject_id integer REFERENCES subject(subject_id);
alter table student add dob integer ;
ALTER TABLE student
ADD phone integer;
ALTER TABLE student
ADD address VARCHAR;
ALTER TABLE student
ADD year_of_join date;
alter table student
drop column course_subject_id;
alter table student
add column college_course_id INTEGER REFERENCES college_course (college_course_id);
--alter table student
--drop column year_join;
alter table student
drop column college_course_id;
ALTER TABLE student
add column college_id INTEGER REFERENCES college(college_id);
ALTER TABLE student
add column course_id INTEGER REFERENCES course(course_id);
alter table course_subject
drop column college_course_id;
ALTER TABLE course_subject
add column course_id INTEGER REFERENCES course(course_id);


--insert 

insert into university ( university_name ) values ('pondicherry university;')

insert into college (college_name, university_id) values('rajiv gandhi college of engineering and technology',1);
insert into college (college_name, university_id) values('Ganesh college college of enginering',1),
('manakula vinayagar institute of technology',1),
('venkateshwara engineering pondicherry',1),
('puducherry technological university',1);

insert into course (course_name) values ('computer science engineering'),('electrical and electronics engineering'),
('electrical and computer engineering'),('mechanical engineering'),('information technology engineering');

insert into subject (subject_name) values('computer programming'),('maths1'),('termodynamics'),('physics'),('chemistry'),('electrical and electronics');
insert into subject (subject_name) values('engineering mechanics'),('data base'),('cloud computing'),('artificial intelligence ');



insert into college_course (college_id,course_id) values(1,1),(1,2),(1,3),(1,4),(1,5);
insert into college_course (college_id,course_id) values(2,1),(2,2),(2,3),(2,4),(2,5);
insert into college_course (college_id,course_id) values(3,1),(3,2),(3,3),(3,4),(3,5);
insert into college_course (college_id,course_id) values(4,1),(4,2),(4,3),(4,4),(4,5);
insert into college_course (college_id,course_id) values(5,1),(5,2),(5,3),(5,4),(5,5);

insert into course_subject(subject_id,course_id) values(1,1),(2,1),(8,1),(9,1),(10,1),(2,2),(4,2),(5,2),(6,2),(7,2),(2,3),(3,3),(5,3),(6,3),(7,3),
(2,4),(3,4),(5,4),(6,4),(7,4),(1,5),(2,5),(8,5),(9,5),(10,5);


alter table semester rename "month" to "sem_month";
alter table semester rename "year" to "sem_year";


insert into semester(sem_month,sem_year)
values ('april',2023);


ALTER TABLE student
ALTER COLUMN phone
TYPE bigint;

ALTER TABLE student
drop column year_of_join;

ALTER TABLE student
add column year_joined integer;


ALTER TABLE student
drop column dob;

	ALTER TABLE student
	add column d_o_b date;





INSERT INTO public.student (student_name,phone,address,college_id,course_id,year_joined,d_o_b) VALUES
	 ('Rin',9092434586,'Puducherry',1,1,2022,'2001-04-11'),
	 ('Naruto',9392434596,'Puducherry',2,2,2022,'2001-03-03'),
	 ('Sakura',9876453765,'Puducherry',3,3,2022,'2000-11-04'),
	 ('Sasuke',8765897654,'Puducherry',4,4,2022,'2001-07-19'),
	 ('Itachi',6876543278,'Leaf village',5,5,2022,'2001-12-01');
	 
	
	
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (1,1,95,1),
	 (1,1,93,2),
	 (1,1,89,8),
	 (1,1,93,9),
	 (1,1,89,10),
	 (2,1,53,4),
	 (2,1,59,5),
	 (2,1,65,6),
	 (2,1,76,7),
	 (2,1,75,2);
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (3,1,100,2),
	 (3,1,99,3),
	 (3,1,98,5),
	 (3,1,100,6),
	 (3,1,100,7),
	 (4,1,30,2),
	 (4,1,40,3),
	 (4,1,68,5),
	 (4,1,90,6),
	 (4,1,100,7);
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (5,1,40,1),
	 (5,1,50,2),
	 (5,1,60,8),
	 (5,1,70,9),
	 (5,1,60,10);
	
	Task - 1
----------
- Build a University students ranking system database.
- University will have multiple colleges
- Each college will have many courses,
- Each Courses will have many subject
- The university follows semester pattern
- Need to store the marks for each subject , semester wise
- design the table structure and relationships
- feed necessary data to query the output

- completed first task

Task - 2
----------
Querys
------
- 1.) get students count college wise

	- SELECT college.college_name, COUNT(student.student_id) AS student_count
FROM college
JOIN student ON college.college_id = student.college_id
GROUP BY college.college_name;

	(or)

- Another method:
    - SELECT
    college.college_name,
    (
        SELECT COUNT(*)
        FROM student
        WHERE student.college_id = college.college_id
    ) AS student_count
FROM college;

- 2.) get students count in a college, course wise

	- SELECT
    college.college_name,
    course.course_name,
    (SELECT COUNT(*)
     FROM student
     WHERE student.college_id = college.college_id
       AND student.course_id = course.course_id) AS student_count
FROM college
JOIN college_course ON college.college_id = college_course.college_id
JOIN course ON college_course.course_id = course.course_id;



- 3.) get the university rank holder across all courses(1 student)

	- SELECT
    university.university_name,
    student.student_name,
    (
        SELECT SUM(marks.marks)
        FROM course_subject
        JOIN marks ON course_subject.course_subject_id = marks.subject_id
        WHERE student.student_id = marks.student_id
    ) AS total_marks
FROM university
JOIN college ON university.university_id = college.university_id
JOIN college_course ON college.college_id = college_course.college_id
JOIN course_subject ON college_course.college_course_id = course_subject.course_id
JOIN marks ON course_subject.course_subject_id = marks.subject_id
JOIN student ON marks.student_id = student.student_id
ORDER BY total_marks DESC
LIMIT 1;


    (or)

- Alter method

     SELECT m.student_id, s.student_name, AVG(m.marks) AS cgp,c2.course_name, c.college_name 
FROM marks m
join student s on s.student_id = m.student_id 
join course c2 on c2.course_id = s.course_id 
join college c on c.college_id = s.college_id 
GROUP BY m.student_id,s.student_name,c2.course_name,c.college_name
HAVING AVG(marks) = (
    SELECT MAX(avg_marks)
    FROM (
        SELECT AVG(marks) AS avg_marks
        FROM marks
        GROUP BY student_id
    ) AS max_avg
);



- 4.) get the list of rank holders each course(5-because total 5 course):

    -  SELECT 
    student_id,
    student_name,
    course_name,
    cgp AS average_marks
FROM (
    SELECT 
        s.student_id,
        s.student_name,
        c.course_name,
        AVG(m.marks) AS cgp,
        rank() OVER(PARTITION BY c.course_id ORDER BY AVG(m.marks) DESC) AS rank
    FROM 
        marks m
    JOIN 
        student s ON s.student_id = m.student_id
    JOIN 
        course c ON c.course_id = s.course_id
    GROUP BY 
        s.student_id, 
        s.student_name,
        c.course_name,
        c.course_id 
) ranked_students
WHERE rank = 1;





- 5.) get the college topper across all courses(5 - because 5 college):

    - WITH CollegeRankHolders AS ( SELECT s.student_id, s.student_name, co.course_id, co.course_name, c.college_id, c.college_name, AVG(m.marks) AS cgp, RANK() OVER (PARTITION BY c.college_id ORDER BY AVG(m.marks) DESC) AS rank FROM marks m JOIN student s ON s.student_id = m.student_id JOIN course co ON co.course_id = s.course_id JOIN college c ON c.college_id = s.college_id GROUP BY s.student_id, s.student_name, co.course_id, co.course_name, c.college_id, c.college_name ) SELECT student_id, student_name, college_name, course_name, cgp FROM CollegeRankHolders WHERE rank = 1;


    

- 6.) get the college toppers each course(depends upon the toppers in course)

    - WITH CollegeCourseToppers AS (
    SELECT
        student.student_id,
        student.student_name,
        course.course_name,
        college.college_name,
        marks.marks,
        ROW_NUMBER() OVER (PARTITION BY college.college_id, course.course_id ORDER BY marks.marks DESC) AS rank
    FROM
        student
    JOIN
        college ON student.college_id = college.college_id
    JOIN
        marks ON student.student_id = marks.student_id
    JOIN
        college_course ON student.course_id = college_course.college_course_id
    JOIN
        course ON college_course.course_id = course.course_id
)
SELECT
    student_id,
    student_name,
    college_name,
    course_name,
    marks
FROM
    CollegeCourseToppers
WHERE
    rank = 1;

    (or)

-  select student_id,student_name,college_name ,course_name,cgp as avg_marks
from(
	select m.student_id ,s.student_name, c.college_name,c2.course_name, AVG(m.marks) AS cgp,
rank() over(partition by c2.course_id,c.college_id  order by AVG(m.marks) DESC) as ranking
from marks m 
join student s on s.student_id = m.student_id 
join college c on c.college_id = s.college_id 
join course c2 on c2.course_id = s.course_id 
group by m.student_id ,s.student_name, c.college_name,c2.course_id,c.college_id  ,c2.course_name) course_rank
where ranking =1;



- 7.) get the failed students count each subject 

	- SELECT
    subject.subject_name,
    COUNT(*) AS failed_students_count
FROM subject
JOIN course_subject ON subject.subject_id = course_subject.subject_id
JOIN marks ON course_subject.course_subject_id = marks.subject_id
JOIN student ON marks.student_id = student.student_id
WHERE marks.marks < 40
GROUP BY subject.subject_name;

			(or)
- Another method:
    - SELECT
    subject.subject_name,
    (SELECT COUNT(*)
     FROM course_subject
     JOIN marks ON course_subject.course_subject_id = marks.subject_id
     JOIN student ON marks.student_id = student.student_id
     WHERE subject.subject_id = course_subject.subject_id
       AND marks.marks < 40) AS failed_students_count
FROM subject;

    (or)

- SELECT COUNT(*)
FROM (
    SELECT student_id
    FROM marks
    WHERE marks < 40 
    GROUP BY student_id
    HAVING COUNT(DISTINCT subject_id) > 1
) AS dt;


- 8.) get over all students list with semester marks:

	-  SELECT m.student_id, s.student_name, AVG(m.marks) AS cgp,c2.course_name,s2.sem_month,s2.sem_year
FROM marks m
join student s on s.student_id = m.student_id 
join course c2 on c2.course_id = s.course_id 
join semester s2 on s2.semester_id = m.semester_id 
where s2.sem_month ='april' and s2.sem_year =2023
GROUP BY m.student_id,s.student_name,c2.course_name,s2.sem_month,s2.sem_year


- 9.) get the student list who wasnt appear to the exams

	- SELECT
    student.student_id,
    student.student_name
FROM student
LEFT JOIN marks ON student.student_id = marks.student_id
WHERE marks.mark IS NULL;

`Basic query`

- To see total number of students:

    - SELECT COUNT(*) AS total_students
      FROM student;

`For my own reference`
 - select
	p.postcontent ,
	count(l.postid)
from
	posts p
left join likes l on
	p.postid = l.postid
group by
	l.postid,
	p.postcontent
having
	count(p.postid)=(
	select
		max(counts) as max_col
	from
		(
		select
			count(l.postid) as counts
		from
			posts p
		left join likes l on
			p.postid = l.postid
		group by
			l.postid ) as maxresult)