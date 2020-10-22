# Filtering Instructors by Evidence

In this chapter, you are going to implement the idea of the Event Hub from the last chapter and get your components talking to each other with messages.

## Let's Talk About Filter

The `filter()` method on an array creates a brand new array with a subset of items that exist in the original array. Only items in the original array that pass the test can make it into the new, happy, much better array. Here's an example.

Imagine that you have an array of people objects. Each object has the person's name and age. You're the bouncer at a bar, and you want to filter out everyone who isn't of legal drinking age. Here's how you would do that in JavaScript - 'cause, y'know, all bouncers are expert JavaScript developers.

```js
const hopefulPatrons = [
    { name: "Sally Fisher", age: 30 },
    { name: "Dylan Thomas", age: 19 },
    { name: "Callan Morrison", age: 26 },
    { name: "Juan Rodriguez", age: 20 }
]

const legalPatrons = hopefulPatrons.filter(currentPatron => {
    return currentPatron.age >= 21
})

// or

const legalPatrons = hopefulPatrons.filter(currentPatron => {
    if (currentPatron.age >= 21) {
        return true
    } else {
        return false
    }
})

// or

const legalPatrons = hopefulPatrons.filter(currentPatron => {
    const canEnterBar = false

    if (currentPatron.age >= 21) {
        canEnterBar = true
    }

    return canEnterBar
})
```

Three possible ways to write this logic. Everyone thinks differently, so you may think of yet another way to write that code. The point is that the test is written inside the function argument that is passed to `filter`. If that function returns true, then the current item being evaluated is allowed to be added to the new array.

```js
console.log(hopefulPatrons)

// Original array remains unchanged
[
    { name: "Sally Fisher", age: 30 },
    { name: "Dylan Thomas", age: 19 },
    { name: "Callan Morrison", age: 26 },
    { name: "Juan Rodriguez", age: 20 }
]

console.log(legalPatrons)

// Brand new array created that contains items that passed the test
[
    { name: "Sally Fisher", age: 30 },
    { name: "Callan Morrison", age: 26 }
]

```


## Implement Event Hub and Get Your Components Talking and Listening

Time for you to implement the Event Hub, get components sending and listening to messages, and then filtering the list of instructors with the `filter()` array method.

> **`tacod/scripts/evidence/EvidenceSelect.js`**

```js
/*
    Which element in your HTML contains all components?
    That's your Event Hub. Get a reference to it here.
*/
const eventHub = document.querySelector(you_fill_this_in)
const contentTarget = document.querySelector(".filters__evidence")

// On the event hub, listen for a "change" event.
eventHub.addEventListener("change", event => {

    // Only do this if the `evidenceSelect` element was changed
    if (event.target.id === "evidenceSelect") {
        // Create custom event. Provide an appropriate name.
        const customEvent = new CustomEvent("evidenceChosen", {
            detail: {
                evidenceThatWasChosen: event.target.value
            }
        })

        // Dispatch to event hub
        eventHub.dispatchEvent(customEvent)
    }
})


const render = evidenceCollection => {
    contentTarget.innerHTML = `
        <select class="dropdown" id="evidenceSelect">
            <option value="0">Please select some evidence...</option>
            ... you wrote awesome code here ...
        </select>
    `
}


export const EvidenceSelect = () => {
    getEvidence()
        .then(() => {
            const allEvidence = useEvidence()
            render(allEvidence)
        })
}
```

> **`tacod/scripts/instructor/InstructorList.js`**

```js
const eventHub = document.querySelector(".container")

// Listen for the custom event you dispatched in EvidenceSelect
eventHub.addEventListener('what custom event did you dispatch in EvidenceSelect?', event => {
    // Use the property you added to the event detail.
    if (event.detail.evidenceThatWasChosen !== "0"){
        /*
            Filter the instructors application state down to the people who demonstrated use of that evidence
        */
        const matchingInstructors = appStateInstructors.filter(???)

        /*
            Then invoke render() and pass the filtered collection as
            an argument
        */
    }
})

const render = instructorCollection => {
    contentTarget.innerHTML = you_fill_this_in
}


// Render ALL instructors initally
export const InstructorList = () => {
    getInstructors()
        .then(() => {
            const appStateInstructors = useInstructors()
            render(appStateInstructors)
        })
}
```
