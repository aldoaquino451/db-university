## Soluzioni

### Query con SELECT

- SELECT *        
  FROM `students`             
  WHERE `date_of_birth` LIKE '1990%'        

- SELECT *        
  FROM `courses`          
  WHERE `cfu`> 10   

- SELECT *        
  FROM `students`       
  WHERE `date_of_birth` < '1993-11-13'  

- SELECT *    
  FROM `courses`    
  WHERE period = 'I semestre' AND year = 1  

- SELECT *    
  FROM `exams`    
  WHERE `hour` > '14:00:00' AND `date` = '2020-06-20'  

- SELECT *    
  FROM `degrees`      
  WHERE level = 'magistrale';

- SELECT COUNT(*) AS `numero_dipartimenti`    
  FROM `departments`;   
  
- SELECT COUNT(*) AS `insegnanti_senza_cellulare`   
  FROM `teachers`   
  WHERE `phone` IS null;



### Query con GROUP BY

- SELECT COUNT(*) AS `studenti_iscritti`, YEAR(`enrolment_date`) AS `anno_di_iscrizione`    
  FROM `students`   
  GROUP BY `anno_di_iscrizione`;

- SELECT `office_number` AS `numero_ufficio`, COUNT(id) AS `insegnanti_per_ufficio`   
  FROM `teachers`   
  GROUP BY `numero_ufficio`;

- SELECT `exam_id` AS `appello`, AVG(`vote`) AS `voto_medio`    
  FROM `exam_student`   
  GROUP BY `appello`;

- SELECT `department_id` AS `dipartimento`, COUNT(`name`) AS `numero_corsi`     
  FROM `degrees`    
  GROUP BY `dipartimento`;




