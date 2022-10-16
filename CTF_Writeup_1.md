# CTF 1 - Security check of a wordpress instance 

## Reconnaissance

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img1.PNG "Title")

*Probably a less than ideal start, wordpress and plugin version on public display*

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img2.PNG "Title")

*teachers think they are funny*

We also immediately find some hints to possible user logins

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img3.PNG "Title")

Trying to login with a random name gives us the following

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img4.PNG "Title")

Which suggests the site may give us too much info(it shouldn´t tell us whether an given username exists or not)

As can be seen below, it does gives us too much info

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img5.PNG "Title")

We also find another username but it seems to be unactivated

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img6.PNG "Title")

## Search for a vulnerability

After some search on CVE websites we find one that is very promising.

CVE-2021-34646 states that up to version 5.4.3 of Booster for WooCommerce, which is installed on this instace have an authentication bypass vulnerability via the email verification process
Inserting flag{CVE-2021-34646} on the CTF website confirms we picked the right one

## Search for an exploit

On exploit db we can find a small python script that exploits this weakness and can bypass login with ease

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img7.PNG "Title")

## Running the exploit

Following these instruction we go to http://ctf-fsi.fe.up.pt:5001/wp-json/wp/v2/users and find the user id related to admin

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img8.PNG "Title")

We run the exploit, giving it the website url and the previously found user id

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img8.PNG "Title")

We then obtain three links, we click on one

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img9.PNG "Title")

And we sucessfully bypass authentication and are now logged in as an admin 

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img10.PNG "Title")

We then access a private post containing the final flag, flag{please don't bother me}, completing our very first CTF

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf1img11.PNG "Title")
