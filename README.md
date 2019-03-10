# PL/SQL

Procedural Language SQL


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

2. Variables

           - Substitution variable : used to accept input from a user  
                        ACCEPT p_name PROMPT ’Enter Name: ’
           - Bind variable
                        -- declare an SQLplus bind variable
                        VARIABLE g_name VARCHAR2(30)
                        BEGIN
                        -- assign value of substitution variable to the bind variable
                           :g_name := '&p_name';
                        END;
                        /
                        PRINT g_name
           - PL variable
                        DECLARE
                           v_name VARCHAR2(20);
3. Variable Scope  

            - Local variables − declared in an inner block and not accessible to outer blocks

            - Global variables − declared in the outermost block or a package
            
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

3. Variable Types with SQL statement

            - automatic type from custname's type of customer table
                  DECLARE
                  v_name customer.custname%TYPE;

            - with whole columns of table
                  DECLARE
                  v_customer customer%ROWTYPE;
                  
            - by defining type
                  DECLARE
                      TYPE cust_record IS RECORD
                      (custname VARCHAR2(20), 
                      custphone CHAR(13),
                      custaddress CHAR(100));
                      r_customer cust_record;


4. Example - to display customer's information
            
            - Prompt for the name a customer and display his/her address using simple variables
            
            SET SERVEROUTPUT ON;
            
            ACCEPT p_name PROMPT 'Enter Customer Name: '
           
            DECLARE
                v_customer customer%ROWTYPE;
           
            BEGIN
               SELECT *
               INTO v_customer
               FROM customer
               WHERE UPPER(custname) = UPPER('&p_name');
               DBMS_OUTPUT.PUT_LINE('&p_name' || CHR(10) || v_customer.custstreet || CHR(10) 
               || RTRIM(v_customer.custcity) || ', ' || v_customer.custprovince || CHR(10) || v_customer.custpostal
               );
            END;
            /
