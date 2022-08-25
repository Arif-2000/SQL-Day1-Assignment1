# SQL-Day1-Assignment1

create table Clients
(
Client_id numeric(4) primary key,
Cname varchar(40) NOT NULL,
Addres varchar(30),
Email varchar(30) unique,
Phone numeric(10),
Business varchar(20) NOT NULL
)
insert into Clients(Client_id,Cname,Addres,Email,Phone,Business) values
(1002,'Trackon Consultants','Mumbai','consult@trackon.com',8734210090,'Consultant'),
(1003,'MoneySaver Distributors','Kolkata','save@moneysaver.com',7799886655,'Reseller'),
(1004,'Lawful Corp','Chennai','justice@lawful.com',9210342219,'Professional')


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
create table Departments
(
Deptno numeric(2) primary key,
Dname varchar(15) NOT NULL,
Loc varchar(20)
)

insert into Departments(Deptno,Dname,Loc) values(10,'Design','Pune'),
(20,'Development','Pune'),
(30,'Testing','Mumbai'),
(40,'Document','Mumbai')

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

create table Employees
(
Empno numeric(4) primary key,
Ename varchar(20) NOT NULL,
Job varchar(15),
Salary numeric(7) constraint positive check(Salary>0),
Deptno numeric(2) references Departments(Deptno)
)

insert into Employees(Empno,Ename,Job,Salary,Deptno) values(7001,'Sandeep','Analyst',25000,10),
(7002,'Rajesh','Designer',30000,10),
(7003,'Mahadev','Developer',40000,20),
(7004,'Manoj','Developer',40000,20),
(7005,'Abhay','Designer',35000,10),
(7006,'Uma','Tester',30000,30),
(7007,'Gita','Tech. Writer',30000,40),
(7008,'Priya','Tester',35000,30),
(7009,'Nutan','Developer',45000,20),
(7010,'Smita','Analyst',20000,10),
(7011,'Anand','Project Mgr.',65000,10)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------

create table Projects
(
Project_ID numeric(3) primary key,
Descr varchar(30) NOT NULL,
Start_Date DATE,
Planned_End_Date DATE,
Actual_End_Date DATE,
Budget numeric(10) constraint positivebug check(Budget>0),
Client_id numeric(4) references Clients(Client_id)
)
alter table Projects
add constraint dateChk check(Actual_End_Date > Planned_End_Date)

insert into Projects(Project_ID,Descr,Start_Date,Planned_End_Date,Actual_End_Date,Budget,Client_id) values(401,'Inventory','01-APR-11','01-OCT-11','31-OCT-11',150000,1001),
(402,'Accounting','01-AUG-11','01-JAN-12',null,500000,1002),
(403,'Payroll','01-OCT-11','31-DEC-11','null',750000,1003),
(404,'Contact Mgmt','01-NOV-11','31-DEC-11','null',50000,1004)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------

create table EmpProjectTasks
(
Project_ID numeric(3) references Projects(Project_ID),
Empno numeric(4) references Employees(Empno),
Start_Date DATE,
End_Date DATE,
Task varchar(25) NOT NULL,
Status varchar(15) NOT NULL,
primary key(Project_ID,Empno)
)

insert into EmpProjectTasks(Project_ID,Empno,Start_Date,End_Date,Task,Status) values(401,7001,'01-APR-11','20-APR-11','System Analysis','Completed'),
(401,7002,'21-APR-11','30-MAY-11','System Design','Completed'),
(401,7003,'01-JUN-11','15-JUL-11','Coding','Completed'),
(401,7004,'18-JUL-11','1-SEP-11','Coding','Completed'),
(401,7006,'03-sep-11','15-sep-11','Testing','Completed'),
(401,7009,'18-sep-11','05-oct-11','Code Change','Completed'),
(401,7008,'06-oct-11','16-oct-11','Testing','Completed'),
(401,7007,'06-oct-11','22-oct-11','Documentation','Completed'),
(401,7011,'22-oct-11','31-oct-11','Sign off','Completed'),
(401,7010,'01-aug-11','20-aug-11','System Analysis','Completed'),
(401,7002,'22-aug-11','30-sep-11','System Design','Completed'),
(401,7004,'01-oct-11','null','Coding','In Progress')

