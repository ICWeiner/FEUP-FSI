We start by doing an initial setup, including disabling address space randomization

After running make on the folder with code provided for the lab, we get 2 binaries "a32.out" and "a64.out", which are 32 bit and 64 bit versions of the same program.
Running them appears to change the current shell session into a brand new one, that lacks all environment values with the exception of PWD
This new shell session appears to "steal" the old one, so if something like this is injected into an ordinary vulnerable program, we can potentially gain root shell access on a machine.



Compiling the vulnerable program we disable stack protection to simplify the attack, change ownership of the program to root and the change the permissions just like on the last lab, to enable Set-UID.
All of this is already provided in the "Makefile"

Running the target program in debug mode, we extract the buffer´s starting position and the place where the return adress is stored

