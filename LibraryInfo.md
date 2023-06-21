```
create keyspace libInfo with replication = {
   ... 'class':'SimpleStrategy',
   ... 'replication_factor':1
   ... };
```

```
use libInfo;
```

```
create table libInfo (
           ... studID int,
           ... studName text,
           ... bookID int,
           ... bookName text,
           ... dateOfIssue timestamp,
           ... counterValue counter,
           ... primary key ((studID, bookID), studName, bookName, dateOfIssue)
           ... );
```

**Inserting values in the table**

```
update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 001 and studName = 'Raj' and bookID = 101 and bookName = 'The Midnight Library' and dateOfIssue = '2023-05-08';
           
update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 002 and studName = 'Krishna' and bookID = 102 and bookName = 'The Little Coffee Shop of Kabul' and dateOfIssue = '2023-03-07';
           
update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 003 and studName = 'Trupti' and bookID = 103 and bookName = 'Tokyo Ueno Station' and dateOfIssue = '2022-12-26';

update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 004 and studName = 'Arya' and bookID = 104 and bookName = 'A Thousand Splendid Suns' and dateOfIssue = '2022-10-03';
           
update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 005 and studName = 'Karan' and bookID = 105 and bookName = 'Portrait of an Unknown Woman' and dateOfIssue = '2023-01-28';
```

```
select * from libInfo;
```

```
 studid | bookid | studname | bookname                        | dateofissue                     | countervalue
--------+--------+----------+---------------------------------+---------------------------------+--------------
      1 |    101 |      Raj |            The Midnight Library | 2023-05-07 18:30:00.000000+0000 |            1
      3 |    103 |   Trupti |              Tokyo Ueno Station | 2022-12-25 18:30:00.000000+0000 |            1
      2 |    102 |  Krishna | The Little Coffee Shop of Kabul | 2023-03-06 18:30:00.000000+0000 |            1
      5 |    105 |    Karan |    Portrait of an Unknown Woman | 2023-01-27 18:30:00.000000+0000 |            1
      4 |    104 |     Arya |        A Thousand Splendid Suns | 2022-10-02 18:30:00.000000+0000 |            1
```

```
update libInfo
           ... set counterValue=counterValue+1
           ... where studID = 005 and studName = 'Karan' and bookID = 105 and bookName = 'Portrait of an Unknown Woman' and dateOfIssue = '2023-01-28';
```

```
select * from libInfo;
```

```
 studid | bookid | studname | bookname                        | dateofissue                     | countervalue
--------+--------+----------+---------------------------------+---------------------------------+--------------
      1 |    101 |      Raj |            The Midnight Library | 2023-05-07 18:30:00.000000+0000 |            1
      3 |    103 |   Trupti |              Tokyo Ueno Station | 2022-12-25 18:30:00.000000+0000 |            1
      2 |    102 |  Krishna | The Little Coffee Shop of Kabul | 2023-03-06 18:30:00.000000+0000 |            1
      5 |    105 |    Karan |    Portrait of an Unknown Woman | 2023-01-27 18:30:00.000000+0000 |            2
      4 |    104 |     Arya |        A Thousand Splendid Suns | 2022-10-02 18:30:00.000000+0000 |            1
```

```
select studID from libInfo where bookName = 'Portrait of an Unknown Woman' and counterValue = 2 allow filtering;
```

```
 studid
--------
      5
```

**Exporting table into a CSV file**

```
copy libInfo(studID, studName, bookID, bookName, dateOfIssue, counterValue) to 'c:\libInfo.csv';
Using 3 child processes

Starting copy of libinfo.libinfo with columns [studid, studname, bookid, bookname, dateofissue, countervalue].
Processed: 5 rows; Rate:       2 rows/s; Avg. rate:       1 rows/s
5 rows exported to 1 files in 9.163 seconds.
```

**Deleting the values in the table**

```
truncate libInfo;
select * from libInfo;

 studid | bookid | studname | bookname | dateofissue | countervalue
--------+--------+----------+----------+-------------+--------------

(0 rows)
```

**Importing a CSV into the table**

```
copy libInfo(studID, studName, bookID, bookName, dateOfIssue, counterValue) from 'c:\libInfo.csv' with header = true;
Using 3 child processes

 studid | bookid | studname | bookname                        | dateofissue                     | countervalue
--------+--------+----------+---------------------------------+---------------------------------+--------------
      1 |    101 |      Raj |            The Midnight Library | 2023-05-07 18:30:00.000000+0000 |            1
      3 |    103 |   Trupti |              Tokyo Ueno Station | 2022-12-25 18:30:00.000000+0000 |            1
      2 |    102 |  Krishna | The Little Coffee Shop of Kabul | 2023-03-06 18:30:00.000000+0000 |            1
      5 |    105 |    Karan |    Portrait of an Unknown Woman | 2023-01-27 18:30:00.000000+0000 |            2
      4 |    104 |     Arya |        A Thousand Splendid Suns | 2022-10-02 18:30:00.000000+0000 |            1
```
