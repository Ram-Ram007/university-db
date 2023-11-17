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
	