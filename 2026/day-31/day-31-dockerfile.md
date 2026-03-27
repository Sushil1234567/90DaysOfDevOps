**Task 1: Your First Dockerfile**

1.Create a folder called my-first-image

2.Inside it, create a Dockerfile that:
* Uses ubuntu as the base image
* Installs curl
* Sets a default command to print "Hello from my custom image!"
<img width="957" height="676" alt="image" src="https://github.com/user-attachments/assets/3083a4a4-a951-4e01-b954-be5a51e063b7" />
3.Build the image and tag it my-ubuntu:v1
<img width="863" height="536" alt="image" src="https://github.com/user-attachments/assets/e00897e3-97cb-40a8-9ef8-3a42be87b03c" />

4.Run a container from your image
  
<img width="597" height="68" alt="image" src="https://github.com/user-attachments/assets/80d44443-b209-4032-96c0-86e2186cdcf2" />

**Task 2: Dockerfile Instructions**

Create a new Dockerfile that uses all of these instructions:

FROM — base image :                    Uses lightweight Python image based on Alpine Linux.

RUN — execute commands during build :  Sets /app as working directory inside container.

COPY — copy files from host to image : Copies everything from the my-first-image folder into /app inside container.

WORKDIR — set working directory      : Installs all Python dependencies.

EXPOSE — document the port           : Documents that container uses port 8000.

CMD — default command                : Runs Python app when container starts.

Build and run it. Understand what each line does.

<img width="975" height="287" alt="image" src="https://github.com/user-attachments/assets/5ac9152b-6777-4dfc-b24e-8bc883415250" />
<img width="1267" height="585" alt="image" src="https://github.com/user-attachments/assets/0f28e8ee-bbf6-46ba-b169-ce75a5ab4b81" />
<img width="1892" height="997" alt="image" src="https://github.com/user-attachments/assets/e295f22c-1c93-4ae9-965c-645ef31a680b" />

**Task 3: CMD vs ENTRYPOINT**

1.Create an image with CMD ["echo", "hello"] — run it, then run it with a custom command. What happens?

<img width="827" height="413" alt="image" src="https://github.com/user-attachments/assets/8381249e-2901-47a5-8149-74c9fe596ca7" />

2.Create an image with ENTRYPOINT ["echo"] — run it, then run it with additional arguments. What happens?

<img width="783" height="490" alt="image" src="https://github.com/user-attachments/assets/6a347674-c3a3-42a6-af8f-85fcaa07a1a2" />

3.Write in your notes: When would you use CMD vs ENTRYPOINT?

* Run without arguments: The container runs the default command echo hello and outputs: hello
  
* Run with a custom command: When we run the container with a custom command (e.g., echo "this is custom command"),
  the custom command completely overrides the CMD, so the output is: this is custom command

* Run without arguments: The container runs echo with no arguments,resulting in a blank output

* Run with additional arguments: When you pass arguments (e.g., hello-world), they are appended to the ENTRYPOINT,
  so it runs echo hello-world and outputs: this is a passed argument


**Task 4: Build a Simple Web App Image**

1.Create a small static HTML file (index.html) with any content

2.Write a Dockerfile that:
* Uses nginx:alpine as base
* Copies your index.html to the Nginx web directory

3.Build and tag it my-website:v1

4.Run it with port mapping and access it in your browser

<img width="1902" height="755" alt="image" src="https://github.com/user-attachments/assets/303e78fe-b7e8-403a-856d-34076130cb31" />


**Task 5: .dockerignore**
1.Create a .dockerignore file in one of your project folders
2.Add entries for: node_modules, .git, *.md, .env
3.Build the image — verify that ignored files are not included

<img width="798" height="916" alt="image" src="https://github.com/user-attachments/assets/060d880f-45c0-4c6c-9f86-31e725f2227a" />


**Task 6: Build Optimization**

1.Build an image, then change one line and rebuild — notice how Docker uses cache

2.Reorder your Dockerfile so that frequently changing lines come last

3.Write in your notes: Why does layer order matter for build speed?

ans:
* Docker builds images in layers. Each instructions (FROM, COPY, RUN) creates a new layer.
* Docker caches layers, so all layers before any unchanged instruction is not rebuilt, used from cache.
* If a layer changes, all layers after it are rebuilt.
* Placing frequently changing layers last, ensures maximum use of cache and minimum rebuild time.
* Provides faster and efficient builds.
