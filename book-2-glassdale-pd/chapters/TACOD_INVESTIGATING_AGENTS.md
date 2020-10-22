# Show Who Was Investigating Whom

For this feature, you will be doing nearly the exact same thing you did when you filtered the displayed instructors by evidence. Except in this case, you will build a component that renders a `<select>` element that is populated with all agents in the TACO department.

When the user selects an agent, show the instructors that were investigated by that agent.

TODO: make a gif for investigating agents
![animated image showing how criminals will be filtered](./images/arresting-officers.gif)

## Data Source

The agents are located at the URL of https://totally.legit.site/agents. You will `fetch` that data in your **`AgentDataProvider`** component and then export a `useAgents()` function in it so that the **`AgentSelect`** component can iterate it and render an `<option>` element for each one.

When an agent is selected by the user the **`AgentSelect`** component can dispatch a `agentSelected` custom event.

```js
eventHub.addEventListener("change", changeEvent => {
    if (changeEvent.target.id === "agentSelect") {
        // Get the name of the selected agent
        const selectedAgent = changeEvent.target.value

        // Define a custom event
        const customEvent = new CustomEvent("agentSelected", {
            detail: {
                agent: selectedAgent
            }
        })

        // Dispatch event to event hub
        eventHub.dispatchEvent(customEvent)
    }
})
```

1. What component would need to react to the fact that the user chose an agent? Evidence select? Inustrctor list?
1. Once you determine which component should react to the user action, implement an event listener in that component.
    ```js
    eventHub.addEventListener("agentSelect", event => {
        // How can you access the agent name that was selected by the user?
        const agentName = event.???

        // How can you get the instructors that were investigated by that agent?
        const instructors = useInstructors()
        instructors.???(
            instructorObject => {
                if (instructorObject.??? === agentName) {
                    return true
                }
            }
        )
    })
    ```