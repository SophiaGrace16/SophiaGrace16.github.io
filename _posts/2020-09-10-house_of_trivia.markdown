---
layout: post
title:      "House of Trivia"
date:       2020-09-10 21:27:46 +0000
permalink:  house_of_trivia
---

## Troubleshooting Answers
I started with a lot of ideas. I thought about focusing on dinosaurs, space, animals, sharks, whales, food, etc. but when looking for an API, nothing sparked excitement. Then I stumbled onto a Trivia API. I LOVE trivia. I have always enjoyed trivia, so when I saw it, I thought, "I can use this to create a mini trivia game!" As I began working through my project, I hit a few speed bumps. One of the last issues I ran into was checking the answer. 
This issue stemmed from the initial format of the question array. The original form of the array looks like this:
```
[{:category=>"Mythology",
  :type=>"multiple",
  :difficulty=>"medium",
  :question=>"According to Japanese folklore, what is the favorite food of the Kappa.",
  :correct_answer=>"Cucumbers",
  :incorrect_answers=>["Kabocha", "Nasu", "Soba"]}]
```
Notice there is no "answers" key/value pair. This meant combining the incorrect and correct key/value pairs. In the code this was done in the Question class, initialize statement:
```
 def initialize(category,difficulty,question,correct_answer,incorrect_answers)
        @question = question
        @difficulty = difficulty
        @answers_arr = []
        @correct_answer = correct_answer
        @incorrect_answer = incorrect_answers
        @answers_arr << correct_answer
        @answers_arr << incorrect_answers
        @@all << self
```
Originally after this, back in the CLI class, I called on the answers_arr to shuffle the answers and then print them with their index. I did this to avoid predictability; a game is no fun if the answer is always in the first spot. The original code read as follows:

```
Question.all.first.answers_arr.flattenshuffle.each.with_index(1) {|answer, index| puts "#{index}. #{answer}"}
```
At first, this worked perfectly, or at least I thought it did. Until I realized there was no way to check the answer anymore because the answers are in random order. My first thought was I could have the user enter a word answer instead of an index. Then I recognized that this would allow more room for error. I then refactored the code as follows: 
```
answ = Question.all.first.answers_arr.flatten       answ.shuffle.each.with_index(1) {|answer, index| puts "#{index}. #{answer}"}
        user_answer = gets.chomp.to_i-1
```
Setting the flattened array to its own variable creates a saved predictable order of the answers(correct answer, incorrect answer, incorrect answer, incorrect answer). Using the answ variable I will check to see if the array position is [0], if it is 0 then it is correct, if it is 1,2,3 then it is incorrect. However, that logic was flawed. I needed to compare TWO arrays' values: the ordered array (answ) and a shuffled array. This lead me to the solution below:
```
answ = Question.all.first.answers_arr.flatten
    answ_shuffle = answ.shuffle.each.with_index(1) {|answer, index| puts "#{index}. #{answer}"}
    user_answer = gets.chomp.to_i-1
    binding.pry
    if answ_shuffle[user_answer] == answ[0]
        puts "Correct!!! Good job!"
    else answ_shuffle[user_answer] != answ[0]
        puts "Sorry, that's not right! The correct answer is #{Question.all.first.correct_answer}"
```
This code finally worked the way I intended! I was officially close to the end of my project, and I was ecstatic! I continued working and extending the code to do more things. I ended up with a mostly working, but lengthy, aaq method:
```
def aaq
        Question.all
        puts "Difficulty: #{Question.all.first.difficulty}"
        puts "Your question is... #{Question.all.first.question}"
        puts "Choose an answer below, then enter the number you think is correct!"
answ = Question.all.first.answers_arr.flatten
    answ_shuffle = answ.shuffle.each.with_index(1) {|answer, index| puts "#{index}. #{answer}"}
    user_answer = gets.chomp.to_i-1
    binding.pry
    if answ_shuffle[user_answer] == answ[0]
        puts "Correct!!! Good job!"
    else answ_shuffle[user_answer] != answ[0]
        puts "Sorry, that's not right! The correct answer is #{Question.all.first.correct_answer}"
end
        puts "Play again?"
        menu
        puts "To exit enter 'exit!'"
end
```
The method was mostly working, but it was lengthy and created a looping error. After hours of tinkering, I realized that I shouldn't have tried to tack on the play again sequence to this method. I didn't like that my aaq method had become a lengthy monstrosity, so I created a new_game method, and broke apart aaq into aaq and check?:  
```
 def aaq
        Question.all
        str=Question.all.first.question
        new_str=str.gsub("&quot;",'"').gsub("&#039;","'").gsub("&amp;","&")
        puts "Difficulty: #{Question.all.first.difficulty}"
        puts "Your question is... #{new_str}"
        puts "Choose an answer below, then enter the number you think is correct!"
    end 

    def check?
        answ = Question.all.first.answers_arr.flatten
        answ_shuffle= answ.shuffle.each.with_index(1) {|answer, index| puts "#{index}. #{answer}"}
        user_answer = gets.chomp.to_i-1
        if answ_shuffle[user_answer] == answ[0]
            puts "Correctomundo! Good job!"
            correct
        else answ_shuffle[user_answer] != answ[0]
            puts "WRONG. The correct answer is #{Question.all.first.correct_answer}."
        end
    end  

    def new_game
        puts "Do you want to play again?"
        puts "Please enter Y or N"
        input = gets.chomp.downcase
            if input == "y" 
            Question.reset
            list_categories
            menu
            elsif input == "n"
                puts "Questions too hard? That's okay... you can always comeback later!"
                exit
            else 
                puts "Your answer disappeared into the oblivion. Try again. "
                Question.reset
                list_categories
                menu
            end
    end
```
I am very proud of how these methods came out. I will continue to try and refactor them and better my code. 
P.S. In the meantime, my boyfriend is obsessed with the game!



