# Ex. No: 6 Creating Cursors using PL/SQL
### DATE: 07.09.2023
### AIM: 

To create a cursor using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create a cursor named as employee_cursor
3. Using cursor read each record and display the result
4. Close the cursor

### Program:
### Create employee table
#### Query:
```
CREATE TABLE employee (empid INT PRIMARY KEY,empname VARCHAR(10),dept VARCHAR(10),salary DECIMAL(10, 2));

insert into employee values (1,'Abi','HR',35000);
insert into employee values (2,'Divya','TL',25000);

select * from employee;
select * from employee;
```
#### Table:
![1](https://github.com/Divya110205/Ex-no-6-Creating-Cursors-using-PL-SQL/assets/119404855/bd20c556-76b2-471f-91ee-858ece41df24)

### PLSQL Cursor code
```
DELIMITER //

CREATE PROCEDURE fetch_employee_data()
BEGIN
  DECLARE v_empid INT;
  DECLARE v_empname VARCHAR(10);
  DECLARE v_dept VARCHAR(10);
  DECLARE v_salary DECIMAL(10, 2);
  
  DECLARE employee_cursor CURSOR FOR SELECT empid, empname, dept, salary FROM employee;
  
  DECLARE CONTINUE HANDLER FOR NOT FOUND SET @finished = 1;
  
  OPEN employee_cursor;
  
  SET @finished = 0;
  
  FETCH_NEXT: LOOP
    FETCH employee_cursor INTO v_empid, v_empname, v_dept, v_salary;
    IF @finished = 1 THEN
      LEAVE FETCH_NEXT; -- Exit the loop when no more rows
    END IF;

    SELECT v_empid, v_empname, v_dept, v_salary;
  END LOOP FETCH_NEXT;
  
 
  CLOSE employee_cursor;
END //

DELIMITER ;

CALL fetch_employee_data();
```
### Output:
![2](https://github.com/Divya110205/Ex-no-6-Creating-Cursors-using-PL-SQL/assets/119404855/62e01ed8-6b5d-4da3-8cf6-ee5a3ef09e21)

### Result:
The program is implemented successfully.
