**Task 1: The Problem**

1.Run a Postgres or MySQL container
<img width="972" height="331" alt="image" src="https://github.com/user-attachments/assets/36a6277d-c6ef-4f83-a51a-16e50e4620ba" />

2.Create some data inside it (a table, a few rows — anything)
<img width="1121" height="572" alt="image" src="https://github.com/user-attachments/assets/38dbcec8-8075-42d2-a84f-08069e65ff32" />

3.Stop and remove the container

<img width="651" height="108" alt="image" src="https://github.com/user-attachments/assets/6f56c072-fd19-4b7d-91a3-81ce39c39ca2" />

4.Run a new one — is your data still there?

The data is deleted .
<img width="992" height="236" alt="image" src="https://github.com/user-attachments/assets/858e0c39-79b1-4021-af93-384ab912501e" />

Write what happened and why.

The postgres table was deleted along with the container,when a Docker container is removed, any database data stored inside it is deleted. 
Containers are ephemeral, meaning their writable file system layer is temporary.

----------------------------------------------------------------------------------------------------
**Task 2: Named Volumes**

1.Create a named volume

2.Run the same database container, but this time attach the volume to it

3.some data, stop and remove the container

4.Run a brand new container with the same volume

<img width="1217" height="637" alt="image" src="https://github.com/user-attachments/assets/ad25a1c6-d79b-4fe2-9914-395afe309ccd" />
<img width="680" height="552" alt="image" src="https://github.com/user-attachments/assets/bf3c3b3f-e3e8-4ee3-ac32-ab74d7b19362" />

5.Is the data still there?

Yes, the data exists as we have succesfully mapped the volume to the second container.

----------------------------------------------------------------------------------------------------------

**Task 3: Bind Mounts**

1.Create a folder on your host machine with an index.html file

2.Run an Nginx container and bind mount your folder to the Nginx web directory

3.Access the page in your browser

<img width="1897" height="510" alt="image" src="https://github.com/user-attachments/assets/38b03ddb-9bc2-4072-ac68-180fbaba60f8" />

4.Edit the index.html on your host — refresh the browser

<img width="1897" height="890" alt="image" src="https://github.com/user-attachments/assets/f9093135-c5df-4c11-8397-50664b936ab4" />

Write in your notes: What is the difference between a named volume and a bind mount?

ans:  Named volume only maps the data in the container to our local , inorder to persist the data even if the container is deleted/lost.

There is no real time data mapping aswell . It is kind of a backup of the data from container.

Bind mount is the real time mapping of the data in our host/local to a container. we can see the continuous live changes made in the local reflects in the container at the same time as if both are connected live.

--------------------------------------------------------------------------------------------------------------------------------

**Task 4: Docker Networking Basics**

1.List all Docker networks on your machine

<img width="522" height="87" alt="image" src="https://github.com/user-attachments/assets/4e323746-4e39-4988-892f-73bdf37103c9" />

2.Inspect the default bridge network
<img width="881" height="818" alt="image" src="https://github.com/user-attachments/assets/5ef582d1-73f0-45fe-b4c3-75f12c848bb6" />

3.Run two containers on the default bridge — can they ping each other by name?
* No, they cant ping each other.
<img width="657" height="142" alt="image" src="https://github.com/user-attachments/assets/6bd0fa18-7326-492a-a249-716d7957a0dc" />

4.Run two containers on the default bridge — can they ping each other by IP?
* yes, they can ping now.
<img width="537" height="502" alt="image" src="https://github.com/user-attachments/assets/492c0c41-40d1-4b08-bc72-3a4a203fff46" />

---------------------------------------------------------------------------------------------------------------------------------------
**Task 5: Custom Networks**

1.Create a custom bridge network called my-app-net

2.Run two containers on my-app-net

3.Can they ping each other by name now?

* yes, they can ping now.

<img width="898" height="556" alt="image" src="https://github.com/user-attachments/assets/b6e38e7b-ff14-4521-98b0-9057468d7aad" />


4.Write in your notes: Why does custom networking allow name-based communication but the default bridge doesn't?

ans: Custom networking allows name-based communication because Docker automatically provides an embedded DNS server that maps container names to IP addresses. 

But the default bridge network does not provide DNS server, hence requires container communication to be done via IP addresses only.

-----------------------------------------------------------------------------------------------------------------------------------------

**Task 6: Put It Together**

1.Create a custom network

2.Run a database container (MySQL/Postgres) on that network with a volume for data

3.Run an app container (use any image) on the same network

4.Verify the app container can reach the database by container name

<img width="1441" height="367" alt="image" src="https://github.com/user-attachments/assets/4ffd6999-62ea-4f61-b845-21967e44c709" />


