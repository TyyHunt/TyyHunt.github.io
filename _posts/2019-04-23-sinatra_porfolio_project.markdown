---
layout: post
title:      "Sinatra Porfolio Project"
date:       2019-04-23 20:36:59 -0400
permalink:  sinatra_porfolio_project
---


## Summer InTent:

#### It's spring here in Colorado and everyone is itching to get outdoors.  With nothing but nature on my mind, I came up with the idea for my Sinatra project.  Summer InTent is a web application that allows users to log in and create plans for the summer as well as check other users plans to see how they compare.

Learning Sinatra is, as I'm told, a great gateway to learning Rails.  It was my first opportunity as a Flatiron School student to build mulitpage web applications that incorporated databases, HTML, CSS, and Ruby.  It was extremely enjoyable, which created a deeper understanding of the Sinatra framework.


### Databases and the MVC

#### 1. Database Structure

In order for any web application to hold data, such as a username or password, we must set up a tables for all the content we are wishing to store.  These are stored in the database migration folder and are ran by either their creation timestamp or a numbering system in the name of the file. For example `01_create_users.rb` would load before `02_create_plans`.  A database file would look something like this:

```
class CreateUsers < ActiveRecord::Migration
  def change
    create_table :users do |t|
      t.string :username
      t.string :password_digest
    end
  end
end
```

The class CreateUsers is inheriting the code from the Migration class in the Activerecord module. Under that, you can see that a table is created for the Users and holds the username as a string and a password that is encrypted for safekeeping thanks to the `bcrypt` gem.  After creating a table, it is important to run `$ rake db:migrate` to activate and bring the table into use on your application.

#### 2. Models

Models are what hold the logic of the application. This is where you create a class for the table and provide any special methods that would be able to control or solve any complex formulas that would come through the application. 

```

class User < ActiveRecord::Base 
  has_secure_password
  has_many :plans
  
  def slug 
    username.downcase.strip.gsub(' ','-').gsub(/[^\w-]/,'')
  end
  
  def self.find_by_slug(slug)
    User.all.find{|user| user.slug == slug}
  end
  
end
```

This time, the class User is inheriting from the Base class in the ActiveRecord module.  In this instance, there are two methods that assist in changing a users from its current state to one that is hyphanated.  For example, my Github profile name is TyyHunt so this would change to Tyy-Hunt with assistance from the slug method.  Also, at the top of the class you can see that the class is associating with another table specifying that it 'has many' plans.  In the Plan class, it will say that it 'belongs to' a user.  This will help in the controllers part of the application to help the databases stay current and allow the user's work to not be permanant upon first creation.

#### 3. Views

When you think about a website, you consider the way that it looks and how you interact with it.  This is what the views are for.  They are the visual result of your HTML and Ruby.  The views are all ERB files, meaning they have Embedded RuBy(ERB) that helps show the content of the databases or the logic of the model in a stylish and practical way.  


#### 4. Controllers

The controllers are the go-between for the views and the models.  Controllers use RESTful programming, which is the gold standard for creating web applications.  Restful programming has created a common format for all websites to use in their pathing in controllers.

```
get '/login' do
    if !session[:user_id]
      erb :'/users/login'
    else
      redirect '/plans'
    end
  end
  
  post '/login' do
    user = User.find_by(:username => params[:username])
    if user && user.authenticate(params[:password])
      session[:user_id] = user.id
      redirect "/plans"
    else
      redirect to '/login'
    end
  end

```

Here you can see that we are using RESTful routes to apply the models logic to the views of the application.  The controllers have the most work to do, running back and forth to make sure that the users experience is seemless and accurate.  

Overall, using the MVC format in Sinatra keeps single responsibilty for each file and can lay out the framework of your application in a straight forward manner.  I had a great time learning Sinatra and creating an application that I would use in my personal life.

If you would like to see my application head over to [https://github.com/TyyHunt/Summer-InTent](http://).






