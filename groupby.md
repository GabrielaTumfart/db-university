1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT YEAR(enrolment_date) AS anno, COUNT(*) AS total_iscritti
FROM university.students
GROUP BY YEAR(enrolment_date);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT office_address, COUNT(*) AS total_insegnanti
FROM university.teachers
GROUP BY office_address;
```

3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT exam_id, AVG(vote) AS media_voti
FROM university.exam_student
GROUP BY exam_id;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT departments.name, COUNT(*) AS total_corsi_di_laurea
FROM university.departments
INNER JOIN university.degrees
ON departments.id = degrees.department_id
GROUP BY departments.id;
```
