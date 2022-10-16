# LOGBOOK 4 Environment Variable and Set-UID Program

## TASK 1

For the first task we run both printenv and env, and, if not additional arguments are given, they have the same output.
With printenv we can more easily print the value of a specific variable, we can also achieve this with env, if we use it in conjunction with grep

Running export "insert_var_name_here"="insert_value_here" sets the given value to the selected variable, or creates it if it didnt exist
Running unset deletes a variable and its set value

## TASK 2

Compiling and running the program myprintenv.c seems to give the same output as running the printenv command on the shell, which is normal, since the program itself calls the printenv command


![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img1.PNG "Title")


Commenting out the child process case and uncommenting the parent process case gives the exact same output which makes us believe that child processes inherit environment variables from their parent

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img2.PNG "Title")

## TASK 3


Compiling and running the program myenv.c as gives no output

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img3.PNG "Title")

Making the suggested change appears to give similar, if not the same output as running env on the shell(since it seems to use that program internally in myenv.c)

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img4.PNG "Title")

The new program get a *copy* of its parents environment variables (in this case, the shell) 

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img5.PNG "Title")*this info obtained by running man environ*


## TASK 4

Compiling and running the given code confirms that the enviroment is passes on to the new program

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img6.PNG "Title")

## TASK 5

Doing the steps given and running export on PATH ,LD_LIBRARY_PATH, DESKTOP_SESSION and XDG_MENU_PREFIX had varying effects.
LD_LIBRARY_PATH was the only one that didn´t inherit the newly set value which was a surprise.


## TASK 6

Running our own malicious code instead of "ls" in this case is fairly easy, all you have to do is name a malicious binary "ls" and add the path to it using export (e.g export PATH=/home/seed/Documents/Labsetup:$PATH)

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/log4img7.PNG "Title")
