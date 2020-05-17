---
layout: post
title:      "Not a Simple Walk in the Park..."
date:       2020-05-17 03:41:25 +0000
permalink:  not_a_simple_walk_in_the_park
---


Our first project after the first mile was a CLI project. A CLI is a form of UI; instead of being graphical (GUI) following with the attributes of WIMP (Windows, Icons & Mouse Pointer) the CLI is a command line terminal program. I have previous experience with creating CLIs and have a fondness for their simplicity.

My initial idea was making a program where you would list the alcohols you have, and it would pull from a database to find what ingredients you could buy at the grocery store to make drinks with those alcohols. However, this idea was barred from use because it was the idea that our professor used to demonstrate CLI programs. 
My next thought would be a program that would help the user find upcoming movies, and top 10 movies of the past based on genre. So horror fans like me can find upcoming horror films, and good ones that I may not know about. This idea didn't pan out because the APIs I found weren't organized by genre and were very limited. My next interest would be finding parks!
I know that governments tend to have databases that they make available to the public, and with that knowledge I found that the National Park Service has an API that fit my needs precisely. Despite my previous experience with CLIs I found that learned a lot more from this project while doing it. 
Some interesting things I've tried for the first time was using the program to download data via a provided API. This is an awesome function that allowed my program to be versatile; instead of just relying on data I've downloaded it can download data based on what the user required. Additionally, I created some (*I think*) ingenious functions including downloading the required data and saving it locally on the system as a .json. The next time the program is executed, if the user picks a state they've previously inquired about, the program will check the cache first before pulling information from the internet; which not only provides faster performance but also saves bandwidth by not unnecessarily downloading the same data over and over. Another fun function I did for the first time was pretty formatting with my function `pretty_output(long_sentence:, line_width:)` which would accept the parameters of a long description, and how wide the output should be. This would make the description fit nicely in the borders without spilling out of the sides for long descriptions. This method would split the description word by word, count each character in the word including any punctuation and whitespace characters and make sure that no line expands past the `line_width` dimension. All of these functions weren't required, but were more for user experience and a fun idea to implement.

Every time I code it feels like some sort of Rorschach Ink Blot, never the same--always unique, something new tried, some creative idea explored resulting in a program I am proud to show off to nobody but myself.
