# XSS

## Getting familiar with HTTP Header Live

Before actually starting this lab, we need to make sure that "HTTP Header Live" is functioning, so we enable it, and click on any link to start capturing data...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img1.PNG "Title")

As we see, it appears to be working correctly.

## Task 1: Posting a malicious message to display an alert window

This task is fairly simple, just insert the given code in one of the profile´s fields...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img2.PNG "Title")

 And any one that visits this profile will execute the code.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img3.PNG "Title")

This is completely harmless, but has the potential to be extremely dangerous, allowing attackers to obtain private/sensible information.


## Task 2: Posting a malicious message to display cookies

This task is just as simple as the first one, but potentially more dangerous, if the attacker were to gain access to it, and it reveals user session info.
Like last time, put some JS code in a profile field...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img4.PNG "Title")

And again, everyone that visits the profile will have session info revealed.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img5.PNG "Title")

## Task 3: Stealing cookies from the victim´s machine

In this task, we will try to transmit the info obtained in the last task, to the attacker.
The way we will do this, is send an HTTP request with info in the cookies appended, as is explained in the seed lab guide.

Again, we put some JS code in the attacker´s profile...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img6.PNG "Title")

And here we see, when an innocent user visits the attackers profile, his cookies are sent to the attacker, as an HTTP GET request.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img7.PNG "Title")

## Task 4: Becoming the victim´s friend

First we need to figure out what is sent to the served when a friend request is sent.

To test this, we login as Alice, send a friend request to Boby and capture the generated HTTP request, with the help of "HTTP Header Live"

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log10img8.PNG "Title")