# SQL INJECTION

## Task 1: Get familiar with SQL statements

- In the first task we want to get all the information associated with the employee "Alice"

-The only info needed is the name of the table and the name of the column where employee names are stored

- The name of the table is found by using "show tables;" and the name of the column can be seen on the guide

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img1.PNG "Title")

- Here we have all the info for "Alice"

## Task 2: SQL injection attack on SELECT statement

### Task 2.1: SQL injection attack from webpage

 - Since the WHERE statement is all inline we can avoid the password clause by ending the line early by appending to a valid username ';#, like seen in the screenshot below.

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img2.PNG "Title")

 - The password field can be left empty as the web application doesn't check if it contains any info, but even if it did, the data entered in the password field would not be processed anyways.

### Alternative method

 - Besides the attack where we comment out the rest of the line we were also able to login with any account while only knowing its username with the following method.

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img5.PNG "Title")

 This works because it adds and OR clause together with a TRUE statement, which also makes it skip the password clause.

### Task 2.2: SQL injection attack from command line

- This is a slight variation of the last task, just change the special characters to the  equivalent HTTP enconding (admin%27%3B%23), once again leaving the password field empty as we dont actually need it for this attack.

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img3.PNG "Title")

 - We get returned the html code of the page.

 - For curiosity´s sake, inserting this link in a browser has the same effects as doing the attack on the previous task

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img4.PNG "Title")

### Task 2.3: Append a new SQL statement

- For this task we tried to use the login page to inject a completely new SQL statement to try to delete or insert something in the database.

- After multiple failed attempts or trying both INSERT and DELETE statements, we got no sucess so by trying to search the web for any information on this we found that the MySQL server is configured to not allow multi-queries, so this attack seems impossible.


### Task 3.1: Modify your own salary

- After inspecting the SQL statement it seems fairly easy to change the salary since its a column on the same table, just add the statement for the row on one of the fields, we can do this by inserting in the nickname field, for example "Alice', salary = '40000" without the double quotes, as seen below.

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img6.PNG "Title")

- After pressing save on the site we can see that it worked.

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img7.PNG "Title")


### Task 3.2: Modify other people´s salary

- Next we are given the task of modifying a different user´s salary, and in the meantime, we also changed his Nickname.

- The principles are the same, except now we end with a WHERE clause, and since we already know the target´s name, we use the following statement "Worst Boss Ever', salary = 1 WHERE name ='Boby';#", as can be seen below

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img8.PNG "Title")

- Next we login to the admin´s account with one of the vulnerabilites found in task 2 to see if it took effect and we see the following

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img9.PNG "Title")
