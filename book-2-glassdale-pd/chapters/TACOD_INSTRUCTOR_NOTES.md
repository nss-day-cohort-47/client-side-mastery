# Notes on Specific Instructors

In this chapter, you are going to modify your data so that notes are about specific instructors. A note will have an `instructorId` foreign key on them, so this is your first one -> many relationship you will be using in an application.

## Instructor and Note Data Example

Here is a quick example of how the data will look in your `database.json` file.

```json
{
    "notes": [
        {
            "id": 1,
            "noteText": "I'm pretty sure I saw them reading a book about... themselves?",
            "instructorId": 5
        }
    ]
}
```

## Changing the Note Form

Since you are going to record the `instructorId` on the note, you need to change the note form. Instead of having a text input field, you need to have a `<select>` element instead. It will contain an `<option>` element for each instructor.

Each option's value attribute must have a unique value. For example...

```html
<select id="noteForm--instructor" class="instructorSelect">
    <option value="${ instructor.id }">${ instructor.name }</option>
</select>
```

Then, when you build a note object to be saved to the database, you would get the value of the dropdown to determine the instructor id.

So an example object would look like this.

```js
const noteToSave = {
    text: noteText,
    instructorId: selectedInstructorId
}
```

## Multiple Providers

When you have two objects in different collections in your database that are related to each, that means that you need to pull in both collections to a component that wants to render information about both resources. For example, if you want your notes to render with the instructor name, then just using `useNotes()` will not be enough because each note only have the instructor's number on it.

> #### `tacod/scripts/notes/NoteList.js`

```js
import { useNotes } from './NoteProvider.js'
import { useInstructors } from '../instructors/InstructorProvider.js'


const render = (noteCollection, instructorCollection) => {
    contentTarget.innerHTML = noteCollection.map(note => {
        // Find the related instructor
        const relatedInstructor = instructorCollection.find(instructor => instructor.id === note.instructorId)

        return `
            <section class="note">
                <h2>Note about ${relatedInstructor.name}</h2>
                ${note.noteText}
            </section>
        `
    })
}

const NoteList = () => {
    getNotes()
        .then(getInstructors)
        .then(() => {
            const notes = useNotes()
            const instructors = useInstructors()

            render(notes, instructors)
        })
}
```
