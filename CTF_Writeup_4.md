### Challenge 1: Login as admin on web server

- We are tasked with logging in as an admin on the [server](http://ctf-fsi.fe.up.pt:5003/)

- We use the technique we learned on LOGBOOK8 and write "admin';#" on the username field and random characters on the password field

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf4img1.PNG "Title")

- And we sucessfully login as an admin and obtain the flag

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf4img2.PNG "Title")

### Challenge 2

Checksec:

- The execution of checksec in the executable shows that PIE is enable and NX is disable. 

- PIE (Position-independent code) is a countermeasure against buffer exploitation that allows code to execute in a random address in memory in each execution. Therefore, the fact that the PIE is enable makes the attack more challenging since it makes it more difficult to predict where the code will be placed and, consequently, the value of the memory addresses.

- NX is disabled, this means writable memory can also be executed.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf4img5.png "Title")

Question 1:
"What is the line of code where the vulnerability is found?"
- Analyzing the supplied main.c we found that the vulnerability was in line 12 - gets(buffer).
- gets() is a C function that reads a byte from the stdin until \0 or \n is found. 

Question 2:
"What does the vulnerability allow you to do?"
- This vulnerability allow us to overwrite the value of the return address, inject shellcode, and then jump to that code, which will be executed automatically.
--------------------------------------------------------------

- We used gdb to analyse program and found that 108 is the offset we need to alter the return adress.

- We used the shellcode to the execution of the /bin/bash command and x90 (advance).

- We used the following exploit:

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf4img3.png "Title")

- And we sucessfully get the flag:

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf4img4.png "Title")
