# PL/SQL

<a href='https://www.oracle.com/database/technologies/appdev/plsql.html' target='_blank'>Link to Oracle</a>

<a href='https://www.tutorialspoint.com/plsql' target='_blank'>Link to tutorials Point</a>   

1. Blocks 
      
            DECLARE 
                Variable declaration
            BEGIN 
                Program Execution 
            EXCEPTION 
                Exception handling
            END;


2. Variable Scope  

            Local variables − declared in an inner block and not accessible to outer blocks

            Global variables − declared in the outermost block or a package
            
            DECLARE 
               -- Global variables  
               num1 number := 95;  
               num2 number := 85;  
            BEGIN  
               dbms_output.put_line('Outer Variable num1: ' || num1); 
               dbms_output.put_line('Outer Variable num2: ' || num2); 
               DECLARE  
                  -- Local variables 
                  num1 number := 195;  
                  num2 number := 185;  
               BEGIN  
                  dbms_output.put_line('Inner Variable num1: ' || num1); 
                  dbms_output.put_line('Inner Variable num2: ' || num2); 
               END;  
            END; 
            / 
