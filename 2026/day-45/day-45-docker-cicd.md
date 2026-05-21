**Task 1: Prepare**

Use the app you Dockerized on Day 36 (or any simple Dockerfile)

Add the Dockerfile to your github-actions-practice repo (or create a minimal one)

Make sure DOCKER_USERNAME and DOCKER_TOKEN secrets are set from Day 44

[Dockerfile](https://github.com/Sushil1234567/github_Action_Practise/blob/main/Dockerfile)

------

**Task 2: Build the Docker Image in CI**

Create .github/workflows/docker-publish.yml that:

Triggers on push to main

Checks out the code

Builds the Docker image and tags it


```
.github/workflows/docker-publish.yml
```
```
name: Nginx App
on: 
 push: 
  branches: [main]

jobs:
  BuildJob:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Build Image
        run:  |
          docker build -t nginxapp:v1 .

```

Verify: Check the build step logs — does the image build successfully?

<img width="978" height="831" alt="image" src="https://github.com/user-attachments/assets/1ccc4ef3-dbb2-4030-9832-e65d861fd253" />

-----

**Task 3: Push to Docker Hub**

Add steps to:

Log in to Docker Hub using your secrets

Tag the image as username/repo:latest and also username/repo:sha-<short-commit-hash>

Push both tags

```
.github/workflows/docker-publish.yml
```
```
name: Nginx App
on: 
 push: 
  branches: [main]

jobs:
  BuildJob:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

#      - name: Build Image
#        run:  |
#          docker build -t nginxapp:v1 .

      - name: Login to Dockerhub via Secrets
        uses: docker/login-action@v3
        with: 
           username: ${{ vars.DOCKER_USERNAME }}
           password: ${{ secrets.DOCKER_TOKEN }}

      - name: Slicing the SHA 
        run:  echo "SLICED_SHA=${GITHUB_SHA:0:7}" >> $GITHUB_ENV 

      - name: Build & Push   
        uses: docker/build-push-action@v6
        with: 
          context: .
          push: true
          tags: |
              ${{ vars.DOCKER_USERNAME }}/nginxapp:latest
              ${{ vars.DOCKER_USERNAME }}/nginxapp:${{ env.SLICED_SHA }}
```
<img width="1261" height="663" alt="image" src="https://github.com/user-attachments/assets/b05329b9-3a5a-4f21-b309-eca51bb635bb" />

<img width="1580" height="846" alt="image" src="https://github.com/user-attachments/assets/948bd458-5bdb-405f-a034-e46ec8818e4b" />

* Yes , it is showing in Dockerhub 

-----

**Task 4: Only Push on Main**

Add a condition so the push step only runs on the main branch — not on feature branches or PRs

Test it: push to a feature branch and verify the image is built but NOT pushed.

```
.github/workflows/docker-publish.yml
```
```
name: Nginx App
on: 
 push: 
  branches: [main]

jobs:
  BuildJob:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

#      - name: Build Image
#        run:  |
#          docker build -t nginxapp:v1 .

      - name: Login to Dockerhub via Secrets
        uses: docker/login-action@v3
        with: 
           username: ${{ vars.DOCKER_USERNAME }}
           password: ${{ secrets.DOCKER_TOKEN }}

      - name: Slicing the SHA 
        run:  echo "SLICED_SHA=${GITHUB_SHA:0:7}" >> $GITHUB_ENV 

      - name: Build & Push   
        uses: docker/build-push-action@v6
        if:   github.ref_name == 'main'
        with: 
          context: .
          push: true
          tags: |
              ${{ vars.DOCKER_USERNAME }}/nginxapp:main
              ${{ vars.DOCKER_USERNAME }}/nginxapp:${{ env.SLICED_SHA }}

```
<img width="1165" height="632" alt="image" src="https://github.com/user-attachments/assets/044f1bac-8e9c-4826-b49e-b932533d0783" />
<img width="883" height="307" alt="image" src="https://github.com/user-attachments/assets/c823b3a5-35ca-44fe-9e55-d0714fe3b630" />

* Test it: push to a feature branch and verify the image is built but NOT pushed.
  
The iamge is built , but not pushed .
```
.github/workflows/docker-publish.yml
```
```
name: Nginx App
on: 
 push: 
  branches: [feature]

jobs:
  BuildJob:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

#      - name: Build Image
#        run:  |
#          docker build -t nginxapp:v1 .

      - name: Login to Dockerhub via Secrets
        uses: docker/login-action@v3
        with: 
           username: ${{ vars.DOCKER_USERNAME }}
           password: ${{ secrets.DOCKER_TOKEN }}

      - name: Slicing the SHA 
        run:  echo "SLICED_SHA=${GITHUB_SHA:0:7}" >> $GITHUB_ENV 

      - name: Build & Push   
        uses: docker/build-push-action@v6
        with: 
          context: .
          push: ${{ github.ref_name == 'main' }}
          tags: |
              ${{ vars.DOCKER_USERNAME }}/nginxapp:feature
              ${{ vars.DOCKER_USERNAME }}/nginxapp:${{ env.SLICED_SHA }}
```

<img width="1177" height="595" alt="image" src="https://github.com/user-attachments/assets/d4af35dd-cf9f-40a4-a365-be251bec9af1" />

------

**Task 5: Add a Status Badge**

Get the badge URL for your docker-publish workflow from the Actions tab

Add it to your README.md

Push — the badge should show green

<img width="1122" height="345" alt="image" src="https://github.com/user-attachments/assets/3e4b0eb4-9eca-4906-98cc-24c14200da4a" />

----
**Task 6: Pull and Run It**

On your local machine (or a cloud server), pull the image you just pushed

Run it

Confirm it works

Write in your notes: What is the full journey from git push to a running container?

* Starting from :

 **git push:** pushes the code from our local to remote 
 
 **git merge & commit:** merges the code with the branch 
 
 **docker build:** the CI/CD workflow runs under the actions which builds the image and push to dockerhub 
 
 **docker run:** takes(downloads) the image and runs the app in the container .



