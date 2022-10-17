## Reconnaissance

To start off, we read both files that are placed in the starting directory (/home/flag_reader) 

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctfbritish1.PNG "Title")

We can see that "main.c" tries to access "flags/flag.txt" and that "my_script.sh" will enter an if section when there is a "env" file in /tmp/.


![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctfbritish2.PNG "Title")

By navigating to /tmp/ we also find a "last_log" file that seems to be generated every minute by a "cron" service and seems to contain output from both "my_script.sh" AND "main.c" AND it has permissions since it writes "File exists!!". This file also belongs to "flag_reader" so whatever generates it should be exploitable, if we can abuse of that "printenv" in "my_script.sh" 

## Exploit

After some testing we find that we can change environment variables by altering the contents of "env" so, we write to it echo "PATH=/tmp:$PATH", with this we can run our own version of "printenv"
We grant all permissions to our "printenv" by running "chmod 777 printenv", and write inside it "cat /flags/flag.txt".
Now all we need to do is wait until the next minute, followed by reading the contents of "last_log"

## Example

A full example of this CTF can be found below

![alt text](https://git.fe.up.pt/fsi/fsi2223/l11g03/-/raw/main/imgs/ctfbritish3.PNG "Title")
