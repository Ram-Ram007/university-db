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

