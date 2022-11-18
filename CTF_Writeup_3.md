# CTF 3


## Task 1

### Checksec

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img1.PNG "Title")

### Obtaining the flag

In this challenge, the memory addresses are static and the flag is loaded into memory.
The vulnerability is located in a printf function that doesnt have a format string specified, so it accepts all types of content, and this content comes from outside, completely unfiltered.
We used the provided exploit script, giving it the adress of the buffer, which we found with the help of gdb.

First we need to extract the variable´s address

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img2.PNG "Title")

Running the script against the ctf server, we immediately get the flag.
The principles applied in this CTF are essentially the same ones that were used in the format string logbook

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img3.PNG "Title")

## Task 2

### Checksec

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img4.PNG "Title")

### Challenge

This time, instead of reading a value stored in memory, we need to change the value of a variable to unlock the flag, something we also did in the format string logbook, except this time, the value is 0xbeef (ha!), or 48879 in base 10.

First off, we need the address of the variable we want to change

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img5.PNG "Title")

Then , we edit the script used in the last ctf to send "%n", the address of the variable and inject a total of 48879 chars, to change the variable to the correct value, and gain shell access.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img6.PNG "Title")

Then we get shell access, so now all we need is to read the flag.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf3img7.PNG "Title")
