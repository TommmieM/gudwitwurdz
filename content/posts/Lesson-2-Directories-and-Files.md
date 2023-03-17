+++
title = "Lesson 2 Directories and Files"
date = "2023-03-16T18:57:00-06:00"
author = "Tommie Matherne"
authorTwitter = "" #do not include @
cover = ""
tags = ["Linux", "commands", "files", "directories", "mkdir", "rmdir", "cp", "mv", "locate", "touch", "rm"]
keywords = ["Linux", "commands", "directories", "files"]
description = "Now that was know where we are, what can we do with it? Making and removing directories and files"
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

## Let's Be Manipulative

So now that we have an idea of what our filesystem looks like and how to traverse it, how do we change it? Let's go over a few commands to get the basics on creating and deleting files and folders, as well as moving them around. We are also going to talk a bit about wild cards that you can include to lower the amount of typing. Well, enough talk, open your terminal and let's get started!

### The Power of Creation

While moving around the file system, you may have noticed that your Linux system comes with quite a large set of files and folders already included. Especially if you ventured out of just your home folder. For the most part, however, most of what you will do as  a user of a system involves only what is in your home folder, and that area is pretty bare. 

To keep things rather tidy, you will likely want to make directories inside your directories, and files inside of those. So, let's get that sorted now, shall we? Assuming you began from your home folder, type in ```cd Documents``` to get to your Documents directory. If you run ```ls``` to list the contents of this folder, it will likely not show any files or folders (unless of course, you have been studying ahead. If that's the case, good on you!). 

Again, organization is always a good thing, so how about we drop a directory in here before we start creating files out of nowhere? Type in ```man mkdir``` to get a look at what the ```mkdir``` program does for us. The command and the options for it are pretty straightforward, and I'm not going to insult your intelligence by going over all of them. Most important information, right at the top, "Make Directories", and it does just what it says on the tin.

So type in ```mkdir foo```. You don't have to go with the name ```foo``` there, that's just a common placeholder in tutorials. Anything after the command ```mkdir``` is going to be the name of the directory that is created where you currently are. You can prove this by once again tpying ```ls```. The listing should show a folder named ```foo```, or whatever you chose to name that folder. If it doesn't, go back in your history and look for errors, chances are you may have made a typo in the command like I did when I was following along with my own tutorial! No shame in that, just check the spelling, and try again.

Going back to last lesson, if we use the ```ls``` command, we can list the contents of the new folder if we pass the name of the folder to the command. Let's try that, ```ls ./foo```. Remember, the ```.``` is a shorthand for the current directory, and ```foo``` can be replaced with whatever you named that folder you just created. The command should come back empty on this one, since we just created the directory and didn't put anything in it. 

To do that, unless you want to dig into downloading things from the internet right away from the command line, we can use the ```touch``` command. Go ahead, try reading through ```man touch``` to see what that is all about. Go ahead, I'll wait for you, and join you back in the next paragraph.

So this one seems a bit more complicated, doesn't it? It is important to know what it says there. "Change file timestamps". For our purposes, the more important information is in the second section, second paragraph, though. "A FILE argument that does not exist is created empty..." If you ever do get into a role where you have to do a forensics investigation, however, keep that first part in mind. ```touch``` can change the creation and access dates that show up in the system for a file, so you cannot just believe what you see!

Anyway, to the matter at hand, let's pass it a non-existent file and get it created. Try ```touch ./foo/bar```. Again, ```bar``` is just one of those placeholder words used in beginner tutorials a lot when the author has no imagination and a lot of geekiness, you can name the file whatever you would like. Now, if you type in ```ls```, you'll see... ```bar```? What? That's the folder we created? 

We never changed directories to get into the folder, but gave the directory name as part of the argument for ```touch```. What are the results of ```ls ./foo```?  There is our file, safe and sound. This is another important idea to keep in mind: you can manipulate any part of the system from wherever you are in the system, so long as you know the path to get there!

### An bit of misdirection

Two commands that we will go into detail about later are ```echo``` and ```cat```. For now, though, we will use them. I won't have you read the ```man``` pages for these two just yet, but you can if you want to. Who am I to stop you? I'm just words on a screen.

Right now, we have an empty file. We can change that, and prove that we have changed it with the above two commands. The ```cat``` command prints the text in a file to the terminal. Right now, if we try ```cat bar```, nothing happens, because the file is empty.

However, ```echo``` is a much more interesting command. Try ```echo "Hello, world!"``` . You should see the words ```Hello, world!``` printed back before your prompt returns. The fun of echo, though, comes in some built in utilities of the command line. Namely, redirecting input. 

We can do this with what are called the direction operators. The first we are going to use is ```>```. Try ```echo "Hello, world!" > bar```. The command prompt should return as normal with nothing printed after the command and before the prompt. If you do ```cat bar``` now, though, it should output ```"Hello, world!"```. You have just written information to the file!

If you try that again, and put in ```echo "Good-bye!" > bar```. When you try ```cat bar```, it writes out ```Good-Bye!```. What happened to the greeting? It was overwritten. When you use the ```>``` direction operator in the terminal, it does what is called a destructive direction to the file. Anything that was previously in the file is removed, and the new data is written. 

Let's put our greeting back, ```echo "Hello, world!" > bar```. If you'd like, you can ```cat bar``` to verify, it now says ```Hello, World!```. If we want to add more to the file without losing what is already there, the non-destructive operator has our back. ```echo "Good-bye!" >> bar```. Note the double ```>>```, that is what makes it non-destructive. 

For now, it isn't important, but we can actually make things flow in the other direction, as well. We have no occasion to use this now, but when we are building longer, more complicated lines, you may need to read information from a file in a part of it. At this point, the ```<``` and ```<<``` operators will direct that flow of data. 

### Rearranging things

Right now, the file we made sits in a directory we made, inside of our Documents directory. While I mentioned earlier that organization is important, we are about to mess things up a bit. Get back out of the ```foo``` directory and back into the Documents. You have all the tools needed, I'm not going to give you the code for this one. 

Got back there? Good! Knew you had it in you! Those shortcuts we've been mentioning are about to come in handy. Let's say for a moment that you want a copy of ```bar``` here in Documents. While it is a rather simple bit of text, it would get cumbersome later to recreate a file that may be a few thousand lines long. There are easier ways: copying and moving files.

Copying files can get rather wild. If you read ```man cp```, the man page for the ```cp``` command, you will quickly get to realizing that there are a few different ways to use the command. We are about to go through all of those ways.

First, we will copy the file to a different file name within the same folder with a different name. To do this, we are going to use the following: ```cp ./foo/bar ./foo/baz```. Again, ```baz``` is just a placeholder, use whatever name you like. We use the file path as the terminal is currently working in the Documents directory, so we need to point first to the ```foo/``` directory before specifying our file. Likewise, if we try to ```ls``` the contents of ```foo/```, you can see both the ```bar``` and ```baz``` files sitting there. Further, with ```cat``` and the file path you can confirm that both files contain the same data. 

It seems a bit silly to have two files with the same information in the same directory, so we are going to get rid of one of them. To do that, we use ```rm```. ```man rm``` gives more information. This is the remove command, and it does just what it says on the tin, which is probably a phrase that is getting tiring at this point. But it is true. Let's try ```rm ./foo/baz```, and then ```ls ./foo``` one more time. Yup, it's gone!

For the sake of argument, though, go ahead and re-copy that file into existence. I promise, this will make sense soon. In fact, let's get into how. So if you ```ls foo``` now (that's right, you don't need the ```./```), you should see both files sitting in that folder. Now, let's say you want those files in the Documents directory instead. We could copy them and then remove them from ```foo```, but that seems a bit overkill. There has to be an easier way, right?

Enter ```mv```. If you read the ```man``` page, you will see that the use and options between ```mv``` and ```cp``` are very similar. Other than the program name, commands written with the two will both work if you just change the program name at the beginning. For the most part. Some flag sets are different, but other than that, they are very similar. Keep that in mind as we go through this part, because we are going to do a move that could work just as well for copying files. 

For instance to move both files to the Documents directory, the command would be ```mv ./foo/bar ./foo/baz .```. The two file names are both provided, the final ```.``` denotes the place we want the files to be moved to. So if you do ```ls``` now, you can see that ```foo/```, ```bar```, and ```baz``` are all here. 

There is one more useful thing that ```mv``` can do for you as well. Try ```mv baz bas```. The file name ```bas``` did not exist when you did this, but if you do ```ls``` now, the contents of Documents are ```foo/```, ```bar```, and ```bas```. ```baz``` no longer exists. And if you ```cat bas```, you see that the contents are the same. You can use ```mv``` to rename your files. That's enough for now, though. Shall we clean up?

### The Power of Destruction

Just as we can create files and directories, we can remove them. For instance, currently, we have an empty directory. ```rmdir``` will help us get rid of it. I will actually not walk you through this one! Read the ```man``` page if needed, and see if you can get ```foo/``` gone.

Keep in mind, this will only work if the directory is empty. If there are any files in the directory, you will recieve an error. That's Linux's way of keeping you from stepping on your own toes and deleting files you didn't mean to. There is a way around this, hidden in the ```man``` page. I encourage you to recreate a new directory and put a file or two in it, and try to delete the directory along with it's contents after we are done. 

Similarly, as we showed earlier, ```rm``` can get rid of those identical files in your Documents folder, but can actually do it both at the same time! I'm sure you can figure that out as well... Yes, I know, lazy of me. I'm tired, what can I say.

Again, I encourage you to read those ```man``` pages, play around in your Home folders, and see what you can do. Next time, we will actually take that leap mentioned earlier, and download a file from the internet, and do some manipulation of it's contents. It promises to cover more commands, but actually take less time to read!
