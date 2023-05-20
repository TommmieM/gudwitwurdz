+++
title = "Side Track Building a Research Database"
date = "2023-05-19T18:02:59-06:00"
author = "Tommie Matherne"
authorTwitter = "" #do not include @
cover = ""
tags = ["python", "database", "pandas", "sqlite"]
keywords = ["research", "database", "python", "project"]
description = "Build a functioning research database using Python, Pandas, and the FRASER API from the St. Louis Federal Reserve"
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

## Bit of a Side Track

Today we are going to focus on something a bit different. A real-world level project. Something that you can copy and work with, and even take beyond what we build here to actually start creating your own resume out in order to get hired and make some money! The best part is, this is actually a rather simple project. It's what you decide to do with it afterwards that will make all the difference in your future.

The building blocks of this project are Python, of course, the Pandas data library, the sqlite3 built-in module for Python. Outside of our actual program, we will need access to the St. Louis Federal Reserve's FRASER REST API. After everything is built, we will draw value out of it using a database viewer. 

For today, we are going to focus on what FRASER is, what it can be used for, what an API is, and why building a database out of the information you can gather using this API is actually something that would apply in the real-world.

## St. Louis Federal Reserve and FRASER

Properly named the Federal Reserve Bank of St. Louis, the [St. Louis Federal Reserve](https://www.stlouisfed.org) is part of the United States Federal Reserve bank system. While the main decisions are made in New York and Washington, D.C., there are several districts across the country with branches of the Federal Reserve posted in order to take the issues distinct to each district into consideration in reports back to the central hubs. All of this is much better described and shown on the ['About Us'](https://www.stlouisfed.org/about-us) page for the St. Louis Fed itself.

A thorough reading of that page shows an interesting bullet point under the 'Our Purpose' heading:

> Advancing economic knowledge, community development, and fair access to credit.

Part of the way that they advance economic knowledge is through the [FRASER program](https://fraser.stlouisfed.org). Through the FRASER site, you can browse around and find current and historical articles and information about the economic history of the United States from 1784 to today. In addition, you can find cirriculum information and lessons aimed at teaching economics from basics to advanced for audiences from pre-school to collegiate levels.

Every bit of this data is accessible from their FRASER REST API, which can be cound in the top menu under the 'About' section, or through [this link](https://www.stlouisfed.org/about-us). Let's take a quick tour of what we can get from this API.

## The Grand Tour

I hope you'll pardon the subtle reference in titling this section. Listening to George Jones right now.

So what is included in the API? Each of the headings includes information on what you need, and how to use the resource to gather that information. After a short overview on what the purpose of the API is, there are immediately instructions on how to request an API key. An API key is used as data passed in your program's calls to the API to let the FRASER website know that you are a legitimate user requesting this information. At a simple level, it can be thought of as a simple way to log into the site for access to information when a program is visiting the site rather than a user. 

The ```curl``` command that is given can be typed into a bash or PowerShell prompt, replacing the email address with your own, of course. If the command is successful, you will see ```{"message":"API key created and sent via email."}``` at your command line, and you will have an email from the St. Louis Fed FRASER project in your inbox that contains your API key. Remember, this is a necessary part of making any call to the API, so don't lose it!

The second bit of information tells you a bit on how to use the key to interact with FRASER. This can be ignored for now, with Python, we aill be using a different method to create a header. Below that, though, do note that there is a limit on the amount of information you can call for within a given time. You are limited to 30 requests per minute to the site. This may seem like a lot, being one request every two seconds on average, but we are doing this with Python. It is easier than you may think to blow through that limit. Because of that, we will actually be making sure we don't by adding in a two second pause in our work. Sometimes, to act reliably, you have to slow down your program!

The table in the next section gives you a short description of the different record types you can request, and what is included within them. Below that, you will come across an interface where you can input your API key. This is because you can effectively use this page to run requests to the server provided and see what the responses will look like. We aren't going to actually program anything today, so I encourage you to try this out and see what kind of data you will be working with in order to create a personal database.

One last thing to keep in mind, is that there are several API requests you can make that include items in curly brackets, such as ```{itemId}``` or {titleID}. To actually make these calls, you need to provide a title or item to be searched. At this time, you can take wild guesses on these identifiers, but there isn't really a way to know what identifier will return what information. This is the reason to create the database. We are going to use a lot of calls up front in order to build a repository containing a searchable record on hand of all of this information so that when you want to do actual research, you can simply refer to your own database to find out what identifier you need, make a few calls, and return the maximum information!

## What to include?

So there is obviously a lot of information here. Storing it all would take more memory than our computer can possibly hold. I mean, we are talking about historical records about the United States of America's economic environment almost since its inception! We can't really do that.

What we can do, though, is make it a lot easier to find out how to call for that information when we need it! For that reason, rather than keep large items, we keep the things that allow us to call for those large items. These are easily realized by simply looking for any API call that doesn't require an identifier. There are only four:

* All author records
* All subject records
* All theme records 
* All timeline records

Don't be fooled, though! This is still a *LOT* of data! I haven't personally created this database myself yet, I'm going to do that along with you next post. However, I am confident that the resulting database will be on the order of a few gigabytes of information, so please ensure you have the space available to store this.

## Next time...

In our next post, we will move into actually creating the Python scripts that we will combine into a program that will request all of this information and store it in a brand new databse for our easy access. In the meantime, as mentioned, acquire your API key, come back to the API documentation page, and make a few requests to see what REST data looks like.
