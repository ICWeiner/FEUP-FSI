## Challenge 1: Number Station

For this CTF, we know that the public exponent is 0x10001 and that p and q that make up n are prime numbers.

p is close to 2^512 and q is close to 2^513.

Our first objective is to find the exact values for p and q. 

This is easily achived with the following python code.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf6img1.PNG "Title")

Next we need to get the value of d, which is used to decode the flag.

We get d with the following code.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf6img2.PNG "Title")

Now we just need to get the enconded flag from the server...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf6img3.PNG "Title")

And decode using the script.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf6img4.PNG "Title")

Flag obtained.

## Challenge 2: 