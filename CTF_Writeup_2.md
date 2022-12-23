# CTF 2


## Task 1

### Checksec

- Arch: 	i386-32-little
- RELRO:	No RELRO
- Stack:	No canary found
- NX:		NX disabled
- PIE:		No PIE
- RWX:		Has RWX segments

### Code analysis

- Very overflow prone
- Name of file is stored right after(in memory) the buffer that is overflow prone
- Buffer is read straight from input, no filtering
- Flag is in flag.txt, on the working directory

### Exploit

Exploiting this code is fairly easy, we only have to replace the contents of the "meme_file" array.  
How? Simple  
First we have to cause an overflow by writing any char a total of 20 times
Since the function reads 28 chars on a buffer of 20 all chars read afterwards will be written to its neighbour, replacing its original content, in this case "meme_file".  
Then we write "flag.txt", and since the code doesnt check for overflows, it will simply continue running with its new content and the flag is given to us.  


![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf2img1.png "Title")

## Task 2

### Checksec

Same as above

### Code analysis

Whats changed?  
The program now has a new defense mechanism, altough not only does it suffer from the original overflow problem, the new defense ALSO suffers from overflow.  
After some careful looking we realize that "0xdeadbeef" was written in code as "\xef\xbe\xad\xde"  
So all we have to write "0xfefc2223" in this notation , "\x23\x22\xfc\xfe"  


### Exploit

First overflow "val", to be equal to the one in code, then overflow "meme_file" just like last time.  

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/ctf2img2.png "Title")
