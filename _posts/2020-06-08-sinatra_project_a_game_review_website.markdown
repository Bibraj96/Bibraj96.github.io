---
layout: post
title:      "Sinatra Project: A Game Review Website"
date:       2020-06-08 14:42:55 +0000
permalink:  sinatra_project_a_game_review_website
---


For my Sinatra project, I decided to stick with the video game theme of my last project and create a simple CRUD app using the MVC (model, view, controller) paradigm which allows users to create, read, update, and delete game reviews. In addition, the app allows users to visit other users' profiles and read their reviews. Demonstrating my project from head to toe would make for an unnecessarily lengthy post, so I'll only convey the main takeaways upon completing this application.

Ultimately, this project proved useful in unveiling what it means to interact with a web app. Despite being a fairly simple app, building it helped me learn the flow of a website behind the scenes. A client makes a request, and the server finds the appropriate route to render or redirect a page with the relevant information. This game of catch continues up until the user's exit point. Fundamentally, it is as simple as that. Take this route for example:

```
  get '/reviews/new' do
    erb :'/reviews/new'
  end
```

* If a client (browser) sends a get request to write a new review, that would be the response that the server would send back to the client. 

* This client is then presented with the form to write a new review:

```
<h2>Write a New Review!</h2>

<form action="/reviews" method="POST">
  <label for="game">Game: </label>
  <input type="text" name="game" value="">
  <br>
  <label for="content">Content: </label>
  <textarea name="content" style="width:auto; height:auto;"></textarea>
  <br><br>
  <input type="submit" value="Create Review">
</form>
```

Now, naturally, the more functionality one adds to the app, the more complex the game of catch becomes. For example, figuring out how to allow a user to visit another user's profile while restricting them from editing or deleting that user's reviews takes some planning out. As a developer it's imperative that you have a strong understanding of the flow of your app in order to implement more complex features. It's easier than you might think to get lost in your own file structure and misunderstand which route leads to which view page. 

Given some more time, here's some functionality I would've tried to add:

* A search bar for users to search for reviews by game title. 
* A comments section for each review.
* More creative styling.

I'm certainly pleased with what I've learned upon building this web app and I'm excited to learn the different ways to improve it in the Rails module. You can check out my project on my [GitHub](https://github.com/Bibraj96/game_reviews).
