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
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.
