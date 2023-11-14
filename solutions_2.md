## Soluzioni

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia 

        SELECT 
            `degrees`.`name`,     
            `students`.`name`,      
            `students`.`surname`,     
            `students`.`registration_number`,     
            `students`.`enrolment_date`     
        FROM `degrees`      
        INNER JOIN `students`     
        ON `degrees`.`id` = `students`.`degree_id`      
        WHERE `degrees`.`name` = 'Corso di Laurea in Economia'      

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze 

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


