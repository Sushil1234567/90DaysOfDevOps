**Task 1: Build Your Own App Stack**

Create a docker-compose.yml for a 3-service stack:
* A web app (use Python Flask, Node.js, or any language you know)
* A database (Postgres or MySQL)
* A cache (Redis)
  
[CODE](https://github.com/Sushil1234567/flask-3tier-docker-app/tree/main)

---------------------------------------------------------------------------------------------
**Task 2: depends_on & Healthchecks**

 1.Add depends_on to your compose file so the app starts after the database

 2.Add a healthcheck on the database service

 3.Use depends_on with condition: service_healthy so the app waits for the database to be truly ready, not just started
 
Test: Bring everything down and up — does the app wait for the DB?
* Yes

<img width="628" height="171" alt="image" src="https://github.com/user-attachments/assets/266f5698-41c5-4855-9acc-11fbdfd5c6c0" />
<img width="647" height="95" alt="image" src="https://github.com/user-attachments/assets/c3faf9d6-d6b9-4e43-8350-116653bdbffb" />

* MySQL container starts first.
* Healthcheck waits until DB is ready.
* App container starts only after DB is healthy.

---------------------------------------------------------------------------------------------------------
**Task 3: Restart Policies**

1.Add restart: always to your database service

2.Manually kill the database container — does it come back?
* yes it is back
<img width="1215" height="283" alt="image" src="https://github.com/user-attachments/assets/98bfa6e5-f5e4-4985-859b-13ecbbd17f13" />

3.Try restart: on-failure — how is it different?
* No
  
4.Write in your notes: When would you use each restart policy?
* restart:always - Use When Databases, Backend APIs, Production services, Anything that must always run
* restart:on-failure - Use When Data processing jobs One-time migration scripts
-------------------------------------------------------------------------------------------------
**Task 4: Custom Dockerfiles in Compose**

1.Instead of using a pre-built image for your app, use build: in your compose file to build from a Dockerfile

2.Make a code change in your app

3.Rebuild and restart with one command
<img width="1898" height="580" alt="image" src="https://github.com/user-attachments/assets/2fd82aa4-af09-4976-b124-613e16c9ce44" />

---------------------------------------------------------------------------------------------------------------------------
**Task 5: Named Networks & Volumes**

1.Define explicit networks in your compose file instead of relying on the default

2.Define named volumes for database data

3.Add labels to your services for better organization

[composeFile](https://github.com/Sushil1234567/flask-3tier-docker-app/blob/main/docker-compose.yml)

---------------------------------------------------------------------------------------------------------------------------------
**Task 6: Scaling (Bonus)**

1.Try scaling your web app to 3 replicas using docker compose up --scale

2.What happens? What breaks?

3.Write in your notes: Why doesn't simple scaling work with port mapping?
<img width="788" height="258" alt="image" src="https://github.com/user-attachments/assets/b004ce82-4c4a-4dad-ab42-7090f76b580e" />
<img width="1896" height="488" alt="image" src="https://github.com/user-attachments/assets/c8d15759-6b94-488a-8cd3-fd1cfb5526ac" />

* First container started

* It binds host port 5000 = container port 5000.

* First & third containers failed

* Status:Created  means Docker couldn’t start them,port 5000 is already in use on the host.

* Docker can’t bind multiple containers to the same host port.
