---
layout: post
title:      "CLI Data Gem Project "
date:       2019-03-13 03:48:34 +0000
permalink:  cli_data_gem_project
---


### Hello everyone,  my name is Tyler and today I will be sharing with everyone how to create a CLI gem.  This was a project done through Flatiron School to help provide a larger project for our portfolio.

From a young age I have always enjoyed the genre of Epic Fantasy.  Anything that had an imaginative plot captured my attention entirely.  So, for this project, in a field where I take enjoyment from learning, I thought I would pick a subject that I enjoyed talking about.  EA just released a game called Anthem that I had had my eye on for quite a while, so for me it was a no brainer to create a CLI gem on the "robot suits," or javelins.

This was a relatively simple scraper that takes the list of current javelins from the EA website and lists them out.  If you wish for additional information such as play style you just have to type in the name of the javelin and all the information will be made available to you.  It's a quick and easy way to do research on the game to prepare yourself to dive in to this immersive game.

So here is a quick run down of how I built my CLI Gem.

#### 1. Install Bundler Gem

The quickest and easies way to create your ruby gem is to enter the below command  


`bundle gem <name of your project>`

#### 2. Make your BIN file executable

To do this, you need to create a file in you gem's bin directory.  Once the file is created, you need to write in a shebang so that the program knows to run this file as Ruby, since it was not saved as a ruby file.  The line of code that you need to write in at the top is as follows:


`!/usr/bin/env ruby`


At this point your program is not executable, meaning that you may be able to read the file or write new code to it but the program will not run the file.  To make the file executable, you need to make changes to the file in the directory.  In the command line you need to type `#ls -lah` which will list your current files and their capabilities.  In order to make your new file executable, you need to modify the file.

`$ chmod +x <file_name>` will allow your new file to be executed as seen by the `+x` in your command.

#### 3.  Add necessary gems 

In order to complete this gem, multiple other gems are required as seen below.  You also need to make sure your files are all linked. So, my anthem_javelins.rb file became my environment to ensure the gem functioned as is should.

```
require "open-uri"
require "nokogiri"
require "pry"

require_relative "anthem_javelins/version"
require_relative "./anthem_javelins/cli"
require_relative "./anthem_javelins/javelins"
```

#### 4. Gemspec Folder

There is a gemspec file in every program that holds the information about the gem you are creating.  This is a required step in the gem-making process, as it holds information about the name of the gem, it's version, and the creators.  This is also where the gems dependencies are held. 

  ```
spec.add_development_dependency "bundler", "~> 1.17"
  spec.add_development_dependency "rake", "~> 10.0"
  spec.add_development_dependency "pry"
  
  spec.add_dependency "nokogiri"
```

#### 5. Writing my CLI

Finally, we have arrived at the bulk of the gem.  Now it's time to write some code and scrape the data.  As you may have guessed, I scraped my data from the Anthem website.  For the most part this was straight forward, as scraping requires knowledge of HTML in order to grab the code you want.  

Scraping is essentially finding the HTML syntax that you want, such as a section or a div as well as the class descriptors that are provided to specify for CSS where to look.  The difficulty in this can come from the creators of the website reusing class descriptors multiple times on one page.  To counteract this, I also used CSS identifiers to get the code I wanted.

Each javelin was on a different page so my code is a little bit bulkier than I expected as I had to scrape all the similar data off of each webpage.  Here is a snippet of my scraping:

```
 doc = Nokogiri::HTML(open("https://www.ea.com/games/anthem/gameplay-features/ranger-javelin"))
    
ranger = self.new

ranger.name = doc.search("h1.d2").text
ranger.description = doc.css("p")[0].text.strip
ranger.special_1 = doc.css("h4")[0].text.strip
ranger.special_2 = doc.css("h4")[1].text.strip
ranger.url = "https://www.ea.com/games/anthem/gameplay-features/ranger-javelin"
```

Overall, this was a very enjoyable project.  I was able to break free of the lessons, which taught you about one certain aspect of Ruby, and put all my learning together to create something that I am proud of.  It gave me the confidence I didn't have in Git as well as helping me create a gem that I can show to employers to prove my proficiency in what I have been taught.



