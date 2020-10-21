# Gathered Evidence

## Introduction

TODO: Write a beautiful story about how we need to filter our instructors by the evidence gathered against them 😊

## Goal

In this chapter, you are going to be implementing a `<select>` element so that you have a drop-down element on the screen that lists all of the evidence that previous agents of the TACO department have gathered.

In a future chapter, you are going to implement code that detects when the user selects the evidence, and have the instructor list render only those instructors that have demonstrated use of that evidence.

TODO: make a gif of selecting evidence from a dropdown
![filter criminals by crime animation](./images/filter-criminals-by-crime.gif)

The TACOD's API has a resource that gives you a collection of all the evidence that previous agents of the TACO department have gathered.

https://totally.legit.site/evidence

You need to create two, new components in your application

1. The **`EvidenceProvider`** component will `fetch` the evidence and export a `useEvidence()` method for other components to import.
1. The **`EvidenceSelect`** component, which will invoke `useEvidence()` and then iterate that collection to fill out the dropdown in the browser.

## Using the map() Array Method

Before you get started on your code, here is a review of how to use the `.map()` array method to iterate a collection, and convert every item in that collection into something else.

Assume that you have a list of people objects in an array.

```js
const people = [
    { id: 1, name: "Caitlin Stein" },
    { id: 2, name: "Ryan Tanay" },
    { id: 3, name: "Leah Hoefling" },
    { id: 4, name: "Emily Lemmon" },
    { id: 5, name: "Bryan Nilson" },
    { id: 6, name: "Jenna Solis" },
    { id: 7, name: "Meg Ducharme" },
    { id: 8, name: "Madi Peper" },
    { id: 9, name: "Kristen Norris" }
]
```

That's the raw data that should _**always remain unchanged**_. You want to display only a list of names in a dropdown list in your user interface, you would need to build a brand, new array containing those values. You can use `.map()` for that.

```js
const fullNames = people.map(
    personObject => {
        const valueToBeInNewArray = personObject.name
        return valueToBeInNewArray
    }
)

console.log(fullNames)
// ['Caitlin Stein', 'Ryan Tanay', 'Leah Hoefling', 'Emily Lemmon', 'Bryan Nilson', 'Jenna Solis', 'Meg Ducharme', 'Madi Peper', 'Kristen Norris']
```

Now imagine you want to fill a dropdown box in your UI with last names. First, you would get a reference to an existing element, like a `section` or a `div`, and update its `.innerHTML` property like in the example below.

```js
const contentTarget = document.querySelector(".names")

contentTarget.innerHTML = `
    <select>
        ${
            people.map(personObject => {
                const fullName = personObject.name
                return `<option>${fullName}</option>`
            })
        }
    </select>
`
```

What's confusing, and also powerful, about the above code snippet is that you have string template **inside another string template**. That's the true power of the interpolation capability of `${}`. You can put any JavaScript expression inside those curly braces. The only limitation is that it is a single expression. You can't put multiple lines of code inside them. 😢

## Evidence Data Provider

The **`EvidenceProvider`** component will follow the same structure as your **`InstructorProvider`** component.

> **`tacod/scripts/evidence/EvidenceProvider.js`**

```js
let evidence = []

export const useEvidence = () => evidence.slice()

export const getEvidence = () => {
    /*
        Load database state into application state with a fetch().
        Make sure the last `then()` sets the local `evidence`
        variable to what is in the response from the API.
    */
}
```

## Evidence Select Component

This component will render a `<select>` element with child `<option>` elements for each piece of evidence collected in the API.

#### Starter Code

> **`tacod/scripts/evidence/EvidenceSelect.js`**

```js
/*
 *   EvidenceSelect component that renders a select HTML element
 *   which lists all pieces of evidence in the TACOD's API
 */
import { useEvidence } from "./EvidenceProvider.js"

// Get a reference to the DOM element where the <select> will be rendered
const contentTarget = document.querySelector(".filters__evidence")

export const EvidenceSelect = () => {
    // Get all evidence from application state
    const allEvidence = useEvidence()
    render(allEvidence)
}

const render = evidenceCollection => {
    /*
        Use interpolation here to invoke the map() method on
        the evidenceCollection to generate the option elements.
        Look back at the example provided above.
    */
    contentTarget.innerHTML = `
        <select class="dropdown" id="evidenceSelect">
            <option value="0">Please select some evidence...</option>
            ${
                something.map()
            }
        </select>
    `
}
```

## Optional Advanced Challenge: Map the Aquarium

If you want to practice using the `map()` array method a handful of times to build up the mental muscle, you can go back to your Martin's Aquarium application and replace all of the `for..of` loops in the list components to use `map()` instead.

For example...

```js
let locationListHTML = ""

for (const location of locations){
    locationListHTML += LocationAsHTML(location)
}

contentElement.innerHTML += `
    <article class="locations">
        ${locationListHTML}
    </article>
`
```

Would become...

```js
contentElement.innerHTML += `
    <article class="locations">
        ${locations.map(location => LocationAsHTML(location)).join("")}
    </article>
`
```

## Optional Advanced Challenge: Map the Farm

Likewise, the Modern Farm application code has many `for..of` loops in it to plant the seeds and harvest the seeds. Here's the modules you can refactor to use `map()`.

* catalog.js
* harvester.js

## Optional Advanced Challenge: Map the Journal

Open your `JournalEntryList.js` module and see if you can rewrite the `for..of` loop that iterates your entries

```js
for (const entry of entries) {

}
```

To work correctly with `entries.map()`.
