# pl/sql: cursor

## 1 Create Table
```
CREATE TABLE customerinfo (
    customer_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    salary NUMBER(10, 2)
);
```
Table created.

## 2 Insert Value in table
```
INSERT INTO customerinfo (customer_id, customer_name, salary)
VALUES (1, 'John Doe', 5000);

INSERT INTO customerinfo (customer_id, customer_name, salary)
VALUES (2, 'Jane Smith', 5500);

INSERT INTO customerinfo (customer_id, customer_name, salary)
VALUES (3, 'Michael Johnson', 6000);

INSERT INTO customerinfo (customer_id, customer_name, salary)
VALUES (4, 'Emily Davis', 6200);
```
1 row(s) inserted.

1 row(s) inserted.

1 row(s) inserted.

1 row(s) inserted.
## 3 Check Column values
```
select * from customerinfo;
```
```
customer_id	customer_name	    salary
1	            john Doe	     5000
2	            Jane Smith	     5500
3	            Michael Johnson	 6000
4	            Emily Davis	     6200
```
##  4 Increase salary 100 every customer

Enable Server Output
Once logged in, enable server output by running:
```
SET SERVEROUTPUT ON;
```
```
DECLARE
    total_rows NUMBER(2);
BEGIN
    UPDATE customerinfo
    SET salary = salary + 100;

    IF SQL%NOTFOUND THEN
        dbms_output.put_line('No customers selected');
    ELSIF SQL%FOUND THEN
        total_rows := SQL%ROWCOUNT;
        dbms_output.put_line(total_rows || ' customers selected');
    END IF;
END;
/
```
4 customers selected
## 5 Check Column value
```
select * from customerinfo;
```
output
```
CUSTOMER_ID	CUSTOMER_NAME	    SALARY
1	             john Doe	      5100
2	             Jane Smith	      5600
3	             Michael Johnson  6100
4	             Emily Davis	  6300
```

Enable Server Output
Once logged in, enable server output by running:
```
SET SERVEROUTPUT ON;
```
## This program essentially retrieves and displays all customers' IDs and names from the customer table.
```
DECLARE
    CURSOR customer_cur IS
        SELECT CUSTOMER_ID, CUSTOMER_NAME FROM customerinfo;

    customer_rec customer_cur%ROWTYPE;
BEGIN
    OPEN customer_cur;

    LOOP
        FETCH customer_cur INTO customer_rec;
        EXIT WHEN customer_cur%NOTFOUND;
        
        DBMS_OUTPUT.put_line(customer_rec.CUSTOMER_ID || ' ' || customer_rec.CUSTOMER_NAME);
    END LOOP;
```
1 John Doe
2 Jane Smith
3 Michael Johnson
4 Emily Davis

# End of the program
