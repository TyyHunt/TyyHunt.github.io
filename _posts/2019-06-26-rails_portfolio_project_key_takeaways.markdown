---
layout: post
title:      "Rails Portfolio Project Key Takeaways"
date:       2019-06-26 22:26:14 +0000
permalink:  rails_portfolio_project_key_takeaways
---



### Rails is levels above any other Ruby framework

As I finished up my Rails portfolio project I reflected on what makes Rails such a great famework to work with and why it is extremely easy to make applications that excel in logic and layout.  To me being able to write an application in such a short amount of time is the highlight of Rails.  Excluding design, you are quickly able to create a database, controller actions, and application views without much work.  A few examples that I will go over that made Rails so easy to work with are:


###### 1. Validations
###### 2.  Field With Errors
###### 3.  Form for
###### 4.  Routes

<hr>
#### Validations

Validations are a quick way to stop objects from getting saved to the database without the correct requirements which you are able to set.  In the example below the Person Model is validating the name field to ensure that it has been filled out.  If it has not then they object will not be saved to the database.  Once the form is submitted you are able to check if the person is `valid?`.  If valid returns true than it would be saved if not the form repopulates with a `field_with_errors` HTML class around the failed validation.

```

class Person < ApplicationRecord
  validates :name, presence: true
end
 
>> p = Person.new
# => #<Person id: nil, name: nil>
>> p.errors.messages
# => {}
 
>> p.valid?
# => false
>> p.errors.messages
# => {name:["can't be blank"]}
 
>> p = Person.create
# => #<Person id: nil, name: nil>
>> p.errors.messages
# => {name:["can't be blank"]}
 
>> p.save
# => false
 
>> p.save!
# => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
 
>> Person.create!
# => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank

```

#### Field_with_errors

Field with errors is an amazing HTML class that surrounds a failed validation field after initially submitting the form.  It is utilized while using the form_for form tag that is created by rails "magic".  We will go over form_for later in the blog but for now I will show you how the field with errors works.  

First you need to submit a form purposefully not completing the validations required to save to the database.  This will repopulate the form with errors like this:

```
<div class="field_with_errors">
<input type="text" value="" name="project[name]" id="project_name" />
</div>
```

Now with the class of `field_with_errors` surrounding our failed field we can stylize that using CSS to make the failure more pronounced for our users to see and fix. It is common to use this css on `field_with_errors`:

```
.field_with_errors {
border: 1px solid red;
}
```

This brings attention to the field by putting a red border around the area that needs to be fixed.  Once the changes have been made and all the validations are passing then the form can be properly saved to the database.

#### Form for

As I mentioned above `field_with_errors` works properly when using the the `form_for` from builder.  This is probably one of the more advanced Rails "magic" that you can use when building a model object form.  To ensure that `form_for` works properly you need to create a "new" action in the controller for the specific object.

```
def new
  @article = Article.new
end
```

This allows the `form_for` to bind a form to a model object.

```
<%= form_for @article, url: {action: "create"}, html: {class: "nifty_form"} do |f| %>
  <%= f.text_field :title %>
  <%= f.text_area :body, size: "60x12" %>
  <%= f.submit "Create" %>
<% end %>
```

As you can see above the form is now attached to `@article` which we set in the new action of the Article controller.   The attachment is important because now `@article` is set as `Article.new` which has validations that are required before being saved to the database.  Using a `.html.erb` file will now translate the `form_for` into this HTML form: 

```

<form class="nifty_form" id="new_article" action="/articles" accept-charset="UTF-8" method="post">
  <input name="utf8" type="hidden" value="&#x2713;" />
  <input type="hidden" name="authenticity_token" value="NRkFyRWxdYNfUg7vYxLOp2SLf93lvnl+QwDWorR42Dp6yZXPhHEb6arhDOIWcqGit8jfnrPwL781/xlrzj63TA==" />
  <input type="text" name="article[title]" id="article_title" />
  <textarea name="article[body]" id="article_body" cols="60" rows="12"></textarea>
  <input type="submit" name="commit" value="Create" data-disable-with="Create" />
</form>
```

This `form_for` tag implies an authenticity token, sets the charset to `UTF-8` and translates the inputes to include `type`, `name`, and `id`.  So with that quick from field using `form_for` and Ruby you can create a very thorough form which has `field_with_errors` included as well as error messages to add additional information fo our users.

#### Rails Routes

After completing the Sinatra project and switching to Rails one of the major differences that I found was the controller actions.  

A Sinatra action looks like this

```
get '/products' do
  # Display the products page
end
```

where you explicitly write the `get` path and the logic inside of it.  For rails it uses the Ruby method format for action routes such as 

```
def index
    if params[:status] == "activated"
      @clients = Client.activated
    else
      @clients = Client.inactivated
    end
end
```

This ends up being more straight forward because Rails is smart enough to know that the `index` route for products will take you to `/products`.  It is implied with the `index` method so Rails writes the routes for you.  They both have their benefits but having a uniform action path for your methods becomes a lot easier when you have multiple models and want the models to perform in similar ways.  Instead of having to remember each explicit path set in Sinatra you can easily remember you actions which are implied in Rails.

Overall Rails has a lot of "magic" that the creators added to the framwork.  They took the time to make it easier for Rubyists to quickly and thoroughly manage a full app.  With the shortcuts in coding you can power through relatively short sessions and come out way of where you would be at if you manually coded your whole applications.  With all that being said I had a blast learning Rails and creating a more secure app.


