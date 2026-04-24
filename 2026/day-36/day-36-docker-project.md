**Task 1: Pick Your App**

Choose one of these (or use your own project):

* A Python Flask/Django app with a database
* A Node.js Express app with MongoDB
* A static website served by Nginx with a backend API
* Any app from your GitHub that doesn't have Docker yet
  
If you don't have an app, clone a simple open-source one and Dockerize it.

[APP](https://github.com/Sushil1234567/ToDoApp.git)

---------------------------------------------------------------------------------------------------------------

**Task 2: Write the Dockerfile**

1.Create a Dockerfile for your application

2.Use a multi-stage build if applicable

3.Use a non-root user

4.Keep the image small — use alpine or slim base images

5.Add a .dockerignore file

Build and test it locally.

[Dockerfile](https://github.com/Sushil1234567/ToDoApp/blob/main/Dockerfile)

---------------------------------------------------------------------------------------------------------------


**Task 3: Add Docker Compose**

Write a docker-compose.yml that includes:

1.Your app service (built from Dockerfile)

2.A database service (Postgres, MySQL, MongoDB — whatever your app needs)

3.Volumes for database persistence

4.A custom network

5.Environment variables for configuration (use .env file)

6.Healthchecks on the database

Run docker compose up and verify everything works together.


* Used the default sqlite3 db from Django, therefore it does not need a database service or volume persistence
  
[DockerCompose](https://github.com/Sushil1234567/ToDoApp/blob/main/docker-compose.yml)

[.envfile](https://github.com/Sushil1234567/ToDoApp/blob/main/docker-compose.yml)

--------------------------------------------------------------------------------------------------------------
**Task 4: Ship It**

1.Tag your app image

2.Push it to Docker Hub

3.Share the Docker Hub link

4.Write a README.md in your project with:
* What the app does
* How to run it with Docker Compose
* Any environment variables needed

[Dockerhub](https://hub.docker.com/repository/docker/broaduse/todoapp_web/tags)

----------------------------------------------------------------------------------------------------------------

**Task 5: Test the Whole Flow**

Remove all local images and containers

Pull from Docker Hub and run using only your compose file

Does it work fresh? If not — fix it until it does

* Yes , it is up and running .

<img width="1192" height="687" alt="image" src="https://github.com/user-attachments/assets/8aecb10e-54ad-481e-8d2e-650eb92122bd" />

----------------------------------------------------------------------------------------------------------------------------------------------

**SCREENSHOTS**

<img width="655" height="960" alt="image" src="https://github.com/user-attachments/assets/b5c55865-c7ad-40c2-8a2e-21d87526a63e" />

-------------
<img width="1188" height="993" alt="image" src="https://github.com/user-attachments/assets/764ee0b1-53ff-45bb-81ed-11ba43bad134" />

------------
<img width="658" height="422" alt="image" src="https://github.com/user-attachments/assets/67aa9a2a-644a-42dd-a4d2-4da7f3aa0db5" />

------------
<img width="1222" height="658" alt="image" src="https://github.com/user-attachments/assets/2a315a67-dc94-4323-9ef1-ac1e1e9b5e31" />

------------
<img width="906" height="652" alt="image" src="https://github.com/user-attachments/assets/5ec0fecc-25fb-42fa-b824-edceb13d42a8" />

------------
<img width="742" height="451" alt="image" src="https://github.com/user-attachments/assets/8d7a308a-54bd-43bb-8d91-431e030a65e6" />






