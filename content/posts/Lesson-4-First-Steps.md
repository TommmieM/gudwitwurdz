---
title: First Steps - The Curse of Choice
date: "2023-04-02"
author: "Tommie Matherne"
tags: ["Python", "Project", "CYOA"]
keywords: ["Python", "COYA"]
description: "Now that we have a skeleton of a project needs, we have to decide what to build first. We will introduce the concept of a Minimal Viable Product, and how to use it to drive your decisions from beginning to end."
showFullContent: false
readingTime: true
hideComments: false
color: ""
format: hugo-md
---

## How To Decide Where To Start

In our last meeting, we discussed what would go into making a digital version of an RPG game book and what Python concepts need to be learned in order to create it. Hopefully, I also made it apparent that this is a skeleton, not the entire plan. Things will come up, you will never create a 100% plan at the outset. So don't try to do so. Make a basic outline of what you plan to put together, and how it will look and work, and then work forward from there.

After this skeleton is completed, though, a realization usually hits most new programmers working on their first project. "Where do I start?" This is another freeze point for a lot of folks. You know the pieces are relatively simple to break down, and a rough idea on how to make them fit together, but how to begin creating to make it a project that is cohesive is difficult when just looking at the skeleton. This is when you have to decide what is your Minimal Viable Product?

## Minimal Viable Product

A MVP is the least work you can do that can provide at least the basics of the functionality core to the end product you want to produce. In total, what we are looking to build would be an interactive story with branches built into the story that the character can proceed through while gathering items, talents, magic, and other items to affect the branches that are open to us. 

At minimum, we need to be able to create a story that has branches that the user can choose without any extras. So our MVP looks a lot like a Choose Your Own Adventure. This is both why I didn't choose a CYOA as the project, and what our first step is in the building of the final product we want to produce. 

All we need to accomplish this is to produce text in terminal, print our choices, accept user input, parse that to determine the choice, and call the next part of the story up depending on the choice made, and print that choice and repeat the process. To do this, we will need the following Python features:
* the ```print``` statement. A very powerful feature of Python, basic as they come, but used daily by even the most seasoned Python developer.
* Python ```functions``` to control what gets printed to the screen next based on user input. 

Some other features that we are going to use, not necessarily pertinent to the completion of this project, but pertinent to being features used in a Python project:
* ```if __name__ == "__main__":``` The entry point to Python work. This is so that your file is accessible as a standalone script as well as an importable module. Any Python work can be imported to another Python file. This allows a way of beginning execution, but is not really necessary. Python will execute scripts from top to bottom as it is not compiled, but interpreted at run time. While this is not really needed, it also serves to provide you with a way of knowing where execution begins in order to evaluate the program if you leave it and come back after a time. 
* ```import``` statements. Not usually covered in beginning Python books or tutorials, imports allow you to pull in code from outside the current file and work with it. We will be doing this with our own code, but this also applies to libraries outside the Python Standard Library.

I'm sure there will be more, but we will get to it as we go along.

## Let's Code!

I'm sure everyone has heard of "Hello World!". The quintessential first program. Not only used to show absolute newbies that they can indeed "do this", but frequently the first program written by veterans working with a new system because it can show you that your toolchain is properly set up simply by being able to execute. 

With Python, this second reason is not that important for our purposes. We can prove that our toolchain is set up simply by typing ```python``` at our command line. If we get a Python input, we have all the toolchain we need. 

Instead, I'm going to use a slightly less well-known simple introduction for newbies. One stolen from tabletop role playing. When introducing new players to fantasy role playing, we frequently introduce the basic rules by running a player through the Cake Adventure. The adventure is the smallest complete quest possible, or at least that I've ever seen. The player is told of a cave nearby that is rumored to have a treasure that is guarded only by a single goblin. Upon arrival, said goblin is found, defeated, and the treasure is found to be a piece of cake. The player gets familiar with the basic rules and flow of the game, gains a few experience points, and has a tasty treat!

Let's adapt that for our first game. Properly structured, it gives us a story that is short, but can branch, as well as have multiple endings (no, we aren't going to kill the player! Bad designer!)

To begin, we need to create our folder structure to hold the files we are working with. Go ahead and create a new directory in your Home named "Cake" and ```cd``` into it. Once there, use ```touch``` to create a new file named ```cake.py```. You can use any editor of your choice to actually write this file, I'm not going to judge. Personally, I am using vim. It is not the easiest editor for new programmers, but well worth learning. I'm going to leave you to figure it's use out if you decide to use it, a tutorial seris on vim would be overblown from our scope here. Like I said, use whatever you feel comfortable with, but eventually, learning vim is something I highly recommend if for no other reason than its ubiquity.

Once you have that blank file open in your editor, let's add some text to turn it into a Python program.

```{python}
#! /bin/python3
import story

def choose():
    choice = input("""Do you want to: \n 
    1. Draw your sword and lantern and to in! \n 
    2. Go home. \n""")
    return choice

def decide(choice):
    if choice == '1':
        story.proceed()
    elif choice == '2':
        story.home()
    else: 
        print("Sorry, I didn't understand. \n")
        choice = choose()
        decide(choice)
        

if __name__ == '__main__':
    print("CAKE ADVENTURE!")
    print("""
    You were having dinner in the town tavern when you overheard a rumor 
    of this cave containing a treasure guarded only by a single goblin. This is 
    your chance! You have been wanting to prove that you are fit for the life of  
    an adventurer, and if you can get this treasure, no one can doubt you! \n """)

    choice = choose()
    print(choice)
    decide(choice)
```


Save and exit, and once back to your command line inside your Cake folder where this resides, you can ALMOST run it. If you type in ```python```, you will get an error that says something along the lines of "failed import, module story does not exist". We are going to ignore that for now because we are not done yet. But we will go line by line here and figure out what we have written.

The first line is ```#! /bin/python3```. This is known as a "shebang line". On non-Windows systems, this tells the operating system where to find the way to run this program if file permissions say it can be executed. On Windows systems, it just acts like a comment line and has no effect. 

Next we ```import story```. This looks first in our operating folder, in our case Cake, for a file named 'story.py' and makes that part of the current program. Anything in that file will be recognized as valid code in this program. Since we haven't yet made that file, this import will cause an error as mentioned above. We will get to that momentarily.

```def choose():``` creates a new local function named 'choose'. The ```def``` keyword in Python says we are defining something outside of the Python Standard Library that we want to be able to call and reuse over and over if need be. This isn't going to be our only 'choose()' function, as we will need different choices each time. I put it here to show you how to define a function, what it looks like, and what it does.

Then we define another function, ```decide(choice)```. This one is a bit different. It has something in the parentheses. Why? Because we are declaring that we want to have information before calling this function. We store it in a variable that the function will know as ```choice```. Inside the function, we can write code that references this variable, and not have to declare it or assign it a value. That value comes from the part of code that calls it.

Inside this function, we immediately see another new item, the ```if``` statement. This makes a yes or no decision in Python. The bit between ```if``` and the colon is known as a "conditional statement", or a "Boolean statement". This will take two things, in this case a variable, ```choice```, and a string ```'1'``` (make sure this is a string, the ```input()``` function returns a string, and you cannot compare strings to numbers in Python. Well, you can, but it isn't what we want.) This then evaluates to one of two values, the Boolean values of ```True``` or ```False```. If ```True```, the code indented below the ```if``` is executed, if ```False```, that code is skipped.

IMPORTANT NOTE: You may have noticed a difference between areas of the code that have ```=```, and the conditional statements having ```==```. There is a powerful difference between these two. When Python sees a single ```=```, it is expecting to assign a value to a variable, will look to the right of that equals sign first, evaluate anything there until there is only one value, and then assign that value to the variable name located to the left of the ```=```. BUT, if Python sees ```==```, this is known as the equality operator, and Python will take the left side first, store its value, look at the left side, store its value, and then compare the values to see if they are identical. If they are, Python returns a ```True``` value, and if they are not, Python returns a ```False``` value. 

But what if you want to make a choice to do different things if something else if ```True``` about the code? Enter ```elif```! While this may sound like a fantasy creature with a speech impediment, it actually stands for ```else if```, and allows you another choice. In this case, the conditional statement ```choice == '2'```. Then it treats the indented code beneath exactly as a normal ```if```. There is also no limit to the number of ```elif``` clauses you can include beneath an ```if```, so if you write a story that reaches a point with three or more branches are possible, you can check for each branch with ```elif``` under ```elif```.

Notice below these, there is an ```else``` sitting there with no conditional statement. The ```else``` is a catch-all. It covers your bacon if you have something that you want to do if none of the expected conditions covered in your ```if``` or ```elif``` clauses were ccaught. It allows you to do something in that case. So what do our clauses do? Let's cover those one by one...

With our ```if```, when a player chooses to enter the cavern, it goes to our ```import```ed file, ```story.py``` (which we haven't created, yet), and looks for a function named ```proceed()``` to be executed. Our ```elif```, similarly, looks to ```story.py``` for a function named ```home()``` and executes it.

But what if the player enters something we don't cover with a function? under the ```else:``` you can see that we apologize (treat your readers/players with respect), then go back to the ```choice()``` function. Then we do something really freaking strange. We... call... the function we are in, ```decide(choice)```... from inside ```decide(choice)```? Is that allowed?

It totally is! In fact, this is an important programming concept called "recursion". Calling a function from inside itself makes it possible to perform any action with repeated steps by only calling the function once in code, but running that step as often as needed to complete the task. In our case, we have it easy, we only need ```decide(choice)``` to recur until our reader/player plays ball and gives a valid answer.

Notice, this is at the top of the file. I have said before that Python executes from the top of the file down. Later, when all the peices are in place and no errors return, you will notice that when you run it, this will not actually print anything to the screen. Also, you may be questioning why this is first, if Python goes from the top of the file and goes down, and I also said that ```if __name__ == '__main__':``` is the entry point of file execution. 

All of these things are true. Python is reading from the top down, and execution hasn't strictly started yet. All of this part is just defining things for Python to keep in the background for later reference. So what are we wanting to store for later reference? our next line is a ```input("")``` call. ```input()``` is a Python function that will print whatever you put in the parentheses (known as an "argument"), print it to the screen, then give a input to the user and pause all execution of the program until the user types in something and presses enter.

Some notes about the text string inside the parentheses for this particular ```input```:
* Note the triple quotes. Python will recognize this as a multi-line string. You can break up the text by pressing enter in your text editor if you need to, and Python will still treat it as a continuous line. For long strings like a story, this is useful.
* The '\n' areas are what is known as "escaped characters" in Python strings. These do not print to screen as they are presented, but do something different. These in particular are "new line" characters. When you see a '\n', Python will enter a line break in the terminal output. This keeps things looking nice for your presentation. 

Then we are storing a way for decisions to be made upon that ```input()```, if needed, ```input()``` our player again, and make that decision all over. Python will keep this in mind for us, our work is done.

Whew, we have finally made it to our actual program! ```if __name__ == '__main__':```. This is going to be the first things our program apparently does when we run it. So what do we do with it? This is rather short:

```print()``` functions act much like ```input()``` with the difference being that once it reaches the end of the string passed to it as an argument, Python just continues execution of the program. So why do two ```print()``` calls rather than just one and put everything together? Honestly, you could. I just wanted to have only the name of the story-game on the first printed line, and then begin printing the story itself. 

After the story is presented, we have both our first variable declaration, and our first call to a function that we defined. The program, at this point will call the ```choose()``` function, execute it as described, and then store that value (the input string from the user), in the variable named ```choice```. This flow of execution is important to keep in mind!

When you see a variable being assigned a value in Python, the interpreter will look at what is AFTER the ```=```, or assignment operator, execute that if needed to arrive at a value. Only after that execution has completed, will the variable be stored in memory and point at the value derived. 

So, now that we know what is going on in this file, lets complete our program. Back in your Cake folder, create a file named, of course, ```story.py```. We know of two functions that will need to be included, ```proceed()``` and ```home()```. Will there be others? Yes, there will be. In fact, this is how it looks for me. If you want to branch your story more, feel free to follow the patterns established and expand your story as much as you want.

```{python}
#! /bin/python3
#! /bin/python3

def fight():
    print("""Well, this is what it came down to! What you \n
    kind of hoped for. But you didn't think it would be this... \n
    Intense! \n
    \n
    The goblin obviously doesn't have a sense of its own \n
    mortality as it comes across at you with a dinner knife. \n
    By the time it dawns on you that the only treasure it owns \n
    is the cake on the table, and that the cake means more to this \n
    creature than it really does to you, there is a dull slice \n
    from the knife under the armor flap near your wrist! \n
    \n
    It wasn't really much of a battle. A few parries to avoid \n
    any more scratches from its dulled dinner knife, and one \n
    good cut on your part puts the goblin down. You decide to \n
    try the cake anyway and see for yourself if the goblin was \n
    THAT out of its mind. You'd recognize your aunt's baking \n
    anywhere. You kind of get it. No idea how the goblin got a hold \n
    of it, but there are doubtful to be any goblin bakers quite \n
    like her! \n
    \n
    You go back to town with your story, and a bit of frosting \n
    on your lip for evidence. That is how your adventuring career \n
    begins, with little fanfare, no actual treasure, but a lot \n
    of local reknown that you will continue to turn into more adventure. \n
    \n
    The end, hero!"""
    )

def bargeIn():
    def choice():
        decision = input("""what do you want to do? \n
        1. FLEE! \n
        2. FIGHT! \n""")
        return decision

    def branch(decision):
        if decision == '1':
            home()
        elif decision == '2':
            fight()
        else:
            print("Sorry, I don't understand. \n")
            decsion = choice()
            branch(decision)

    print("""Throwing the detritus that passes for a goblin door \n
    you enter a small chamber. Before you on a table is a \n
    single bare candle throwing a dancing light around the \n
    room. Also on the table is a fine looking slice of cake. \n
    \n
    Opposite you from the table, sits a chair that contains \n
    an goblin that is apparently angry at having its dessert \n
    interrupted! \n
    \n
    It drops its fork, but retains the small knife it was holding \n
    and comes around the table at you with a scream!""")

    option = choice()
    branch(option)

def home():
    print("""
    You decide to head home. Honestly, you don't know \n
    what you were thinking. An adventurer? Hunters get \n
    killed by prey all the time, and deer and pigs don't \n
    hold a grudge like a goblin does! \n
    \n
    \t It takes until almost morning to get back home, but \n
    at least your bed is safe. \n
    \n
    The end, you lived.
    """)

def proceed():
    def choice():
        decision = input("""what do you want to do? \n
        1. Turn back. \n
        2. Barge in! \n""")
        return decision

    def branch(decision):
        if decision == '1':
            home()
        elif decision == '2':
            bargeIn()
        else:
            print("Sorry, I don't understand. \n")
            decsion = choice()
            branch(decision)

    print("""
        Drawing your sword and lighting your lantern, you \n
        proceed through the dark maw of the cavern entrance. \n
        \n
        It isn't much of a cavern, but it's shallowness is \n
        hidden from the entrance by a quick cut right in the \n
        passage about thirty yards in. A short way down the \n
        right hand passage, you see a makeshift door constucted \n
        of branches and twigs. Beyond it, you see the dancing light \n
        of a candle.
        """)
    decision = choice()
    branch(decision)
```
We aren't going to go as much into detail in this part as the previous, as there really isn't anything new, just different. First of all, you will likely notice that for the most part, the functions are in reverse order. That is because a function needs to be defined **before** it gets called. If, for instance, you put ```proceed()``` at the top, when the ```branch()``` function calls on ```bargeIn()```, Python wouldn't know what to do with that, as it hasn't gotten to the part of the file that defines ```bargeIn()``` yet.

Speaking of, you may notice that the ```choose()``` and ```decide(choice)``` functions take on new names, change the name of the arguments, or sometimes the variables passed doesn't match the variable name in the function definition. This is to show you that this is **fine**. The names are arbitrary, and variable name consistency only has to be maintained inside of the particular block of code referencing that variable.

For instance, in ```bargeIn()```, I name the function ```branch(decision)```. Inside of the function definition, I stick to referring to the variable as ```decision```. But in the actual area where we call the function to be executed, I wrote the line as ```branch(option)```. This still works. During a function call that requires an argument, you pass in a variable from the code you are working on, and you call it by whatever name it has in that part of the code. Once it actually passes control to the function itself, the variable name essentially gets changed to whatever you named it inside the function, in this case ```decision```, and the code proceeds. 

Additionally, you probably noticed that there are function definitions inside of function definitions! This is called nesting functions. For our purposes, it is useful because we are writing functions with the same name in this file, but the function names have to do different things in each of the outer functions that contain them. By nesting them inside the function that will call them, the inner functions effectively don't exist for any other functions in this file!

For instance, if we call ```choice()``` within ```bargeIn()```, it only sees the function ```choice()``` defined within itself. It cannot know that a function named ```choice()``` also exists inside of ```proceed()``` for example. This is called "scope". Pay attention to the indent levels of the file! If you indent something inside a body block, for instance, after the colon in a function definition, it only exists inside that body. Once indent goes back to the level of it's contained area or more, for instance, a new first level indent function definition, that new first level indent cannot see anything in the previous first level indent's body block. It's out of "scope".

## Conclusion

So, now you know the basics of a lot of advanced Python stuff. We've covered importing external code, how to write that code to be called in, defining our own functions to get things done when Python doesn't have the abilities baked in, making decisions in code with ```if``` statements, inner and outer functions, scope, and even recursion, which is widely considered one of the most confusing things in all of programming!

Take this knowledge, and try to make your own story using this pattern. Have fun with it, that's what coding is all about. 