drop table if exists class_attendance;
drop table if exists classes;
drop table if exists students;
drop table if exists mentors;

create table if not exists mentors (
id SERIAL primary key,
name VARCHAR(50) not null,
years_glasgow smallint not null,
address VARCHAR(20),
favourite_PL VARCHAR (30)
);

insert into mentors (name, years_glasgow, address, favourite_PL)
values ('Marco',3,'Barcelona','SQL'),
('Camila', 2, 'Barcelona', 'JS'),
('Carlos', 3, 'Barcelona', 'JS'),
('Lucia', 1, 'Barcelona', 'HTML');

create table if not exists students (
	id SERIAL primary key,
	name VARCHAR(30),
	glassgow_living_period VARCHAR(30),
	address VARCHAR(30),
	graduated boolean not null
);

create table if not exists classes (
	id SERIAL primary key,
	mentor_id INT references mentors(id),
	topic VARCHAR(60),
	taught_date DATE not null,
	class_location VARCHAR(60)
);

insert into mentors (name, years_glasgow, address, favourite_pl) values
('John', 5, '11 New Road', 'Javascript');

create table if not exists class_attendance (
id SERIAL primary key,
student_id INT references students (id),
class_id INT references classes (id)
);

insert into students (name, address, graduated) values ('Nuno', '7 New Road', true);
insert into students (name, address, graduated) values ('Danielle', '8 New Road', false);
insert into students (name, address, graduated) values ('Nimra', '9 New Road', true);
insert into students (name, address, graduated) values ('Amanda', '10 New Road', false);
insert into students (name, address, graduated) values ('Yun', '11 New Road', true);
insert into students (name, address, graduated) values ('Mann', '12 New Road', true);

insert into classes (mentor_id, taught_date) values (1, '2022-12-17');
insert into classes (mentor_id, taught_date) values (2, '2022-12-17');
insert into classes (mentor_id, taught_date, topic) values (2, '2022-12-17', 'Javascript');

insert into class_attendance (student_id, class_id) values(1,3);

select * from mentors;
select * from students limit 5;
select * from students where graduated= true limit 3;
select * from students where name like 'M%' limit 2;

select name from class_attendance as ca
join students as s 
on ca.student_id  = s.id
where s.name like 'N%' limit 5;

select s.name from class_attendance as ca
join students as s
on ca.student_id  = s.id
join classes as c 
on c.id = ca.class_id;

select s.name from students as s
join class_attendance as ca
on s.id = ca.student_id 
join classes as c
on c.id = ca.class_id 
where c.taught_date = '2022-12-17'
;

select * from mentors m 
where years > 5;

select * from mentors m 
where m.favourite_pl= 'Javascript'; 

select * from students s 
where graduated = true;


select * from classes;