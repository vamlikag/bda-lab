```
create keyspace Employee with replication = { 
   ... 'class':'SimpleStrategy',
   ... 'replication_factor':1
   ... };
```

```
use Employee;
```

```
create table EmployeeInfo (
            ... EmplID int PRIMARY KEY,
            ... EmplName text, 
            ... Designation text, 
            ... DateOfJoining timestamp, 
            ... Salary int,
            ... DeptName text
            ... );
```

```
begin batch
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (101, 'employee1', 'designation1', '2020-03-29', 40000, 'dept1')
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (102, 'employee2', 'designation2', '2020-06-04', 60000, 'dept1')
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (103, 'employee3', 'designation3', '2020-04-21', 75000, 'dept1')
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (104, 'employee4', 'designation4', '2020-12-02', 90000, 'dept2')
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (105, 'employee5', 'designation5', '2020-09-11', 15000, 'dept2')
apply batch;
```

```
emplid | dateofjoining                   | deptname | designation  | emplname  | salary
--------+---------------------------------+----------+--------------+-----------+--------
    105 | 2020-09-10 18:30:00.000000+0000 |    dept2 | designation5 | employee5 |  15000
    104 | 2020-12-01 18:30:00.000000+0000 |    dept2 | designation4 | employee4 |  90000
    102 | 2020-06-03 18:30:00.000000+0000 |    dept1 | designation2 | employee2 |  60000
    101 | 2020-03-28 18:30:00.000000+0000 |    dept1 | designation1 | employee1 |  40000
    103 | 2020-04-20 18:30:00.000000+0000 |    dept1 | designation3 | employee3 |  75000
```

```
insert into EmployeeInfo (EmplID, EmplName, Designation, DateOfJoining, Salary, DeptName) values (121, 'employee6', 'designation6', '2020-10-18', 45000, 'dept1');
```

```
select * from EmployeeInfo;
```

```
emplid | dateofjoining                   | deptname | designation  | emplname  | salary
--------+---------------------------------+----------+--------------+-----------+--------
    105 | 2020-09-10 18:30:00.000000+0000 |    dept2 | designation5 | employee5 |  15000
    121 | 2020-10-17 18:30:00.000000+0000 |    dept1 | designation6 | employee6 |  45000
    104 | 2020-12-01 18:30:00.000000+0000 |    dept2 | designation4 | employee4 |  90000
    102 | 2020-06-03 18:30:00.000000+0000 |    dept1 | designation2 | employee2 |  60000
    101 | 2020-03-28 18:30:00.000000+0000 |    dept1 | designation1 | employee1 |  40000
    103 | 2020-04-20 18:30:00.000000+0000 |    dept1 | designation3 | employee3 |  75000
```

```
update EmployeeInfo SET EmplName='employee7', DeptName='dept2' where EmplID=121;
```

```
select * from EmployeeInfo;
```

```
emplid | dateofjoining                   | deptname | designation  | emplname  | salary
--------+---------------------------------+----------+--------------+-----------+--------
    105 | 2020-09-10 18:30:00.000000+0000 |    dept2 | designation5 | employee5 |  15000
    121 | 2020-10-17 18:30:00.000000+0000 |    dept2 | designation6 | employee7 |  45000
    104 | 2020-12-01 18:30:00.000000+0000 |    dept2 | designation4 | employee4 |  90000
    102 | 2020-06-03 18:30:00.000000+0000 |    dept1 | designation2 | employee2 |  60000
    101 | 2020-03-28 18:30:00.000000+0000 |    dept1 | designation1 | employee1 |  40000
    103 | 2020-04-20 18:30:00.000000+0000 |    dept1 | designation3 | employee3 |  75000
```

```
alter table EmployeeInfo add Projects text;
```

```
select * from EmployeeInfo;
```

```
emplid | dateofjoining                   | deptname | designation  | emplname  | projects | salary
--------+---------------------------------+----------+--------------+-----------+----------+--------
    105 | 2020-09-10 18:30:00.000000+0000 |    dept2 | designation5 | employee5 |     null |  15000
    121 | 2020-10-17 18:30:00.000000+0000 |    dept2 | designation6 | employee7 |     null |  45000
    104 | 2020-12-01 18:30:00.000000+0000 |    dept2 | designation4 | employee4 |     null |  90000
    102 | 2020-06-03 18:30:00.000000+0000 |    dept1 | designation2 | employee2 |     null |  60000
    101 | 2020-03-28 18:30:00.000000+0000 |    dept1 | designation1 | employee1 |     null |  40000
    103 | 2020-04-20 18:30:00.000000+0000 |    dept1 | designation3 | employee3 |     null |  75000
```







