# MYSQL关于多表查询和子查询的练习(练习5)

- --查询1课程比2课程成绩高的学生的信息及课程分数 

  ```sql
  select*,(select s.score from score s where s.student_id = a.id and s.course_id =1) as 课程1,(select s.score from score s where s.student_id = a.id and s.course_id
   =2) as 课程2 from student a
      -> where (select s.score from score s where s.student_id = a.id and s.course_id =1)>(select s.score from score s where s.student_id = a.id and s.course_id = 2);
  ```

  ![image-20230730173308535](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301733573.png)

- ### -- 查询平均成绩大于等于 60 分的同学的学生编号和学生姓名和平均成绩 

```sql
 select student.id,student.name,avg(score)
    -> from student,score,course,teacher
    -> where student.id=score.student_id and teacher.teacher_id = course.teacher_id and score.course_id = course.course_id
    -> and score >=60 group by student.id,student.name;
```

![image-20230728225207135](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307282252229.png)

-  -- 查询在 score 表存在成绩的学生信息(exist)

- ```sql
  select student.* from student where EXISTS (select score from score where student.id=score.student_id);
  ```

  ![image-20230728231401769](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307282314811.png)

   -- 查询所有同学的学生编号、学生姓名、选课总数、所有课程的总成绩(没成绩的显示为 null ) 

```sql
 SELECT student.id, student.name, COUNT(course.course_id) AS 选课总
数, IFNULL(SUM(score.score), NULL) AS 分数总和 FROM student
 left join score on student.id =score.student_id
 left join course on score.course_id = course.course_id
 LEFT JOIN teacher ON course.teacher_id = teacher.teacher_id  group by student.id,student.name;
```

![image-20230729000401550](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307290004597.png)

- -- 查询学过「老张」老师授课的同学的信息 

```sql
 select student.* from  student
    -> LEFT JOIN score ON student.id = score.student_id
    -> LEFT JOIN course ON score.course_id = course.course_id
    -> LEFT JOIN teacher ON course.teacher_id = teacher.teacher_id
    -> where teacher.teacher_name ='老张';
```

![image-20230729001818453](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307290018491.png)

- -- 查询没有学全所有课程的同学的信息 

  ```sql
  select distinct student.* FROM student  left join score on student.id
    =score.student_id
      -> left join course on score.course_id = course.course_id
      -> left join teacher on teacher.teacher_id = course.teacher_id where student_id in(
      -> select student_id from score group by student_id having count(student_id) =3);
  ```
  
  

![image-20230730134501708](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301345760.png)

- -- 查询至少有一门课与学号为1的同学所学相同的同学的信息()

```sql
select distinct a.* from student a join score s on a.id =s.student_id
    ->  where s.course_id in (select course_id from score where student_id =1);


```

![image-20230730162101982](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301621022.png)

-  -- 查询和2号的同学学习的课程总数完全相同的其他同学的信息(子查询中的命名在其他查询不生效)

```sql
select a.*,(select count(s.course_id) from score s where s.student_id = a.id) as 选修数量 from student a
    -> where (select count(s.course_id) from score s where s.student_id = a.id) = (select count(course_id) from score where student_id =2);
```

![image-20230730170410791](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301704853.png)

-  -- 查询两门及其以上不及格课程的同学的学号，姓名及其平均成绩

```sql
select a.id,a.name,(select count(course_id) from score s where a.id = s.student_id and s.score <60) as 不及格数 from student a
    -> where (select count(course_id) from score s where a.id = s.student_id and s.score< 60) >2 ;
```

![image-20230730171942091](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301719137.png)

- -- 按平均成绩从高到低显示所有学生的所有课程的成绩以及平均成绩(子查询与左连接)

```sql
SELECT a.name, c.course_name, s.score, savg.avg_score AS '平均成绩' FROM student a
    -> left join (select s.student_id,avg(score) as avg_score from score s group by s.student_id)
    -> savg on a.id =savg.student_id
    -> LEFT JOIN score s ON a.id = s.student_id
    -> LEFT JOIN course c ON s.course_id = c.course_id
    -> order by savg.avg_score desc;
```

![image-20230730155947366](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301559439.png)

-  -- 查询男生、女生人数 

```sql
select a.gender,count(a.id)'人数' from student a group by gender;
```

![image-20230730150614678](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301506710.png)

-  -- 查询课程名称为「数学」，且分数低于 60 的学生姓名和分数 

```sql
select a.name,s.score from student a join score s on a.id =s.student_id
    -> join course c on s.course_id = c.course_id
    -> where score<60 and c.course_name = '数学';
```

![image-20230730150403504](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301504537.png)

- -- 查询所有学生的课程及分数情况（存在学生没成绩，没选课的情况）

```sql
select a.name,a.id,s.course_id,s.score from student a
    -> left join score s on a.id =s.student_id;
```

![image-20230730144547629](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301445679.png)

- -- 查询不及格的课程人数 

```sql
select count(s.id),b.course_id  from student s join score b on s.id = b.student_id
where b.score <60 group by b.course_id,b.course_id;
```

![image-20230730143946430](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301439462.png)

- -- 求每门课程的学生人数

-  -- 统计每门课程的学生选修人数（超过 5 人的课程才统计）。

```sql
select count(s.id)'学生数量',b.course_id'课程' from student s join score b on s.id = b.student_id
    -> group by b.course_id having count(s.id) >5;
```

![image-20230730142016175](https://cdn.jsdelivr.net/gh/vegetabledog5058/photo/md/202307301420210.png)
