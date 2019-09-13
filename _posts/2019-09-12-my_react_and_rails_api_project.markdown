---
layout: post
title:      "My React and Rails API Project"
date:       2019-09-13 00:37:17 +0000
permalink:  my_react_and_rails_api_project
---


My portfolio project is D&D Digital which uses React/Redux front end and Ruby on Rails backend to give consumers the ability to transform their pen and paper character sheets into a modern web form to keep trak of character progress.

I utilized the command ```create-react-app``` to set up the react framework and base app and index files.  Once that was created I used the ```create rails resource``` commands in my Rails framework to create my database, model, controller, and route for each of my individual criteria.  

Once my Rails API framework was complete and all routes and controllers completed I moved onto my react framework to be able to view my data in a pleasant, modern appliation.  Due to my project containing multiple pages and resources I utilized React Router along with Tunk middleware to create paths in order to stick with RESTful routes as well as handle asynchronous API calls.

D&D Digital is a simple application that allows users to create characters that include their name, level, health, stats, race, class, and weapon in use.  When the form is completed and the character is submitted, the character is created and saved into the Rails database with a relationship of User ```has_many``` Characters.  This way a User can see an index of their characters before they load their desired character to update and keep track of their epic journey. Once a User logs in each character follows the CRUD (Create, Read, Update, Detele) framework.  

Overall I found this project to be the most challenging due to it being a multi-faceted project utilizing multiple frameworks, ie. React and Rails.  After a lot of trial by error and research I was able to connect the two frameworks.  I believe that my biggest problem during this project was the CORS security.  Having my React framework hosted on localhost:3000 and my Rails API framework hosted on localhost:3001 dissallowed the two frameworks from communicating due to the possibility of csrf (cross-site request forgery).  In order to bypass this I had to download the ```cors``` gem and enabled the ```cors.rb``` initializer.

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'
    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

Once my CORS problem was solved it was a matter of building each component, including my ```mapDispatchToProps``` and ```mapStateToProps```  when necessary, and ensuring my dispatch fetch processes sent the right data.  At the beginning I struggled to comprehend when each process was needed but after successfully adding my race, class, and weapon paths it was pretty simplistic to add my user path with login and sign up.  

This was a project of troubleshooting and perserverance but I trully appreciated building my skills and accomplishing what I set out to do.  At this point the application is functional and has a pleasant user experience but I will continue to build out the funtionality of the site and add to its capability.

