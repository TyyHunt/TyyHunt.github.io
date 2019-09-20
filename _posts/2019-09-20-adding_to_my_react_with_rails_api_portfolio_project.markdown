---
layout: post
title:      "Adding to my React with Rails API Portfolio Project"
date:       2019-09-20 23:36:34 +0000
permalink:  adding_to_my_react_with_rails_api_portfolio_project
---


After completing my final Portfolio Project with Flatiron school I added to part of my application by putting in a button to vote on which D&D Race is best.  By clicking on the button under each race you are able to add one to the total tally.  Now this information is kept in the state of the component and is not persistant but it was just an example of how to add one button to the mapping of an array of objects.

I started by switching from a constant of RacesContainer to a Class Component of React. 

```
class RacesContainer extends Component {

  constructor() {
    super()
    this.state = {
      Dragonborn: 0,
      'Half-Elf': 0,
      Human: 0,
      Gnome: 0,
      'Half-Orc': 0,
      Dwarf: 0,
      Elf: 0,
      Halfling: 0,
      Tiefling: 0
    }
  }
```

I then used a constructor to create a state for the RacesContainer specifically in order to keep track of the votes.  A button was then added to my mapping so that each iteration through would have a unique id, value, and show the current state for that race's like count.  As you can see below I used a button with an onClick event as well as the individualized information for the button in order to handle the on click event.

```
<Button className="logoutButton" variant="primary" onClick={this.handleClick} id={race.name} value={this.state[race.name]}>Like! {this.state[race.name]}</Button>
```


The on click event that I used for the button was intended to be as implicit as possible in order to create DRY code for the different races that could be voted on.  

```
  handleClick = event => {
    event.preventDefault();
    this.setState({
      [event.target.id]: (Number(event.target.value)) + 1,
    });
  }
```

Here you can see that whenever a button is clicked it sends the information to this event.  The ```handleClick``` code takes in an event as an argument, from there the first thing we do is prevent the default event that happens whenever a button is clicked.  For example if there was a link attached to the button it would reroute the user to that link by default but with this code ```event.preventDefault()``` nothing apperant happens when the button is clicked.  From there we then update the state of the Container by taking the ```event.target.id``` with a value of ```Number(event.target.value)```  which takes the string value of the value for that button which is ```value={this.state[race.name]}``` which changes for every race as ```race.name``` is the individual attribute that is being search for in ```this.state```.  Once all this information has been handed to ```handleClick``` the incriment is raised by one.  This repeats as many times as you are willing to click the button.  

The button also holds the expressed code of ```Like! {this.state[race.name]}``` which gives the current value of that specific race from state.  Every time the button is clicked a new number is expressed on the button as the value went up by one.  

Overall this was a fun excercise of creating one button for a mapping iteration in a way that you did not have to repeat yourself for eery individual race.  I was excited to see the results and am looking forward to adding on to the code in the future.

If you are interested in my coding for this app [click here!](http://github.com/TyyHunt/DnD-Digital)
