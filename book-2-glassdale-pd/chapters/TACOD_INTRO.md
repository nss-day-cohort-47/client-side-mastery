# T.A.C.O'D (Technically Averse Coding Offenses Department)

### What's the story?

This is my take on rewriting Glassdale. All of the actual code will hopefully be relatively easy to replace, and I'll only need to change the story behind the code. The overall story is that there are alien imposters among the NCC (Nashville Coding College) instructional team and the students are trying to figure out who the imposter is. They'll be tasked by the senior lead instructor, Lee Goldenrod, with building out a web app that will utilize an API that a previous student had already started working on.

The endpoints are being replaced with: 
- ~~Criminals~~ --> Instructors
- ~~Officers~~ --> Agents (the students)
- ~~Crimes/Convictions~~ --> Evidence
- ~~Witnesses~~ --> Witnesses
- ~~Facilities~~ --> Cohorts
- ~~CriminalFacilities~~ --> InstructorCohorts

### The intro:
> You've been a student at Nashville Coding College (NCC) for a month now, but you've started to notice some strange things happening around the instructors. From talking to students in other cohorts you've gathered that some of the instructors have been merging their code directly into their main/master branches, rewriting other people's code, and writing code in the morning *without any caffeine*.
>
> Knowing what you've learned about in the first month at NCC, you know that pushing straight to the main/master branch without making a new branch isn't best practice and rewriting someone else's code is a MAJOR concern. 
>
> You're not quite sure what to do with this information you've gathered, so per the guidance from some of your fellow cohort mates you meet with the senior lead instructor, Lee Goldenrod.
>
> You catch Lee in what the staff members at NCC call the "Hackery": "Lee! Can I talk to you for a second?", you nervously ask. He quickly turns around and cheerily says "Of course!"
>
> "Okay, this might sound a little weird but... some of the other students and I think that something feels off about some of the instructors." you say a little louder than intended. Lee's facial expression goes from a cheery smile to a serious, stern look as he quickly pulls you into a small huddle room and asks that you take a seat.

## Setup

1. Create the `~/workspace/tacod` directory with the `mkdir` command.
1. Create the following directory structures.
    1. `~/workspace/tacod/api`
    1. `~/workspace/tacod/scripts/instructors`
    1. `~/workspace/tacod/scripts/evidence`
    1. `~/workspace/tacod/scripts/agents`
    1. `~/workspace/tacod/styles`
1. Create your `scripts/main.js`, and `styles/main.css` files.
1. Make sure that `json-server` was installed correctly by typing it into your terminal. If you get feedback that your system doesn't recognize the `json-server` command, speak to an instructor immediately.
1. Make an `index.html` file in `~/workspace/tacod` directory. You are provided some boilerplate HTML below to place in that file.
1. Start your web server and verify that you get that HTML in Chrome.

#### Boilerplate HTML

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <title>T.A.C.O'D</title>
    <link rel="stylesheet" href="./styles/main.css">
</head>

<body>

    <main class="container">
        <header>
            <div class="filters">
                <div class="filter filters__evidence"></div>
                <div class="filter filters__agent"></div>
            </div>
        </header>
        <article class="instructorsContainer"></article>
    </main>

    <script type="module" src="./scripts/main.js"></script>
</body>

</html>
```