**Task 2: Your First Compose File**

1.Create a folder compose-basics

2.Write a docker-compose.yml that runs a single Nginx container with port mapping

3.Start it with docker compose up

4.Access it in your browser
<img width="1487" height="527" alt="image" src="https://github.com/user-attachments/assets/d565dd70-6dd3-4c32-b2de-52e61f16dded" />

5.Stop it with docker compose down
<img width="1491" height="702" alt="image" src="https://github.com/user-attachments/assets/e2eb6571-0aa7-4ac9-9e17-c02323f95c34" />

-------------------------------------------------------------------------------------------------------------------------------------


**Task 3: Two-Container Setup**

Write a docker-compose.yml that runs:

* A WordPress container
* A MySQL container

They should:
* Be on the same network (Compose does this automatically)
* MySQL should have a named volume for data persistence
* WordPress should connect to MySQL using the service name
Start it, access WordPress in your browser, and set it up.

<img width="1575" height="998" alt="image" src="https://github.com/user-attachments/assets/a0f3903d-3d1b-4484-8e7d-d541d200968a" />

* docker compose down
<img width="1565" height="996" alt="image" src="https://github.com/user-attachments/assets/e5a16fab-6fee-4d45-bbe0-934427f822ca" />

* docker compose up
<img width="1566" height="997" alt="image" src="https://github.com/user-attachments/assets/0b6e3c53-bea5-4a4b-ae8a-23818f35c692" />



---------------------------------------------------------------------------------------------------------------------------------------

**Task 4: Compose Commands**

Practice and document these:

1.Start services in detached mode

<img width="593" height="278" alt="image" src="https://github.com/user-attachments/assets/45b0a64b-33f5-462d-bf6a-1ac00ed5da2a" />

2.View running services

<img width="861" height="110" alt="image" src="https://github.com/user-attachments/assets/0d072432-4bbe-4443-88fe-e5053085c9d2" />

3.View logs of all services

<img width="1892" height="998" alt="image" src="https://github.com/user-attachments/assets/90061f5a-732e-42bd-bb25-4b8ed4132e14" />

4.View logs of a specific service

<img width="1892" height="375" alt="image" src="https://github.com/user-attachments/assets/95b000a7-5386-4ea4-9779-fa76b432211b" />

5.Stop services without removing

<img width="612" height="63" alt="image" src="https://github.com/user-attachments/assets/4d433f4d-17fc-46d6-b91a-646ac5f4ce02" />

6.Remove everything (containers, networks)

<img width="590" height="112" alt="image" src="https://github.com/user-attachments/assets/e478eff5-6e31-4414-a590-8544ccd8276f" />

7.Rebuild images if you make a change

* docker compose up --build.

------------------------------------------------------------------------------------------------------------------

**Task 5: Environment Variables**

1.Add environment variables directly in your docker-compose.yml

2.Create a .env file and reference variables from it in your compose file

3.Verify the variables are being picked up


<img width="591" height="912" alt="image" src="https://github.com/user-attachments/assets/b2051551-eef0-4cec-817a-a57d2bd2acc5" />
<img width="852" height="257" alt="image" src="https://github.com/user-attachments/assets/02ce13af-0ba6-4379-86a7-766d66ca1a92" />


