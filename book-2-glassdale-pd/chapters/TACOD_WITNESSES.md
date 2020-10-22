# Checking Witness Statements

TODO: Write a beautiful story about how Lee Goldenrod asks the student/agent to review all of the witness statements

In this chapter, you will be refactoring your application to implement a new button that will allow you to review all witness statements. The witness data is at the URL http://totally.legit.site/witnesses. Place a button in the UI labeled "Witness Statements".

When the user clicks the button, you should request all witnesses and display the following information. If instructors are currently rendered, this information should take its place.

1. The name of the witness.
1. Their statement text.

Review all of the statements, and if any of them are noteworthy, then make sure you create a new note and POST it to your personal notes API.

## Getting Started

1. Which components do you need to create for this feature?
1. Where is the data coming from in the API? Do you need a new provider?
1. Which component is "talking" (_i.e. dispatches a custom event_) when a user performs an action?
1. Which component would listen and react to that custom event?
1. Does data need to be send along with the message?
1. Which DOM element would contain the list of witness statements? Do you need a new one, or can they go in an existing one?
