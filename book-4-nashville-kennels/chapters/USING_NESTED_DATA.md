# Individual Items with Nested Data

In this chapter, you are going to use one of the features of `json-server` to get nested data back from the API.

You are going to do this with animals.

## Getting the Nested Data

Since the animal detail component is responsible for showing data, and related data about an individual animal, you need a method in your provider to get all of that information for a single animal.

Add the following method to the animal provider. It allows any component to get a single animal, but with the location and customer objects embedded inside the response.

> ##### `/src/components/animal/AnimalProvider.js`

```js
const getAnimalById = (id) => {
    return fetch(`http://localhost:8088/animals/${id}?_expand=location&_expand=customer`)
        .then(res => res.json())
}
```
Be sure to include this method in the export of the provider
```js
<AnimalContext.Provider value={{
    animals, addAnimal, getAnimals, getAnimalById
    }}>
        {props.children}
</AnimalContext.Provider>
```

Here's how the response will look.

```json
{
  "id": 2,
  "name": "Snickers",
  "breed": "Beagle",
  "locationId": 2,
  "treatment": "React Hook useEffect has a missing dependency: 'setDefaults'. Either include it or",
  "customerId": 4,
  "location": {
    "id": 2,
    "name": "Nashville South",
    "address": "209 Emory Drive"
  },
  "customer": {
    "email": "steve@stevebrownlee.com",
    "password": "123",
    "name": "Steve Brownlee",
    "id": 4
  }
}
```

The server (API) did the work for you!!

## Animal List Refactor

The animal list will show a list of animal names, which are hyperlinks. When you click on one animal name, an animal detail component will render.

> ##### `/src/components/animal/AnimalList.js`

```jsx
import React, { useContext, useEffect } from "react"
import { AnimalContext } from "./AnimalProvider"
import { AnimalCard } from "./AnimalCard"
import "./Animal.css"
import { useHistory } from "react-router-dom"

export const AnimalList = () => {
    const { animals, getAnimals } = useContext(AnimalContext)
	
	//useEffect - Side effects are things that cannot be done during render 
	//for example: reaching out to the world for something
    useEffect(() => {
		console.log("AnimalList: useEffect - getAnimals")
		getAnimals()
		
    }, [])

	const history = useHistory()
    return (	
		<div className="animals">
			{console.log("AnimalList: Render")}
			<h2>Animals</h2>
			<button onClick={() => {history.push("/animals/create")}}>
            Add Animal
        	</button>
            {
			animals.map(animal => {
				return <AnimalCard key={animal.id} animal={animal} />
			})
            }
        </div>
    )
}
```
## AnimalCard refactor
> ##### `/src/components/animal/AnimalCard.js`

```jsx
import React from "react"
import "./Animals.css"
import { Link } from "react-router-dom"

export default ({ animal }) => (
    <section className="animal">
        <h3 className="animal__name">
            <Link to={`/animals/${animal.id}`}>
                { animal.name }
            </Link>
        </h3>
        <div className="animal__breed">{ animal.breed }</div>
    </section>
)
```

## New Animal Details Component

Create a new component in the animal directory which will be responsible for showing all the details of the animal.

> ##### `/src/components/animal/AnimalDetail.js`

```js
import React, { useContext, useEffect, useState } from "react"
import { AnimalContext } from "./AnimalProvider"
import "./Animal.css"
import { useParams, useHistory } from "react-router-dom"

export const AnimalDetail = () => {
    const { releaseAnimal, getAnimalById } = useContext(AnimalContext)
	
	const [animal, setAnimal] = useState({})
	const [location, setLocation] = useState({})
	const [customer, setCustomer] = useState({})
	
	const {id} = useParams();
	const history = useHistory();

    useEffect(() => {
		console.log("useEffect", id)
        getAnimalById(id)
        .then((response) => {
			console.log("response", response)
			setAnimal(response)
			setLocation(response.location)
			setCustomer(response.customer)
		})
			}, [])

    return (
        <section className="animal">
            <h3 className="animal__name">{animal.name}</h3>
            <div className="animal__breed">{animal.breed}</div>
			<div className="animal__location">Location: {location.name}</div>
			<div className="animal__owner">Customer: {customer.name}</div>
			
            <button onClick={
                () => {
                    releaseAnimal(animal)
                        .then(() => {
                            history.push("/animals")
                        })
                }
            }>Release Animal</button>
            
            <button onClick={() => {
                history.push(`/animals/edit/${animal.id}`)
            }}>Edit</button>
        </section>
    )
}
```

## Create a New Dynamic Route

You will need to support a route like the following.

http://localhost:3000/animals/7

Within ApplicationViews, add the route for animal details within the **AnimalProvider** component.

> ##### `/src/components/ApplicationViews.js`

```js
<AnimalProvider>
   <Route exact path="/animals/:id">
		<AnimalDetail />
	</Route>
</AnimalProvider>
```

## Try it Out

Now when you click on an animal's name in the list view, you should see your new animal detail view.

![image of animal detail view](./images/animal-details.gif)

## Practice: Locations

Your next task is to refactor your location components. On your location list, display the location name, the number of animals currently being treated, and the number of employees.

When you click the name of a location, you should be taken to a detail view that lists the names of all animals currently being treated, and the names of all employees working there.

> **Tip:** You don't need all of the fancy styling like you see below. Just get the information displayed.

![animation of location list and location details](./images/location-details.gif)