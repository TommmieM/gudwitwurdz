+++
title = "Lesson 1 Command Line Starters"
date = "2023-03-12T14:52:08-06:00"
author = "Tommie Matherne"
authorTwitter = "" #do not include @
cover = ""
tags = ["Linux", "command line", "cd", "ls", "pwd", "flags"]
keywords = ["Linux", "cd", "ls", "cd", "pwd", "flags"]
description = "The most basic commands. Navigation and orientation of you file system, and how to enhance the results with flags."
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

## Welcome to the Command Line

In this first lesson, I am going to make a few assumptions. You have access to a Linux command line, and know how to open it. Other than that, this is completely for a new user. Below we will take our first steps with Linux, and like any first steps, the best way to start off is by being able to orient yourself. The commands in this lesson will give you the ability to know what directory you are in, what is there, and how to go to other areas of the filesystem. So let's go!

### A bit about the prompt.

When you first open the terminal, you should be met with a prompt something like this ```user@host:~$```. This is the default prompt. The anatomy of it is rather simple. The first portion identifies the ```user```, this is the logged in user, hopefully, you. After the at sign, is ```host```, or the name of the workstation (computer) that you are logged into. Linux has roots from Unix, the original multiuser and multi-machine operating system. From your desk, you may sign into any number of available servers. The ```host``` portion of the name is a bit of an identifier of that legacy, and gives your computer a server name. Linux, by virtue of that Unix legacy, can be used as a server. In fact, Linux servers run more of the internet than any other kind of server operating system at 38% of all websites and 49% of the top 1,000 websites currently active according to W3Techs' usage comparison. 

That is the end of the identifier portion of the prompt. As is common in Linux, the separator is a colon (:). Everything after this is the actual prompt. The ```~``` located here is actually the current location. ```~``` is a shorthand in Linux as the user's Home folder. If you come from a Windows background, think of this as your Users folder there. This is where you, as a user, keep your files. Other users have their own Home folders, which you may or may not be able to look into depending on the permissions that are set up on your account as well as the individual folders. 

One last note. Up to now, I have been using the Windows terms that should be more familiar to most readers. In Linux, though, they are called directories. The meaning is exactly the same: a filesystem organization tool to present an easy way to find files stored on the hard drive. From now on, I will be referring to them as directories. 

Next, there is the ```$``` identifier. This is the active prompt. The ```$``` signifies that you are using the prompt as a normal user. If you change to a root account (synonymous with superuser or administrator), the ```$``` will change to a ```#``` to signify that difference. After that, is the blinking cursor. Let's put it to work, shall we?

## 'pwd' - the Where Am I? of Linux

At any time at the prompt, if you type in ```pwd``` and hit enter, you will be met with a full print out of your current location. This tells you the path from filesystem root ```/``` (think of this as equivalent to ```C:\``` in Windows), down the directory tree to your current directory. If you haven't changed directories since opening the terminal, it should look similar to ```/home/username``` with 'username' actually being replaced by your user name. That is the folder that is signified by the ```~``` in the prompt. I bring this one up first as it will provide some valuable context for the next few commands. There really is not much to be said about this command, so let's move on, shall we.

### A note about the file paths

The results of the ```pwd``` command was what is known as a file path. More particularly, it is an "absolute" file path. It starts at root (```/```), and travels past each folder name, separated by further '/' characters, and ends with a final '/' to denote that this, too is a directory. There are also a second kind of file path printing known as "relative" file paths. This is the path forward from where you are currently, on through to where you want to end up. Describing this now is a bit difficult to do with clarity. We will return to this idea shortly.

## 'ls' - Well what have we got here?

So, thanks to ```pwd```, we know where we are. But what is here? To overuse comparisons, this command line currently is a cave as black as the screen it is printed on. How do we shine a light on this? ```ls``` is out next command to do so. Typing this command will "LiSt" the contents of the current directory, go ahead and try it out. Your output should include several items like ```Desktop```, ```Documents```, ```Downloads```, etc. These are the directories that are inside of your home directory. If you have a few that are a different color or emphasis level, those are files within this directory. Files will usually have file extensions, where directories will not. The exception to this is plain text files, which in Linux, do not require the '.txt' file extension. 

This is pretty interesting, but the ```ls``` command actually introduces us to a few more concepts to Linux commands: flags and ```man``` pages.

### A note about flags

When you type in a ```-``` after a command, this is called a flag. Most flags are single letters, and can be preceeded with a single ```-```. There are some flags that are entire words, though. When defining those flags, use a double flag notation (```--```). But how do you know when you can use a flag, and what those flags are? 

### A note about ```man``` pages. 

Most, not all, commands in Linux have a MANual page that correlate to them. The help files for Linux are literally built into the system itself! To get to them, type in the command ```man```, followed by the command you want to view the man page for. In this case, let's take a look a the man page for ```ls```. Type ```man ls``` at your command line now. You can use either the arrow keys or the keyboard letters ```j``` and ```k```. The keyboard options are known as Vi controls, we'll touch more on that in a later lesson.

Let's take a look at this page. Being able to read these pages is an important skill for us. Every page should begin with a **NAME** area. This will tell you the command name, which is what you type at the command line, and usually a short line about what it does for you. After that **SYNOPSIS** will give you an idea of how it is used. The ```ls``` command can be followed by \[OPTION\] and \[FILE\]. The ```...``` after each is to denote that more than one of either option can be defined. Anything marked as \[OPTION\] can usually be omitted. 
Next is the **DESCRIPTION** portion of the man page. This is where you first find a more detailed description of what the command does, as well as the options for the command. As you can tell, there are a lot of options that can be used with ```ls```! Let's just focus on two very useful ones for now, ```-a``` and ```-l```. Read up on those two, then press ```q``` to exit the man page.

### Back to our regularly scheduled program

Now, back at the command line, we have a couple of things to clear up. Originally, I said "flags", but the man pages call them "options". This is the first instance of the time that you will see multiple names for the same thing in Linux. At least, if you don't count the fact that a lot of people use the terms "folder" and "directory" interchangably. Hopefully, that doesn't get too confusing, trust me, you get used to it. 

Now, let's put our findings to good use. At the command prompt, type in ```ls -al```. Yes, short code options can be strung together after a single dash (```-```). That is why if you are using an option/flag that is a complete word, you must preceed it with double-dashes (```---```). Anyway, type that in and press enter and you will notice a bit more informationpresented that we need to discuss!

First, there are obviously more directories. And they are all listed in a single row. AND what is with all these columns?! This is actually a more advanced way of viewing the contents of the directory you are in. It includes all folders, including hidden directories, which are revealed by the ```-a``` option. The columns are a result of the ```-l``` option. The first column contains a string of letters and dashes that tell you the permissions for that folder. The 'd' at the beginning denote it is a directory, files have a preceeding dash. Next are three sets of 'rwx', where each letter may be replaced by a dash. These mean "read", "write", and "execute", and are repeated three times for "User", "Group", and "Other". We will get into what that all means in another lesson as well, for now, it isn't important. This is followed by a number that says the number of links to that item (directory or file) exist on the entire file system.

The next two columns at this point will likely have your user name in both columns. These tell you what group the file belongs to, and what user in that group created the file. Again, for now, not terribly important, and we will come back to this as we get deeper into Linux administration.

The next set of numbers is the file size measured in bytes. There are more options available that will print this in more easily digestible numbers, but you may notice now that directories are all listed as being 4096 bytes, no matter how much is contained in the directory. This is because that is just the size of the identifier that is the directory name, not the size of the contents of the directory iteself.

The final column before the directory name is the date and time the file or directory was last modified. Not terribly important for home use, but if you ever get a job as a cybersecurity role, this can actually be important digital forensics to note.

Finally, the names of all directories, including hidden directories. You may notice that all of the directories that now appear that were not in the original listing begin with a '.'. Believe it or not, hiding a directory or file in Linux is as simple as starting it's name with a '.'. You may be a bit confused at the first two directories, ```.``` and ```..```. MORE LINUX SHORTHAND, YAY!

These are indeed, short names for two very specific directories. ```.``` is simply the shorthand form of the current directory. To show this, let's try something. The ```ls``` command is not limited to only the directory we are currently in. If you type in a directory name after the options, you can list the contents of that directory. Let's try it, type in ```ls -al .``` with that '.' included at the end. As you can see, it repeats the same list. That is because '.' is shorthand for the directory itself. Every directory has a reference to itself built in, named '.'

So what about the '..'? That is a shorthand to the directory directly above the directory you are in. If you remember, when we typed in ```pwd```, we got an answer of ```/home/username```. So ```username``` is our current directory, and one level above that is ```home```. If we try ```ls -al ..```, you should get a response of ```username``` along with '.' and '..'. There may be more, as well, if there are other users on your Linux machine. The thing to note here, is that I mentioned every directory in Linux automatically has a '.' file referring to itself. This is also true of '..'. At first, this may not make much sense, as it would seem that there couldn't be a '..' file for this, as there is no level higher. For ```/```, the '..' shortcut simply refers back to ```/``` just as '.' does. Don't worry, that's just trivia, you will never think about it again.

Let's talk briefly about one last command before we stop for the day, shall we?

## 'cd' - Now we are going places!

Our next command is ```cd```. If you are a curious reader, you may notice that this command doesn't have a man page. The only reason for that is that there are no options for this command. ```cd``` is the "Change Directory" command. By typing in ```cd``` followed by the name of a directory, you move your ```pwd``` to that directory. This brings up an important point, though. How do you have to type in the name of the directory? We mentioned earlier that the "absolute" path to our home folder was ```/home/username```, to get to, say, the Docurments directory, do we have to type in ```cd /home/username/Documents```? Well, we could. That would absolutely work. However, "relative" pathing would be much simpler.

### More about relative file paths

So, what is a relative file path? Simply, it is typing the name of a directory with the assumption that you are currently in the directory containing that as a subdirectory. The system will prepend ```pwd``` to the path, and attempt to move there. So if you were to type in ```cd Documents``` from your home directory, the system would see that as exactly the same as ```cd /home/username/Documents```. This makes typing a lot easier. 

If you ever do find yourself outside you home folder, or whatever other folder you thought you were in, Linux will print out a nice error message saying that the directory you are trying to move to doesn't exist. You can use a mixture of ```pwd``` and ```ls```, to orient yourself to correct your ```cd``` command to get where you mean to be. 

### Whew! That was a Lot!

Well, not really. But it was enough to get started. Look around, see what you can find. Explore your file system a bit and see what is there, and try to think about why. Knowing how your system is laid out is a very important thing for someone looking to take control of that system. Stay curious!
