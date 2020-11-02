# Listing Cohorts per Instructor

To get the cohorts in which each instructor has taught for, it's a two-step process to traverse the data.

1. You start with iterating the instructors array.
1. For each instructor, filter the `instructorCohorts` array down to the cohorts that the instructor has taught in.
1. From **that** array, we can get the corresponding cohort objects.

## Setup

### Cohort Provider

First, set up a **`CohortProvider`** component with the following code:

> **`tacod/scripts/cohorts/CohortProvider.js`**

```js
let cohorts = []

export const useCohorts = () => cohorts.slice()

export const getCohorts = () => {
   return fetch("https://totally.legit.site/cohorts")
    .then(response => response.json())
    .then(apiData => {
        cohorts = apiData
    })
}
```

### Instructor Cohorts Relationship Provider

Next, an **`InstructorCohortProvider`** component for the relationship data between instructors and cohorts.

> **`tacod/scripts/cohorts/InstructorCohortProvider.js`**

```js
let instructorCohorts = []

export const useInstructorCohorts = () => {
    return instructorCohorts.slice()
}

export const getInstructorCohorts = () => {
    return fetch("https://totally.legit.site/instructorCohorts")
        .then(response => response.json())
        .then(apiData => {
            instructorCohorts = apiData
        })
}
```

## Showing Cohorts Per Instructor

You want each instructor card in your UI to now show the cohorts that the instructor has taught for. This means that the **`Instructor`** component must be modified to show the new HTML representations, and the **`InstructorList`** component must be updated to get the data.

### Get Data Before Rendering

As the code stands right now, the operation of getting the instructor data is invoked in `main.js` because several components need that data before rendering _(instructor list, notes list, and note form)_. However, the instructor list is the only component that needs information about the cohorts, so you will add the code in that component to get the data.

> **`tacod/scripts/instructors/InstructorList.js`**

```js
export const InstructorList = () => {
    // Kick off the fetching of both collections of data
    getCohorts()
        .then(getInstructorCohorts)
        .then(
            () => {
                // We want to use the data now that it has been fetched
                const cohorts = useCohorts()
                const instructorCohorts = useInstructorCohorts()
                const instructors = useInstructors()

                // Pass all three collections of data to render()
                render(instructors, cohorts, instructorCohorts)
            }
        )
}
```

### Updated Rendering

> **`tacod/scripts/instructors/InstructorList.js`**

```js
const render = (instructorsToRender, allCohorts, allRelationships) => {
    // Step 1 - Iterate through all instructors
    contentTarget.innerHTML = instructorsToRender.map(
        (instructorObject) => {
            // Step 2 - Filter all the relationships to get the only relationships for this instructor
            const cohortRelationshipsForThisInstructor = allRelationships.filter(ic => ic.instructorId === instructorObject.id)

            // Step 3 - Convert the relationships into a new array of cohorts with .map()
            const cohorts = cohortRelationshipsForThisInstructor.map(ic => {
                // Step 3.5 - use the single instructorCohort object (ic) to find the matching cohort
                const matchingCohortObject = allCohorts.find(cohort => cohort.id === ic.cohortId)
                return matchingCohortObject
            })

            // We must pass the matching cohorts to the Instructor component
            return Instructor(instructorObject, cohorts)
        }
    ).join("")
}
```

### Cohort HTML Representation in Instructor Component

There is a new `<div>` element in the instructor HTML representation that uses the `.map()` array method to convert each cohort object to an HTML representation of a cohort.

Be aware that this is all highly abstract code that will push your ability to visualize the data flow to **the extreme**!!

You are going to pattern match when you write code for a many-to-many relationship for quite a while. Doing this from scratch requires a neural rewiring that takes much longer than your time here at NSS.

```js
export const Instructor = (instructorObject, cohorts) => {
    return `
    <div class="instructor">
        <h4>${instructorObject.name}</h4>
        <div class="instructor__details">
            <p>Evidence: ${instructorObject.evidence}</p>
            <p>Investigated by: ${instructorObject.investigatedBy}</p>
            <p>Age: ${instructorObject.age}</p>
            <div class="instructor__cohortList">
            <!-- Here is the list of cohorts for this instructor -->
                <h2>Cohorts</h2>
                <ul>
                    ${cohorts.map(cohort => `<li>${cohort.cohortName}</li>`).join("")}
                </ul>
            </div>
            <button id="associates--${instructorObject.id}">Show Associates</button>
        </div>
    </div>
    `
}
```
