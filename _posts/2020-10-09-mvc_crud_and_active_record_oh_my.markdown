---
layout: post
title:      "MVC, CRUD, & Active Record Oh My!"
date:       2020-10-09 18:20:17 +0000
permalink:  mvc_crud_and_active_record_oh_my
---

## My Dungeons & Dragons Database

As I continue on my journey through Ruby, I have enjoyed learning about how the methods that I was so meticulous about, in the beginning, are such a natural part of Active Record. Active Record opens up a world of possibilities because instead of writing out the basic methods, they are built-in. That leaves our busy coding minds to freedom to dwell elsewhere. My mind found CSS, HTML, and CRUD. The first two are fun; you get to change how things are designed and make something beautiful (almost putting on a web designer hat). But the latter of the three is fun in its own way. It is the roadmap for making your application work. I like to think of my application as an orchestra. CRUD, create - read - update - delete, is the maestro; without it, the code wouldn't know what to do or where/when to do something. The database is the sheet music, its what gives everyone else something to do. MVC, models-views-controllers, are the orchestra (plus CRUD as the maestro) are what make the data come to life and makes everything interact, just like the players in an orchestra do. CSS and HTML create the stage; they make the show beautiful. It all comes together to make a masterpiece. All pieces are equally important; one is never more significant than the other. The maestro - the CRUD, however, is the most interesting to me. 

### CRUD - Create, Read, Update, Delete

CRUD is simplistically beautiful. I began by mapping out my routes, visualizing the different tasks I needed CRUD to handle. 
```
##RESTFUL ROUTES

HTTP
VERB         | ROUTE                                    | ACTION
-----------|-----------------------------|----------
GET            | /CHARACTERS                    | INDEX     - SHOWS THE CHARACTERS INDEX
GET            | /STORIES                               | INDEX     - SHOWS THE STORIES INDEX
GET            | /CHARACTERS/:ID             | SHOW      - SHOWS THE CHARACTER
GET            | /STORIES/:ID                        | SHOW      - SHOWS THE CHARACTER
GET            | /CHARACTERS/NEW        | NEW       - SHOW THE NEW FORM
GET            | /STORIES/NEW                   | NEW       - SHOWS THE NEW FORM
GET            | /CHARACTERS/:ID/EDIT  | EDIT      - SHOWS THE EDIT FORM
GET            | /STORIES/:ID/EDIT             | EDIT      - SHOWS THE EDIT FORM
-----------|-----------------------------|-----------
POST         | /CHARACTERS                    | CREATE
POST         | /STORIES                               | CREATE
DELETE    | /CHARACTERS/:ID             | DELETE
DELETE    | /STORIES/:ID                        | DELETE
-----------|-----------------------------|-----------
PATCH      | /CHARACTERS/:ID              | EDIT
PATCH      | /STORIES/:ID                         | EDIT
```
I relate this to a maestro taking notes in the margins of his music. When does he want crescendos, pauses, various sections to lower, etc. A programmer does the same; we are organizing the data and the flow of a website. The routes grow and change, beginning simplistically, go here do this. Then they evolve to involve user permissions or if/else relationships. My paths grew and changed as I found different things that I needed the routes to do.  Here are a few:
```
   get '/characters' do 
        redirect_if_player_not_logged_in
            @characters = current_player.characters.all # shows the index of characters
        erb :'characters/index'
    end

    get '/characters/new' do
        redirect_if_player_not_logged_in
        erb :'characters/new'
    end

    get '/characters/:id' do 
        redirect_if_player_not_logged_in
        @character = Character.find_by_id(params[:id])
        erb :'characters/show'
    end

    get '/characters/:id/edit' do
        redirect_if_player_not_logged_in
        @character = Character.find_by_id(params[:id])
        if @character.player_id == current_player.id
            erb :'characters/edit'
        else
            redirect to "/characters"
        end
    end

    post '/characters' do
        character = Character.new(params)
        character.player_id = current_player.id
        if character.player_id == current_player.id
            character.save
            redirect to "/characters/#{character.id}"
        else
            redirect to "/characters/new"
        end
    end

    #not saving to player

    patch '/characters/:id' do
        @character = Character.find_by_id(params[:id])
        params.delete("_method")
        if @character.player_id == current_player.id
            if @character.update(params)
                redirect to "/characters/#{@character.id}"
            else
                redirect to "/characters/new"
            end
        end
    end

    delete "/characters/:id" do
        @character = Character.find_by_id(params[:id])
        if @character.player_id == current_player.id
            @character.destroy
            redirect to "/characters"
        else
            erb :"welcome"
        end
        
    end  
```

CRUD is what makes the application work. From displaying the welcome page to signing up a new user. The CRUD, MVC, HTML, CSS, all of it. It all comes together to make one beautiful song. One beautiful performance.
