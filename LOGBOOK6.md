# Task 1

- Compile the server using the provided makefile
- Run server with docker-compose up

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img1.PNG "Title")


- On a new terminal, run "echo hello | nc 10.9.0.5", this send a text containing "hello" to the target server

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img2.PNG "Title")

The server returns properly, how to change that?

- Send a "format string" character (%s) and the program crashes( not the server itself, as the format program i just a child process)

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img3.PNG "Title") 

# Task 2: Server program memory

## Task 2.A: Stack Data

- Now we are given the task of printing out some data from the server memory, that will be printed out server side, but since we are both the attacker and server this is fairly easy to do, especially so when we are know there is a format string vulnerability.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img4.PNG "Title")

- Here we can see that by sending a "%x" character, we obtain data from the memory, in this case we get the "target variable´s value" that is also printed out in regular use, server side.

- Next , before sending a large number of "%x" we need to add something that is identifiable by us, we choose the letter a(ASCII value: 61) and look for it in the server terminal to find out the stack´s size

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img5.PNG "Title")

## Task 2.B: Heap data

- To get the stack data, we used the provided script as a baseline and edit it with the correct values.
- We add the message´s address to the number variable
- Add the same message we used in the last step "aaaa"
- And finally add the number - 1 of "%x" needed to reach the desired postion followed by a %s to read the contents of the desired position.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img6.PNG "Title")

- Finally, we run the script and receive our very secret message

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img7.PNG "Title")

## Task 3 Modifying the server program´s memory

### Task 3.A: Change the value to a different value

- Like we did in task 2.B we add the adress to the beginning of our string that we build using the python script
- We know we can access it by using "%x" 64 times
- And by putting an %n at the correct addres we store the target´s value
- So we edit the previous script for our new objective

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img8.PNG "Title")

- Run the script, send the string to the server and we can see that the value indeed crashed

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img9.PNG "Title")

### Task 3.B: Change the value to 0x5000

- Now, instead of any value, we have to edit it to a specific value of 0x5000(20480 in base 10)

- To do that we to print the exact number of bytes
