---
layout: post
title:      "The Magic of Javascript"
date:       2019-07-25 20:05:46 +0000
permalink:  the_magic_of_javascript
---


The use of Javascript in an application can easily improve it from an okay app into a great one.  Being able to perform actions and render new information without loading the page greatly improves the efficiency and look of overall quality of the application.  I am going to show you an example of what I did to make my Rails Project even better by using Javascript.

### AJAX Requests

AJAX, Asynchronous Javascript and XML are used to load and gather information asynchronously so that it does not effect the information that is currently presented on the page.  This, combined with a listener event, allows you to change what the viewer is able to see and add to what a viewer can interact with before having to travel to a new page.  
An example of an AJAX request is: 

```

$.ajax({
	type: 'GET',
	url: 'send-ajax-data.php',
	dataType: "JSON", // data type expected from server
	success: function (data) {
		console.log(data);
	},
	error: function(error) {
		console.log('Error: ' + error);
	}
});

```

What this means is that there is a ```GET``` request sent to a specific url for the information that is available.  The data is then translated into JavaScript Object Notation, or JSON, which can be used under the success condition to create a function that will create the effect of your choosing.  

This is all being done in the background while the viewer performs other tasks on the page.  Once that  listener event is triggered, events are rolled into action and new information appears on the screen without reloading the page.  This can even include a new form. 

AJAX is beneficial because you are able to prepare more information for a viewer, which is available when they click the corresponding button. Using this method saves a large amount of time since the user does not have to traveling back and forth between pages on the application.

After completing this addition to my project I now understand the power of Javascript.  With  a deeper understanding, you can make your application unique and you are only limited by your imagination.  I am very excited to learn even more Javascript so I can wow my viewers with the speed and flare it allows.





