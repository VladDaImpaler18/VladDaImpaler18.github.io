---
layout: post
title:      "Every Step Matters!"
date:       2020-11-30 04:31:05 -0500
permalink:  every_step_matters
---


This module's project is a utility program, that is used for data entry. The program marries my knowledge of JavaScript as the frontend, and Ruby on Rails as the API backend. My data entry program is for my future project.
The logic goes as follows, A category has many questions. The Question model consists of a question, an answer, and an array of at least 3 incorrect answers (dummy answers), a diagram caption, and what Category the question belongs to.
I wanted to allow a flexible amount of dummy answers so that the user can increase the variety in the wrong answers pool, particularly combined with class function Question.pickDummies(x). 
```
pickDummies(requiredNumber = 3){
        const chosenQuestions = [];
        let questionPool =  [...this.dummy]
        if(requiredNumber > questionPool.length){ return console.log(`Not enough questions to fulfill ${requiredNumber} questions`);} //make a throw and catch exception
        const pickRandomly = (array) => {
            return array[array.length * Math.random() << 0];
        };
        while(chosenQuestions.length < requiredNumber){
            const randomQ = pickRandomly(questionPool); // => "this answer is a dummy answer."
            const pickedQ = questionPool.splice(questionPool.indexOf(randomQ),1); //finds index of the above result, and splices 1 out, returning the one removed
            chosenQuestions.push(randomQ);
            //console.log(`chosen length = ${chosenQuestions.length}`);
            //console.log(`original array = ${this.dummy.length}`);
        }
        return chosenQuestions;
        
    }
```		
One important part of this function if the line `let questionPool = [...this.dummy];`. The \(...\) is called the spread operator and if we were to simply directly equate questionPool with the array in this.dummy, so `questionPool = this.dummy`, then when we modify the questionPool that will destructively change the original array! The spread operator allows us to essentially clone the dummy pool, so any changes done to the clone will not affect the original. This can be seen in console if the `console.log(...)` commands are uncommented. What this function does is simply, it requires a parameter to represent the number of incorrect answers (default is 3), clones the pool of incorrect questions, and then will randomly choose from the pool of dummy questions until the requiredNumber has been achieved. Each time a question is chosen from the dummy pool it is removed for efficiency and to further prevent duplicates. Lastly the function returns the desired array of dummy questions.

By now I should mention that the JavaScript class object recognizes the structure { question: string, answer:string, dummy:[,,], category:string, diagram_info:string }, and we know that similarly, Ruby recognizes the model to have the strings attributes, but how does my Question model know that dummy is an array without it being a separate model, and **even more curious** how do we store it in our database as an array when with sqlite3 we mainly only have `TEXT`, `STRING`,` BOOLEAN`, `INTEGER`, `DATETIME`, and the like. There is no ARRAY datatype in sqlite3. To accomplish this I used ActiveRecord's classmethod serialize `serialize(attr_name, class_name_or_coder = Object)`. By including this class method it allows me declare an attribute that can be saved to the database as an object and retrieved as that object.

```
class Question < ApplicationRecord
    belongs_to :category
    serialize :dummy, Array
    has_one_attached :diagram

    validates :question, :answer, presence: true
    validates :question, uniqueness: true
    validate :must_have_3_dummies

    private
    def must_have_3_dummies
        if dummy.count < 3
            errors.add(:dummy, "At least 3 incorrect questions required")
        end
    end
end
```
As seen in my Question model I used the line `serialize :dummy, Array` to let ActiveRecord know that the :dummy attribute is an Array object. I also used validations to make sure that there is always a :question, and an :answer. In addition I created a custom validation `:must_have_3_dummies` that requires that the :dummy array has at least 3 choices.
My categories question is simple, but plays an important role for the API backend.
```
class Category < ApplicationRecord
    has_many :questions
    attribute :questions
    validates :title, presence: true
end
```
The line `attribute :questions` plays an important role when combined with the render jsoncontroller's action 
```  #category#action
    def index
        categories = Category.all
        render json: categories, except: [:created_at, :updated_at]
    end
```
Without the attribute line our get request JSON would only have the basic information `[{"id":1,"title":"Ecology"},...]` but with it ActiveRecord will also include the category's question(s) and provide much richer data
```
[{"id":1,"title":"Ecology","questions":[{"id":2,"question":"Which relationship best describes the interactions between lettuce and a rabbit?","diagram_info":null,"answer":"producer — consumer","dummy":["predator — prey","parasite — host","decomposer — scavenger"],"created_at":"2020-11-04T05:57:07.895Z","updated_at":"2020-11-04T05:57:07.895Z","category_id":1}, ...]}, ...]```
From this we can use a GET fetch request to get all the Categories, and add Questions for those categories all in one swoop.
