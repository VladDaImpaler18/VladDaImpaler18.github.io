---
layout: post
title:      "Coding, Campfires, and CUTE PUPPIES"
date:       2020-07-27 21:25:37 -0400
permalink:  coding_campfires_and_cute_puppies
---


What does coding, campfires, and **cute** puppies have in common? Normally nothing, but for me this project involved all three.

#### Coding
This project involved using Sinatra and ActiveRecord to create a website with RESTful logic, and a Model, View, Controller structure. It was time consuming, laborous, and *a whole lot of fun.* I started things by mapping out the route that each link could take you to. Figuring out what I wanted users to be able to do, what they shouldn't be able to do, and how to make it practical. During my coding sessions I kept coming up with cool ideas, something to try, see if it works and *that* is the reason why I think this is my best work.
It includes a CLI, which was our first project. When first accessing the website there is a check to see if the environmental variables are set. If the value `ENV["ADMIN_USERNAME"]` doesn't exist, then no admin username has been set and an instance of the `AdminCreator` class is created and started. `AdminCreator` class involves setting an admin username and password. Another cool idea is adding a salt to picture's filenames in order to prevent any user from overwriting another's picture of the same name. The salt is created using the `random-word-generator` gem. To create the salt it requires the number of words and maximum characters used in the salt. Conviently, `AdminCreator` also requests the user to input the number of words and characters to be used in the salt, and includes a method `quality_check(words:, letters:)`. The quality check method will check the integrity of the words:characters ratio to prevent any poor qualty salt words. Another method in `AdminCreator` is `write_env_file(num_of_words:, num_of_characters:, admin_username:)` which can be expanded and used to save variables required throughout the website. My project also includes complex relations. `Owners` has_many `Pets`, and `Pets` has_many `Pictures`. 


#### Cute Puppies!
I had recently adopted a cute puppy, which we named Mako, and his sister Luna, who was adopted by our housemate. These puppies have been given the title of "the world's best time wasters". Having a puppy takes a lot of work, and a bit of a life adjustment. No longer could I follow my own schedule when something so small and cute depends on me and takes attention on demand, my work time was hit and I fell behind. This project was time consuming and took me to the last week but I refused to cut corners or just make a project to  achieve the minimum. This project is art, and i'm proud of this achievement. I've learned so much and it shows in my work. I dedicate this project to Mako, my cute puppy who is the best time waster, a professional greeter and puts a smile to my face everytime I see his huge doggy smile and entire body wag when he sees me.

#### Campfires
How do campfires figure into this? Well being behind schedule I had to cut what little social activities I had to get work done on my project. I missed out on hiking adventures, rock climbing adventures, but I did decide to still go to our two traditional camping trips. During the day we camped and at night we sat around the camp fire. Me being a night owl I was always the last one up so, why not code in front of the camp fire. It was a picturesque moment, the cool night, warm fire and nothing but nature in the background--if you haven't experienced it I would recommend it. If you're reading this and decide to check out my project, I hope you enjoy playing around with it as I enjoyed making it.

