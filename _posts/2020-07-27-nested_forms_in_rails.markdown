---
layout: post
title:      "Nested Forms in Rails"
date:       2020-07-27 18:11:12 +0000
permalink:  nested_forms_in_rails
---


While chipping away at the Rails curriculum, the most significant hurdle was the "Nested Forms" section. It was one of those concepts that simply didn't click with me no matter how much I read about it or watched videos explaining it. It wasn't until I got up to it in my portfolio project, a refactored and improved version of my Game Reviews Sinatra app, that I understood its purpose and benfits.

In my app, a nested form allows a user to create a `Game` and its associated `Genre` (a `Game belongs_to Genre` and a `Genre has_many Games`). First, I started with building the form: 

```
<%= form_for(@game) do |f| %>
  <div class="form-group">
    <%= f.label :title %>
    <%= f.text_field :title, class: "form-control" %>
  </div>

  <p> Choose an existing genre for this game: </p>
  <%= f.collection_select :genre_id, Genre.all, :id, :name, {include_blank: 'Choose a Genre'}, {class: "form-control"}%>

  <p> Or create a new genre for this game: </p>

  <%= f.fields_for :genre do |genre| %>
    <div class="form-group">
      <%= genre.label :name %>
      <%= genre.text_field :name, class: "form-control" %>
    </div>
  <% end %>
	```
	
With this form, I give the user an option to select an existing genre to associate with the game or create a new one. The `<%= fields_for %>` block renders a field for the nested attribute we want to associate. Here, it's the genre's name. Next up, I need to go to the `games_controller`.
	
```
def new
  @game = Game.new
  @game.build_genre
end
```

This `new` action builds a field in the form to accept a new genre.

```
private

def game_params
  params.require(:game).permit(:title, :genre_id, genre_attributes: [:name])
end
```

In my `game_params`, I need to permit the name attribute of a genre or else it can't be submitted. The last step is to go to my model so that I can give my app the `genre_attributes` method.

```
def genre_attributes=(attributes)
  self.genre = Genre.find_or_create_by(attributes) if !attributes['name'].empty?
  self.genre
end
```

This will give me the `genre_attributes` method which finds and existing genre or creates it by the name given. The reason I used my own setter method instead of using `accepts_nested_attributes_for` is because I the setter method prevents duplicates.

When it comes to the tricky topics in this bootcamp, it often helps to just try implementing what you know. From there, you'll hit errors and make mistakes that will help you build on your foundational knowledge of the topic. Applying nested forms to my project, then writing this blog, has helped cement my understanding of this subject. I'm excited to learn more in my upcoming project review!
