Compiling and running the program myprintenv.c seems to give the same output as running the printenv command on the shell

After commenting the line nothing is written in the output.




Compiling and running the program myenv.c as given seems to have not output

Making the suggested change appears to give similar, if not the same output as running env on the shell(since it seems to use that program internally in myenv.c)

The new program get its environment variables



Running export on PATH and assigning random values ended up making the current shell session unusable.
Then running on LD_LIBRARY_PATH, DESKTOP_SESSION and XDG_MENU_PREFIX had varying effects.
LD_LIBRARY_PATH was the only one that inherited the newly set value



Running our own malicious code instead of "ls" in this case is fairly easy, all you have to do is name a malicious binary "ls" and add the path to it using export (e.g export PATH=/home/seed/Documents/Labsetup:$PATH)