## Запросы SELECT с условием WHERE и BEETWEN
### Задача
~~~
Напишите запрос на вывод находящихся в таблице EXAM_MARKS номеров предметов обучения, 
экзамены по которым сдавались между 10 и 20 августа 2010 года.
Решение
~~~
### Решение
~~~
SELECT SUBJ_ID FROM exam_marks
WHERE EXAM_DATE BETWEEN TO_DATE ('10.08.10', 'dd.mm.yy') 
AND TO_DATE ('20.08.10', 'dd.mm.yy');
~~~~

### Результат

|SUBJ_ID|
|-------|
|1|
|8|



### Задача
~~~
Напишите запрос, выводящий идентификаторы всех студентов, родившихся летом 1980 года и проживающих в Красноярске.
~~~
### Решение
~~~
SELECT STUDENT_ID FROM STUDENT
WHERE BIRTHDAY BETWEEN TO_DATE('1980-06-01', 'YYYY-MM-DD') 
AND TO_DATE('1980-08-31', 'YYYY-MM-DD')
AND CITY='Красноярск';
~~~~
### Результат
|STUDENT_ID|
|----------|
|4|

## Запросы SELECT с объединением нескольких таблиц JOIN

### Задача 
~~~~
Напишите запрос, который позволяет вывести имена и идентификаторы всех студентов, 
для которых точно известно, что они проживают в городе, где нет ни одного университета.
~~~~

### Решение
~~~~
select s.name, s.student_id
from student s
left join university u on s.city = u.city
where u.city is null;
~~~~

### Результат

|NAME|STUDENT_ID|
|----|----------|
|Владимир|16|
|Андрей|17|
|Виталий|34|
|Константин|50|
|Александр|72|
|Кирилл|74|
|Виталий|46|
|Татьяна|54|
|Николай|45|

### Задача
~~~~
Напишите запрос на выдачу для каждого студента, 
с указанием фамилии и имени, названий всех предметов обучения, по которым этот студент получил оценку 4 или 5
~~~~

### Решение
~~~~
select t1.surname, t1.name,t3.subj_name 
from student t1
full join exam_marks t2 on t1.student_id = t2.student_id
full join subject t3 on t2.SUBJ_ID = t3.SUBJ_ID
where t2.MARK>3;
~~~~

### Результат

|SURNAME|NAME|SUBJ_NAME|
|-------|----|---------|
|Стечкин|Евгений|Основы теория права|
|Ольховский|Анатолий|Основы теория права|
|Закомолкин|Дмитрий|Основы теория права|
|Григорьев|Антон|Экология|
|Кислицын|Алексей|Экология|
|Строков|Антон|Экология|
|Щеглов|Александр|Экология|
|Стерногин|Анатолий|Философия|
|Закомолкин|Дмитрий|Философия|
|Забитов|Станислав|Философия|
