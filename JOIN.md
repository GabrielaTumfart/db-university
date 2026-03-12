1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT students.*
FROM university.students
INNER JOIN university.degrees
ON students.degree_id = degrees.id
WHERE degrees.name = "Economia";
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT degrees.*
FROM university.degrees
INNER JOIN university.departments
ON degrees.department_id = departments.id
WHERE degrees.level = "magistrale" AND
	  departments.name = "Dipartimento di Neuroscienze";
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT courses.*
FROM university.courses
INNER JOIN university.course_teacher
ON courses.id = course_teacher.course_id
WHERE course_teacher.teacher_id = 44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT students.*, degrees.*, departments.*
FROM university.students
INNER JOIN university.degrees
ON students.degree_id = degrees.id
INNER JOIN university.departments
ON degrees.department_id = departments.id
ORDER BY students.surname, students.name;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT degrees.*, courses.*, teachers.*
FROM university.degrees
INNER JOIN university.courses
ON degrees.id = courses.degree_id
INNER JOIN university.course_teacher
ON courses.id = course_teacher.course_id
INNER JOIN university.teachers
ON course_teacher.teacher_id = teachers.id;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT teachers.*
FROM university.teachers
INNER JOIN university.course_teacher
ON teachers.id = course_teacher.teacher_id
INNER JOIN university.courses
ON course_teacher.course_id = courses.id
INNER JOIN university.degrees
ON courses.degree_id = degrees.id
INNER JOIN university.departments
ON degrees.department_id = departments.id
WHERE departments.name = "Dipartimento di Matematica";
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql
SELECT students.id, students.name, students.surname,
       courses.name AS corso,
       COUNT(*) AS tentativi,
       MAX(exam_student.vote) AS voto_massimo
FROM university.students
INNER JOIN university.exam_student
ON students.id = exam_student.student_id
INNER JOIN university.exams
ON exam_student.exam_id = exams.id
INNER JOIN university.courses
ON exams.course_id = courses.id
GROUP BY students.id, courses.id
HAVING MAX(exam_student.vote) >= 18;
```
