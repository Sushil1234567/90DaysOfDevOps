**Task 1: The Problem with Large Images**

1.Write a simple Go, Java, or Node.js app (even a "Hello World" is fine)

2.Create a Dockerfile that builds and runs it in a single stage

3.Build the image and check its size

Note down the size — you'll compare it later.

<img width="781" height="912" alt="image" src="https://github.com/user-attachments/assets/883a0ebb-a495-4135-b2fc-44367149445a" />


**Task 2: Multi-Stage Build**

1.Rewrite the Dockerfile using multi-stage build:
* Stage 1: Build the app (install dependencies, compile)
* Stage 2: Copy only the built artifact into a minimal base image (alpine , distroless , or scratch )
  
2.Build the image and check its size again

3.Compare the two sizes
<img width="788" height="582" alt="image" src="https://github.com/user-attachments/assets/990c9852-0c1b-4044-8688-2a4aede5f401" />

<img width="782" height="845" alt="image" src="https://github.com/user-attachments/assets/7cb7498e-e2c3-4860-bbf5-b9a4301fad4e" />

Write in your notes: Why is the multi-stage image so much smaller?

* Multi-stage builds smaller images because they separate “build” from “runtime”, copying only what’s necessary into the final image.


**Task 3: Push to Docker Hub**

1.Create a free account on Docker Hub (if you don't have one)

2.Log in from your terminal

3.Tag your image properly: yourusername/image-name:tag

4.Push it to Docker Hub

<img width="902" height="652" alt="image" src="https://github.com/user-attachments/assets/77dd1f98-aefd-4bbf-987c-ee70cc1eee69" />


<img width="1430" height="880" alt="image" src="https://github.com/user-attachments/assets/eae437f7-e78f-41ea-93c5-67e97b0f9036" />

5.Pull it on a different machine (or after removing locally) to verify

<img width="921" height="177" alt="image" src="https://github.com/user-attachments/assets/2841596c-5fe9-438e-bf73-f0dbcdbb434c" />


**Task 4: Docker Hub Repository**

1.Go to Docker Hub and check your pushed image

2.Add a description to the repository

3.Explore the tags tab — understand how versioning works

4.Pull a specific tag vs latest — what happens?
<img width="1898" height="877" alt="image" src="https://github.com/user-attachments/assets/921d467a-736d-40c8-8c4c-f6b2508f39f8" />

