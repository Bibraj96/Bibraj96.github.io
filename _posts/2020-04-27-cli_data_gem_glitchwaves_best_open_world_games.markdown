---
layout: post
title:      "CLI Data Gem: Glitchwave's Best Open World Games"
date:       2020-04-27 14:23:47 -0400
permalink:  cli_data_gem_glitchwaves_best_open_world_games
---


For so many around the world, the COVID-19 pandemic has altered normal daily life. Among these changes, exploration has been halted entirely. To remedy this, one might turn to the great expanse that is an open world video game. However, video games are quite expensive nowadays. Sifting through the countless games in this genre to pick one that is worth the money can prove difficult. For my first project, I built a CLI data gem that scrapes the top 40 open world games from [Glitchwave](https://glitchwave.com/), an online collaborative metadata database of video games, and returns its release year, total number of ratings, and numerical rating out of five.

![](https://i.imgur.com/xVQctng.png)

After the necessary, and sometimes tedious process of installing and setting up a gem, it was time to build. To start, I knew I would begin with three initial classes: CLI, Scraper, and Game. Establishing the logic of the CLI class was daunting at first. Case statements for the user's input proved useful here. Assigning each responsibility to one method and filling each of them up with pseudocode was crucial for me. It gave me an idea of how the CLI would flow before I even did any real coding. In fact, this made the actual coding and scraping processes go smoother because I knew exactly what I was looking for.

Next up was the Game class. This was relatively straightforward, it's a class that has:

* An empty array, @@all
* An #initialize instance method which only initialized with a name attribute at first (more added in the Scraper class)
* A #self.all class method which scrapes data only if the @@all array in the Game class is empty
* A #save method which adds "self" to the array, invoked in the #initialize method

The last, perhaps most difficult part, was the Scraper class. The reason I had some trouble with this class is because I wasn't sure if I needed to create new classes for the rating, total ratings, and release year. While I could've done that, it certainly would've added unnecessary work, like building object relationships. The best way to build it was to create these as attributes for my game class, and initialize a new game with these attributes at the end of the #self.scrape_games class method. This is how it came out:

```
class TopOpenWorldGames::Scraper
  
  def self.scrape_games
    doc = Nokogiri::HTML(open("https://glitchwave.com/charts/top/game/1800-20199999/g:open-world/"))
    
    games = doc.css("div.chart_card")

    games.each do |g|
      name = g.css("div.chart_title a.game").text
      rating = g.css("div.chart_card_score").text.strip
      num_ratings = g.css("div.chart_card_ratings b").text
      release_year = g.css("div.chart_release_date").text
      TopOpenWorldGames::Game.new(name, rating, num_ratings, release_year)
    end
  end
end
```

After completing this first project, however simple it might be to some, was still gratifying. After having to pass someone else's tests for all of the labs prior to the project, it felt fulfilling to build my own personal idea from the ground up and tweak it until it finally worked. I'm excited to learn how I can make it even better in my upcoming project review. 
