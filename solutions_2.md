## Soluzioni

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia    
RESULT: 68

        SELECT 
          `degrees`.`name`,     
          `students`.`name`,      
          `students`.`surname`,     
          `students`.`registration_number`,     
          `students`.`enrolment_date`     
        FROM 
          `degrees`      
        INNER JOIN 
          `students`     
        ON 
          `degrees`.`id` = `students`.`degree_id`      
        WHERE 
          `degrees`.`name` = 'Corso di Laurea in Economia'      

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze    
RESULT: 1    

        SELECT    
          `departments`.`name`,   
          `degrees`.*   
        FROM    
          `departments`   
        INNER JOIN    
          `degrees`   
        ON    
          `departments`.`id` = `degrees`.`department_id`    
        WHERE     
          `departments`.`name` = 'Dipartimento di Neuroscienze'   
        AND   
          `degrees`.`level` = 'magistrale';   
            
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)  
RESULT: 11

        SELECT    
          `teachers`.`name`,    
          `teachers`.`surname`,   
          `courses`.*   
        FROM    
          `teachers`    
        INNER JOIN    
          `course_teacher`    
        ON    
          `teachers`.`id` = `course_teacher`.`teacher_id`   
        INNER JOIN    
          `courses`   
        ON    
          `course_teacher`.`course_id` = `courses`.`id`   
        WHERE   
          `teachers`.`name` = 'Fulvio'    
        AND   
          `teachers`.`surname` = 'Amato'    

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

        SELECT    
          `students`.`surname`,   
          `students`.`name`,    
          `degrees`.`name`,   
          `degrees`.`level`,      
          `departments`.`name`     
        FROM    
          `students`    
        INNER JOIN    
          `degrees`   
        ON    
          `students`.`degree_id` = `degrees`.`id`   
        INNER JOIN    
          `departments`   
        ON    
          `degrees`.`department_id` = `departments`.`id`    
        ORDER BY    
          `students`.`surname`,   
          `students`.`name`;    

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti    
RESULT: 1317 

        SELECT    
          `degrees`.`name` AS `degree_name`,    
          `degrees`.`level`,    
          `courses`.`year`,   
          `courses`.`period`,   
          `courses`.`name` AS `course_name`,    
          `teachers`.`surname` AS `teacher_surname`,	    
          `teachers`.`name` AS `teacher_name`   
        FROM    
          `degrees`   
        INNER JOIN    
          `courses`   
        ON    
          `degrees`.`id` = `courses`.`degree_id`    
        INNER JOIN    
          `course_teacher`    
        ON    
          `courses`.`id` = `course_teacher`.`course_id`   
        INNER JOIN    
          `teachers`    
        ON    
          `course_teacher`.`teacher_id` = `teachers`.`id`   
        ORDER BY    
          `degrees`.`name`    

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)  
RESULT: 70 (senza distinct)    
RESULT: 54    

        SELECT DISTINCT  
          `departments`.`name`,   
          `teachers`.`surname`,   
          `teachers`.`name`   
        FROM    
          `departments`   
        INNER JOIN    
          `degrees`   
        ON    
          `departments`.`id` = `degrees`.`department_id`    
        INNER JOIN    
          `courses`   
        ON    
          `degrees`.`id` = `courses`.`degree_id`    
        INNER JOIN    
          `course_teacher`    
        ON    
          `courses`.`id` = `course_teacher`.`course_id`   
        INNER JOIN    
          `teachers`    
        ON    
          `course_teacher`.`teacher_id` = `teachers`.`id`   
        WHERE   
          `departments`.`name` = 'Dipartimento di Matematica';  

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.      

        SELECT    
          `students`.`surname` AS `cognome`,    
            `students`.`name` AS `nome`,    
            MAX(`exam_student`.`vote`) AS `voto_piu_alto`,    
            COUNT(`exam_student`.`exam_id`) AS `esami_sostenuti`,   
            AVG(`exam_student`.`vote`) AS `media_voti`    
        FROM    
          `students`    
        INNER JOIN    
          `exam_student`    
        ON    
          `exam_student`.`student_id` = `students`.`id`   
        WHERE     
          `exam_student`.`vote` >= 18   
        GROUP BY    
          `exam_student`.`student_id`     
        ORDER BY    
          `cognome`, `nome`   
