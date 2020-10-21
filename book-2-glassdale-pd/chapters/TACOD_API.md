# The TACO Department API

For this book, you will be consuming the Technically Averse Coding Offenses Department's API (https://totally.legit.site) to help you do your job as a highly technical police detective.

## Setup

1. Install [Postman](https://www.getpostman.com/). You instruction team will walk you through the basics of usage.
1. If you are on a Mac or Linux, you need to get oh-my-zsh installed if you haven't yet. See an instructor for help if you need it.



## Introduction
TODO: Write a beautiful story about how there is an API that a previous student/agent (now graduate) made to keep track of all the evidence gathered about the instructors, and now the current students/agents need to make a site that uses that API 👍

## Requesting Data from an API

In JavaScript, you are going to be using the Fetch API. It provides you with a `fetch()` method to initiate the request to another service on the World Wide Web. Here's an example fetch call to get data about TACOD's agents from the TACOD API that you queried via Postman above.

> #### `tacod/scripts/agents/AgentProvider.js`
```js
let agents = []

export const useAgents = () => {
    return agents.slice()
}

export const getAgents = () => {
    return fetch("https://totally.legit.site/agents")
        .then(response => response.json())
        .then(
            parsedAgents => {
                console.table(parsedAgents)
                agents = parsedAgents
            }
        )
}
```

Here's the pattern for a fetch call.

1. Request the data
    ```js
    fetch("https://totally.legit.site/agents")
    ```
1. Convert the JSON string response to a JavaScript data structure (object or array)
    ```js
    .then(response => response.json())
    ```
1. Do something with the data
    ```js
    .then(
        parsedAgents => {
            console.table(parsedAgents)
            agents = parsedAgents
        }
    )
    ```



* Reference: [How to Use the JavaScript Fetch API to Get Data](https://scotch.io/tutorials/how-to-use-the-javascript-fetch-api-to-get-data)

## Assignment

Your first assignment is to pull all of the data from the API (see above) and display all instructors in a grid format. Start with the following details for each instructor.

1. Name
1. Age
1. Role
1. Start Date
1. Evidence

![grid layout of instructors](./images/tacod-assignment-1.png)

### Tips

1. Use the `toLocaleDateString()` method on the dates to get the date in a more human readable format. Example below.
    ```js
    ${new Date(instructor.startDate).toLocaleDateString('en-US')}
    ```
1. Create your instructor data provider component, instructor list component, and instructor component in the `scripts/instructor` directory.
1. The instructor provider component should have the following collections and functions.
    ```js
    let instructors = []

    export const useInstructors = () => instructors.slice()

    export const getInstructors = () => {
        /*
            Load database state into application state with a fetch().
            Make sure the last then() updates the instructors array
        */
    }
    ```
1. Remember to import the `getInstructors()` function into `InstructorList.js` and invoke it there. The instructor list can only be rendered once you know you have the data.
    ```js
    import { getInstructors, useInstructors } from './instructors/InstructorProvider.js'

    export const InstructorList = () => {
        getInstructors().then(
            /*
                Now that you have the data, what
                component should be rendered?
            */
        )
    }

    ```