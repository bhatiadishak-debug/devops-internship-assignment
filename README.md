# DevOps Internship Assignment

## Part 1: Version Control (Git & SSH)

### Git Fetch vs Git Pull

**git fetch** is like peeking at what changed on GitHub without touching your local files. It just downloads the information so you can see what's new, but your actual code stays the same.

**git pull** goes one step further — it downloads the changes AND automatically merges them into your local code. So your files actually get updated.

Think of it this way:
- `git fetch` = "let me see what changed"
- `git pull` = "let me see what changed AND apply it to my code"

### How to Resolve a Merge Conflict

A merge conflict happens when two branches edit the same line in the same file, and Git doesn't know which version to keep.

**Steps to resolve:**
1. Run `git merge feature-B` — Git will say there's a conflict
2. Open the conflicted file — you will see the conflict markers
3. Manually pick the version you want and delete the markers
4. Save the file
5. Run `git add .` then `git commit -m "resolved merge conflict"`

### Branch Simulation (feature-A and feature-B)

- Created `feature-A` branch and set `color = "red"`
- Created `feature-B` branch and set `color = "blue"`
- Merged both into main — Git flagged a conflict
- Resolved by keeping `color = "blue and red"`
- Committed the resolution successfully

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

## Part 3: Kubernetes (EKS Basics)

### Pod vs Deployment vs Service

- **Pod** → the smallest unit in Kubernetes. It runs one container (your app). Think of it as one running copy of your app.
- **Deployment** → manages multiple Pods. It says "I want 2 copies always running." If one crashes, it automatically restarts it.
- **Service** → gives your app a stable address so users can reach it. Pods keep changing IPs, Service stays fixed.

Think of it like a restaurant:
- Pod = one chef cooking
- Deployment = manager making sure there are always 2 chefs
- Service = the front door where customers come in

### Why EKS instead of Kubernetes on VMs?

Setting up Kubernetes yourself on VMs is very complex — you have to manage the control plane, updates, and security yourself. EKS (Amazon's managed Kubernetes) handles all of that for you. You just focus on deploying your app.

### Kubernetes YAML Files

Created `deployment.yaml` with 2 replicas and `service.yaml` with LoadBalancer type.