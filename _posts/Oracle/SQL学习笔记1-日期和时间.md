Title: SQL学习笔记1-日期和时间
Date:
URL: 
Tags: 

一个简单的日期时间策略
```sql
  SELECT ID_KEY                 AS ID_KEY,
    PERSON_NO                   AS PERSON_NO,
--    to_date(sysdate+1,'DD-MON-YY') AS TESTsysdate
  FROM table_name
  WHERE R_DATE < to_date(sysdate+2) AND R_DATE > to_date(sysdate-2);
  ```
- 如果`where`里是+1和-1，就没有数据。需要+/- 2才行
- `to_date(sysdate+1,'DD-MON-YY') AS TESTsysdate`，出来的是当前的日期，假设今天是4号
- 那么分别会显示3号和5号的数据
