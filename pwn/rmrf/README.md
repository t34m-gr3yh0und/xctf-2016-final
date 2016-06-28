# rmrf

As you ssh in, you will find that many of the commands that you are used to are gone just like when a system is being
```sh
    $ rm -rf /
```
Your goal is to find the flag with the limited commands that you can use.

After a few trial and error, you will find that you can use
```sh
    echo
```
which is a very useful command, as you can do a ```ls``` with these commands
```sh
    $ echo *
    $ echo */*
    $ echo */*/*
```
The third will show you the file that contains the flag.
```
/dev/treasure/fl_ag_come_at_me_bro
```
Now to show the contents of this file. However, you cannot use any of the commonly used commands like ```cat```, ```head``` or ```tail```. But you can use ```read``` and you can write a shell script that is ```/bin/sh``` based.

So what you need to do is
```sh
    $ while read line; do    
    > echo $line    
    > done < /dev/treasure/fl_ag_come_at_me_bro
```
And you will be able to get the flag.
