## Challenge 1: ApplyForAFlag

We start by connecting to the server, and are greeted by this page.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img1.PNG "Title")

There doesn´t seem to be a whole lot to explore, so surely the exploit will be performed in the seen above text field.

We first try sending and *honest* request, but are quickly shot down.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img2.PNG "Title")

So, if the input ISN´T sanitized, all we really need to do is write a small block of JS that will click the button for us, since it is shown to us even when we aren´t an admin, for some reason.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img3.PNG "Title")

We submit another request, this time we also inspect the button, to find its ID.

We then write the following code.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img4.PNG "Title")

Wait for a while, and suddenly...

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img5.PNG "Title")

Flag obtained.

## Challenge 2: Router 6G

We start by taking a look around, and we find.

- A login page.

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img6.PNG "Title")


- A secondary page with 2 features  
![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img7.PNG "Title")

	- A speedtest  
	![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img8.PNG "Title")

	- And a ping feature  
	![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img9.PNG "Title")

Of these features we find that.

- The ping feature seems to use the linux "ping" command internally, as the output seems identical to the one in our seed VM

 ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img10.PNG "Title")

 - The login feature redirects to a "login.php" file that tells us our data is incorrect and isnt redirecting us to anywhere.

  ![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctf5img11.PNG "Title")
