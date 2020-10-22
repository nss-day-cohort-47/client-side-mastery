# Checking Alibis

TODO: Write a beautiful story about how Lee Goldenrod or fellow students/agents in the TACO department need to keep track of their own notes 📝

## Goal

In this chapter, you will be refactoring your application to implement a new button on each instructor representation. The button must be labeled "Associate Alibis". Give each button a unique id by interpolating the `id` property of the instructor in the value.

```html
<button id="associates--${instructor.id}">Associate Alibis</button>
```

When the user clicks the button, you must iterate the array of `known_associates` for that instructor and then display the following information. You can display it in a dialog box, as a sidebar, at the top of the screen, or wherever you like.

1. The name of the known associate
1. The alibi that the known associate is providing for the instructor to try to prove the instructor's knowledge of best coding practices.

If any of the alibis for some of your suspects are noteworthy, then make sure you create a new note and POST it to your personal notes API.

## Getting Started

1. Which components do you need to create for this feature?
1. Where is the data coming from in the API? Do you need a new provider?
1. Which component should dispatch a custom event when the user clicks on the alibi button?
1. Which component should react to that custom event?
1. Does data need to be sent along with the event?
1. Which DOM element would contain the list of alibis? Do you need a new one, or can they go in an existing one?
