---
layout: post
title:      "Debugger and Pry"
date:       2020-12-13 21:34:37 -0500
permalink:  debugger_and_pry
---


One of the pinnacles of coding is learning how to effectively use debugger and pry to debunk any issues in your code. In this blog we are going to look at the pros and cons of using debugger and pry. 

### Pry

Pry is a gem that can quickly become an integral part of discovering where your code is going wrong. I utilize it frequently when testing my backend and controllers that work with my frontend. Kicking up pry in an application is pretty easy and user friendly. Your first step is to make sure you have included pry in your gemfile and updating your bundle if your filetree includes a gemfile.lock:

![](https://imgur.com/EVFuaGphttp://)

The arguably tricker aspect of using pry is understanding where to put it and how to interact with it. As a beginning coder, I was fairly intimidated by pry. I didn't fully understand it and didn't recognize how useful it could be; but like any new "tool" the more you use it, the more mastery you gain. 

To call pry in your application you have to insert a ```binding.pry``` into your code wherever *you* think it will be helpful. When developing my Javascript project I utilized pry continuously in my code to see how my objects were being passed in and out. I routinely will place one or two pry's at a time to see how my data looks at different points in my code. For example, in the code below you can see I put it at the beginning and in the middle of my code.

```
def index
**binding.pry**
    if params[:movie_id]
      @movie = Movie.find(params[:movie_id])
      @eggs = @movie.eggs
		**binding.pry**
    else
      @eggs = Egg.all
    end

    render json: @eggs
  end
```
	
I do this for a few reasons, the first of which is because I am still learning how to best use Pry. It helps me to practice pulling data in a few places. If you are well accquainted with Pry, you'll know that the first pry will only show me the *incoming* data. If I were to call @movie in the pry console it wouldn't return anything because we haven't hit that point in the code where those values have been stored. I can test the code ```@movie = Movie.find(params[:movie_id])``` which is why that first pry is helpful, it helps me to work out my syntax to make sure I am pulling the pieces of data that I need. 
When I hit the second pry I can check the stored values since my code is "paused" just have the variables have been assigned. This is a good spot to again confirm that the code is working the way you intend it to. But Pry is just one piece of the puzzle, in order to full work with "debugging" your code, especially when working with Javascript, you also need to utilize *debugger*.

### Debugger

Debugger is a new tool that I am still learning and understanding. I have learned that, like Pry, it can be finnicky depending on where you put it. But I have also learned that it is incredibly important to use when working on debugging your fetches. Below is an example of a fetch that gave me a bit of trouble when I was working throught it.

```
addEgg(e){
**debugger**
        e.preventDefault()
        const neweggMovie = document.getElementById("movie-container").children[0].id
        // capture our form data
        let data = {
            'egg_movie': e.target.egg_movie.value,
            'egg_description': e.target.egg_description.value,
            'image': e.target.image.value,
            'movie_id': neweggMovie
        };
        // write our fetch and send it to our back end
        fetch(`http://localhost:3000/movies/${neweggMovie}/eggs`, {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
				**debugger - attempted here, but it does not work**
        .then(resp => resp.json())
        .then(newEgg => {
            const {id, egg_movie, egg_description, image, approved, found_count, movie_id} = newEgg
            if (approved === true){
            new Egg(id, egg_movie, egg_description, image, approved, found_count, movie_id)
            }
						**debugger**
            document.getElementById('eggForm').reset()
						**debuggger**
        })
      }
```

I dropped a debugger, or attempted to, in multiple places in this code - I have bolded the debuggers above to help you see where I put them. My favorite spots where in the beginning and the end. I found it extremely helpful to, just like in Pry, see the transformation of my data. The debuggers are quintessential to figuring out how to parse your data appropriately or call on different html elements of your code.  In my code this line, ``` const neweggMovie = document.getElementById("movie-container").children[0].id``` gave me quite a spot of trouble. The information was not working with the syntax the way I needed it to, thankfully I was able to use the debugger console to play with the data until my cohort lead and I found a solution that worked! Pry and Debugger can be a powerful combination, make sure you take the time to get familiar with them and practice using them!


