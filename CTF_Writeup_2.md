CTF 2

Step 1
Reading the code we see a buffer of 20 beinf written in a size of 28.
We can cause a buffer overflow by wtiting 20 chars of something followed by flag.txt to get the program to open it instead of the one it normally would

Step 2
now we see that the area is protected by a memory address, with the default being 0xdeadbeef, written as \xef\xbe\xad\xde and the intended being 0xfefc2223.
However the code still has the buffer overflow vulnerabilty so we can replace the value of the address by writing 20 chars followed by \x23\x22\xfc\xfe, followed by flag.txt.