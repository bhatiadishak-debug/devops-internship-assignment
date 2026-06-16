\# DevOps Internship Assignment



\## Part 1: Version Control (Git \& SSH)



\### Git Fetch vs Git Pull



\*\*git fetch\*\* is like peeking at what changed on GitHub without touching your local files. It just downloads the information so you can see what's new, but your actual code stays the same.



\*\*git pull\*\* goes one step further — it downloads the changes AND automatically merges them into your local code. So your files actually get updated.



Think of it this way:

\- `git fetch` = "let me see what changed"

\- `git pull` = "let me see what changed AND apply it to my code"



\### How to Resolve a Merge Conflict



A merge conflict happens when two branches edit the same line in the same file, and Git doesn't know which version to keep.



\*\*Example scenario:\*\*

\- Branch `feature-A` changes line 5 to: `color = "red"`

\- Branch `feature-B` changes line 5 to: `color = "blue"`

\- When we try to merge both, Git gets confused and marks the conflict



\*\*Steps to resolve:\*\*

1\. Run `git merge feature-B` — Git will say there's a conflict

2\. Open the conflicted file — you'll see something like:

<<<<<<< HEAD



color = "red"

color = "blue"


feature-B



3\. Manually pick the version you want (delete the markers)

4\. Save the file

5\. Run `git add .` then `git commit -m "resolved merge conflict"`

\### Branch Simulation (feature-A and feature-B)
See below for the steps I followed to simulate and resolve the conflict.

color="blue and red"

## Part 2: Docker & Containerization

### Dockerfile vs Docker Image vs Docker Container

- **Dockerfile** → a text file with instructions to build your app. Like a recipe.
- **Docker Image** → the result of building the Dockerfile. Like a cooked meal ready to serve.
- **Docker Container** → a running instance of the image. Like the meal served on a plate.

Think of it this way:
- Dockerfile = recipe
- Image = cooked food
- Container = food on the plate being eaten

### How to Reduce Image Size
- Use a slim base image like `python:3.11-slim` instead of `python:3.11`
- Remove unnecessary files after installing dependencies
- Use `.dockerignore` to exclude files not needed in the image
- Combine multiple RUN commands into one to reduce layers

### App Running Successfully
The app was built and ran successfully on localhost:9090
Output: "Hello from my DevOps app!"
