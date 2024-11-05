# Trigger

## 1 Create table
```
CREATE TABLE customerinfo (
    ID NUMBER PRIMARY KEY,
    Name VARCHAR2(100),
    Address VARCHAR2(255),
    Salary NUMBER
);
```
Table created.

## 2 Creating Trigger
```
CREATE OR REPLACE TRIGGER display_salary_changes
BEFORE DELETE OR INSERT OR UPDATE ON customerinfo
FOR EACH ROW
WHEN (NEW.ID > 0)
DECLARE
    sal_diff NUMBER;
BEGIN
    sal_diff := :NEW.salary - :OLD.salary;

    dbms_output.put_line('Old salary: ' || :OLD.salary);
    dbms_output.put_line('New salary: ' || :NEW.salary);
    dbms_output.put_line('Salary difference: ' || sal_diff);
END;
/
```
Trigger created.

## 3 Insert Query

```
INSERT INTO customerinfo (ID, Name, Address, Salary) VALUES (1, 'John Doe', '123 Elm Street', 50000);
```
1 row(s) inserted.
Old salary: 
New salary: 50000
Salary difference: 

## 4 Update Query
```
UPDATE customerinfo SET Salary = Salary + 500 WHERE ID = 1;
```
1 row(s) updated.
Old salary: 50000
New salary: 50500
Salary difference: 500

# End of the program

