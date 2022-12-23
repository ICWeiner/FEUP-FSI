# XSS

## Getting familiar with HTTP Header Live

Before actually starting this lab, we need to make sure that "HTTP Header Live" is functioning, so we enable it, and click on any link to start capturing data...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img1.PNG "Title")

As we see, it appears to be working correctly.

## Task 1: Posting a malicious message to display an alert window

This task is fairly simple, just insert the given code in one of the profile´s fields...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img2.PNG "Title")

 And any one that visits this profile will execute the code.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img3.PNG "Title")

This is completely harmless, but has the potential to be extremely dangerous, allowing attackers to obtain private/sensible information.


## Task 2: Posting a malicious message to display cookies

This task is just as simple as the first one, but potentially more dangerous, if the attacker were to gain access to it, and it reveals user session info.
Like last time, put some JS code in a profile field...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img4.PNG "Title")

And again, everyone that visits the profile will have session info revealed.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img5.PNG "Title")

## Task 3: Stealing cookies from the victim´s machine

In this task, we will try to transmit the info obtained in the last task, to the attacker.
The way we will do this, is send an HTTP request with the cookies appended, as is explained in the seed lab guide.

Again, we put some JS code in the attacker´s profile...

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img6.PNG "Title")

And here we see, when an innocent user visits the attackers profile, his cookies are sent to the attacker, as an HTTP GET request.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img7.PNG "Title")

## Task 4: Becoming the victim´s friend

First we need to figure out what is sent to the server when a friend request is sent.

To test this, we login as Alice, send a friend request to Boby and capture the generated HTTP request, with the help of "HTTP Header Live"

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img8.PNG "Title")

The generated HTTP Request is:
- Of the GET type
- With the values:
    - friend (should be the target user´s id in the database)
    - elgg_ts (ts = timestamp)
    - elgg_token (cookie)

So, to exploit this we we need to trigger a GET request.
The base code for the exploit is provided to us by the seedlab guide

By performing a friend request to samy we find that his *id is 59*

Using the previously gathered information, we fill in the provided exploit and also add an alert at the end, to make it easier to spot that the code was sucessful

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img9.PNG "Title")

We then login into another user´s account, visit samy´s profile and are greeted by the following.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img10.PNG "Title")

And visit samy´s profile to comfirm sucess.

![alt text](https://github.com/ICWeiner/FEUP-FSI/blob/main/imgs/logbook10img11.PNG "Title")


## Questions

### Question 1:
"Explain the purpose of Lines marked 1 and 2, why are they needed"

- Both Lines are required to generate a well-formed friend request, as we learned when we studied the HTTP request at the beggining of task number 4
- If these lines didn´t exist, the server would just ignore our request.
- Also, since these values are unique for each user, they cant just be hardcoded into the generated URL, as we do for samy´s ID


### Question 2:
"If the Elgg application only provided the Editor mode for the "About Me" field, i.e.,you cannot switch to the Text mode, can you still launch a successful attack?

- We dont think it would be possible if the application only provided the editor mode, as the other mode adds extra HTML and also does some encoding.
