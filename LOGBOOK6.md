# Task 1

- Compile the server using the provided makefile
- Run server with docker-compose up

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img1.PNG "Title")


- On a new terminal, run "echo hello | nc 10.9.0.5", this send a text with "hello" to the target server

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img2.PNG "Title")

The server returns properly, how to defeat that?

- Send a "format string" character (%s) and the program crashes( not the server itself, as the format program i just a child process)

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log6img2.PNG "Title") 

# Task 2: Server program memory

## Task 2.A: Stack Data
