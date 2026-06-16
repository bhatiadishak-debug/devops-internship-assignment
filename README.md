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

## Part 4: CI/CD Pipeline

### GitHub Actions Workflow

Created a workflow that runs automatically when code is pushed to main branch:
- **Build** → builds the Docker image
- **Test** → runs a simple test (echo "Tests passed")
- **Push** → simulates pushing image to DockerHub

### How pipeline would change for Kubernetes deployment

After building the Docker image, we would add these extra steps:
- Push the real image to DockerHub or ECR (Amazon's container registry)
- Install `kubectl` in the workflow
- Run `kubectl apply -f deployment.yaml` to deploy to Kubernetes cluster
- Run `kubectl apply -f service.yaml` to update the service

## Part 5: Monitoring & Logs

### Difference between Metrics, Logs and Traces

- **Metrics** → numbers that measure your app over time. Example: CPU usage, memory usage, number of requests per second. They tell you "how much."
- **Logs** → text records of what happened inside your app. Example: "User logged in at 5pm" or "Error: database not found." They tell you "what happened."
- **Traces** → track a single request as it moves through multiple services. They tell you "where did it slow down."

Think of it like a hospital:
- Metrics = patient's heart rate monitor
- Logs = doctor's notes
- Traces = following a patient through every department

### How to Debug a Crashed Kubernetes Pod

```bash
# Step 1 - See all pods and their status
kubectl get pods

# Step 2 - See details about the crashed pod
kubectl describe pod <pod-name>

# Step 3 - See the logs of the crashed pod
kubectl logs <pod-name>

# Step 4 - See logs of previous crashed container
kubectl logs <pod-name> --previous
```

### Recommended Monitoring Tools for AWS EKS

- **Prometheus** → collects metrics from your pods automatically
- **Grafana** → visualizes Prometheus metrics in beautiful dashboards
- **CloudWatch** → AWS built-in tool for logs and metrics, easy to set up with EKS
- **ELK Stack** → Elasticsearch, Logstash, Kibana — great for searching through logs

## Part 6: Problem-Solving Scenario

### Setting up a new microservice in AWS EKS

**The requirement:**
- Code is on GitHub
- Needs to be containerized
- Should auto-deploy on merge to main branch
- Logs should be visible to the dev team

**My approach:**

**Step 1 - Containerize the app**
- Write a Dockerfile for the microservice
- Test it locally using `docker build` and `docker run`
- Make sure the app runs correctly inside the container

**Step 2 - Push image to ECR**
- Create an Amazon ECR repository
- Tag the Docker image and push it to ECR
- ECR is Amazon's private Docker registry

**Step 3 - Write Kubernetes YAML files**
- Create `deployment.yaml` with required replicas
- Create `service.yaml` with LoadBalancer to expose the app
- Apply them to the EKS cluster using `kubectl apply`

**Step 4 - Set up CI/CD with GitHub Actions**
- Write a workflow that triggers on merge to main
- Workflow steps: build image → push to ECR → deploy to EKS using kubectl
- This handles auto-deployment on

