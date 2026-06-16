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

