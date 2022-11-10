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

### Task 2.2: SQL injection attack from command line

- This is a slight variation of the last task, just change the special characters to the  equivalent HTTP enconding (admin%27%3B%23), once again leaving the password field empty as we dont actually need it for this attack.

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img3.PNG "Title")

 - We get returned the html code of the page.

 - For curiosity´s sake, inserting this link in a browser has the same effects as doing the attack on the previous task

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log8img4.PNG "Title")