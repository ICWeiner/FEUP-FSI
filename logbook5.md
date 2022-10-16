# Task 1

We start by doing an initial setup, including disabling address space randomization and configuring /bin/sh

Then we familiarize ourselves with the C Version shellcode, and its respective 32 and 64 bit version in assembly

After running make on the folder with code provided for the lab, we get both versions shellcode  binaries "a32.out" and "a64.out", 
Running them appears to change the current shell session into a new usable shell as can be seen below where we run the ls command on both versions

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log5img1.PNG "Title")

# Task 2

When compiling the vulnerable program we disable stack protection to simplify the attack, change ownership of the program to root and then change the permissions ,enabling the Set-UID bit, just like on the last lab.
All of this is already provided in the "Makefile" as can be seen below

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log5img2.PNG "Title")

# Task 3

Running the target program in debug mode, we extract the buffer´s starting position and the value stored in the ebp register

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log5img3.PNG "Title")

Now to fill the missing data in exploit.py, we add the shellcode code to the correct variable, calculate the starting position which is size of buffer (517 in this case) - length of the shellcode.
ret is starting adress of buffer + 400 so it jumps to the middle of the NOP instructions an enventually get to the shellcode
offset is diference between ebp and start of buffer PLUS 4 (this moves the return address to the right address)
we mantain the value of 4 in the L variable since we use 32 bit shellcode.

we then run the exploit script followed by the vulnerable program and...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log5img4.PNG "Title")

We are now in a new shell with root permissions 

