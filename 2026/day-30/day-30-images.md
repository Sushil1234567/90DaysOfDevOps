**Task 1: Docker Images**

1.Pull the nginx, ubuntu, and alpine images from Docker Hub
<img width="732" height="462" alt="image" src="https://github.com/user-attachments/assets/1399f70b-2f61-48b9-a433-5ae0a6cfcc1e" />

2.List all images on your machine — note the sizes
<img width="562" height="172" alt="image" src="https://github.com/user-attachments/assets/94f968cb-358c-4d72-b20d-f1aca835bd4c" />

3.Compare ubuntu vs alpine — why is one much smaller?

ans: Docker Alpine images are small because they are based on the Alpine Linux distribution, which is designed for resource efficiency and built with a minimalist set of 
core components instead of a full suite of utilities found in larger distributions like Ubuntu or Debian.

4.Inspect an image — what information can you see?

<img width="1166" height="806" alt="image" src="https://github.com/user-attachments/assets/7466b397-f909-406b-9d59-1599dfbb648e" />
we see informations related to : 

* Image id,
* Created date,
* OS
* Size
  
5.Remove an image you no longer need
<img width="793" height="265" alt="image" src="https://github.com/user-attachments/assets/c272e392-9fc6-44bf-a3f1-dd327874feda" />

**Task 2: Image Layers**

1.Run docker image history nginx — what do you see?
<img width="1006" height="362" alt="image" src="https://github.com/user-attachments/assets/582d959c-7298-4c40-9ab6-5a9b00757540" />

2.Each line is a layer. Note how some layers show sizes and some show 0B

3.Write in your notes: What are layers and why does Docker use them?

Docker image layers are created with every changes made to the file system.
Every instruction in dockerfile creates a separate layer (FROM, COPY, RUN, CMD etc).
Layers are very important as docker caches every layer while creating the image and stores it in docker engine.
Now if you recreate after changing docker uses cached layers for unchanged layers. 
Hence images are build faster and more efficient.

**Task 3: Container Lifecycle**
Practice the full lifecycle on one container:

1.Create a container (without starting it)

<img width="1172" height="191" alt="image" src="https://github.com/user-attachments/assets/867179c2-8eae-4ccf-95f4-ed99367f301b" />

2.Start the container

<img width="1185" height="172" alt="image" src="https://github.com/user-attachments/assets/a9eda2c5-adc6-4bbf-8f23-51d4889a88e2" />

3.Pause it and check status
<img width="1185" height="180" alt="image" src="https://github.com/user-attachments/assets/751548d0-bae3-4ef7-927a-3e167003c2c2" />

4.Unpause it
<img width="1182" height="175" alt="image" src="https://github.com/user-attachments/assets/83151628-b018-4e06-a8b1-80601de6851d" />

5.Stop it
<img width="1206" height="177" alt="image" src="https://github.com/user-attachments/assets/86a9effb-15ac-4709-ab46-c0794c46d6bb" />

6.Restart it
<img width="1187" height="172" alt="image" src="https://github.com/user-attachments/assets/c99e6a6d-4c7e-4099-945b-7deaa3be01f8" />

7.Kill it
<img width="1197" height="162" alt="image" src="https://github.com/user-attachments/assets/857353ad-7e14-489d-b6b4-fa3485481f2f" />

8.Remove it
<img width="1180" height="583" alt="image" src="https://github.com/user-attachments/assets/fec27f2b-c18f-4d80-b4ab-15e0fa8abbe0" />

Check docker ps -a after each step — observe the state changes.

**Task 4: Working with Running Containers**

1.Run an Nginx container in detached mode
<img width="1317" height="72" alt="image" src="https://github.com/user-attachments/assets/968cc1e1-e0b1-4014-86aa-89055ab7d13f" />

2.View its logs
<img width="887" height="311" alt="image" src="https://github.com/user-attachments/assets/40d0b78b-87c2-4248-a5aa-521e9d4659c1" />

3.View real-time logs (follow mode)
<img width="872" height="307" alt="image" src="https://github.com/user-attachments/assets/463cca5a-59be-4028-a91e-41035b94b2db" />

4.Exec into the container and look around the filesystem
<img width="1505" height="482" alt="image" src="https://github.com/user-attachments/assets/6c9c33f5-c79e-4971-aa52-a5d6f7fdcec4" />

5.Run a single command inside the container without entering it
<img width="647" height="553" alt="image" src="https://github.com/user-attachments/assets/e95c5298-db5c-4adc-a944-2c9a35bf4629" />

6.Inspect the container — find its IP address, port mappings, and mounts
<img width="962" height="756" alt="image" src="https://github.com/user-attachments/assets/8660da7d-4a90-4611-802b-9330177faa25" />

**Task 5: Cleanup**

1.Stop all running containers in one command

<img width="512" height="538" alt="image" src="https://github.com/user-attachments/assets/4dbd7f93-f109-4abd-884b-47e897540161" />

2.Remove all stopped containers in one command

<img width="498" height="556" alt="image" src="https://github.com/user-attachments/assets/65bf383f-393e-4a88-8641-fdb2e54c70c1" />

3.Remove unused images

<img width="867" height="705" alt="image" src="https://github.com/user-attachments/assets/a61666a6-2a0b-4c93-9d67-b272b865ee98" />

4.Check how much disk space Docker is using

<img width="553" height="133" alt="image" src="https://github.com/user-attachments/assets/f3ad3b08-4034-491d-9e53-beaef6b31dd9" />
