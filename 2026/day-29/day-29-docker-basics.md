**Task 1: What is Docker?**
Research and write short notes on:

* What is a container and why do we need them?
  
ans: Container is a package that bundles an application with all the necessary dependencies and configuration it requires.

This is useful for ease of shearability and make deployment and development smoother and efficient.

* Containers vs Virtual Machines — what's the real difference?

ans: Virtual machines consumed a definite space from the base machine regardless of its usage, this occupied space would be of now use when not in use.

Whereas in case of containers didnt have any fixed OS and hence the space was optimised, it occupied space in realtime only when a specific software is in use(run),
rest of the time, this same space would be alloted to other software which is running this way it consumed very less hard disk and hence the space were optimised .

* What is the Docker architecture? (daemon, client, images, containers, registry)

ans: 



**Task 2: Install Docker**

1.Install Docker on your machine (or use a cloud instance)

2.Verify the installation

3.Run the hello-world container

4.Read the output carefully — it explains what just happened

<img width="767" height="458" alt="image" src="https://github.com/user-attachments/assets/926ae392-6568-4213-a7eb-e6dd75a37272" />

**Task 3: Run Real Containers**
1.Run an Nginx container and access it in your browser

<img width="875" height="338" alt="image" src="https://github.com/user-attachments/assets/80a7d07d-e478-47bc-8c42-7cf703f33dd6" />
<img width="722" height="360" alt="image" src="https://github.com/user-attachments/assets/ab2c708e-4aa1-491f-b930-c1608855f936" />


2.Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
<img width="941" height="530" alt="image" src="https://github.com/user-attachments/assets/c41f363d-48d4-42d7-9d4a-467cca65f819" />


3.List all running containers
<img width="1238" height="85" alt="image" src="https://github.com/user-attachments/assets/780ba120-5ab8-4384-b584-2d4914be9542" />

4.List all containers (including stopped ones)
<img width="1517" height="505" alt="image" src="https://github.com/user-attachments/assets/db19695f-8827-4212-849f-0889c54144ac" />

5.Stop and remove a container
<img width="1487" height="472" alt="image" src="https://github.com/user-attachments/assets/e305e145-2951-4338-ac22-b25c14bd879a" />


**Task 4: Explore**
1.Run a container in detached mode — what's different?

* Running a container in detached mode frees terminal, container run in background, we only get container id and manage it using docker commands with its id.
  
* Running directly without -d, runs it in foreground, it shows live logs.outputs, pressing ctl+c stops it and exits container.

2.Give a container a custom name
<img width="1226" height="116" alt="image" src="https://github.com/user-attachments/assets/3c080e3f-284e-425c-a144-6cd72748f38e" />

3.Map a port from the container to your host
<img width="702" height="42" alt="image" src="https://github.com/user-attachments/assets/bdcda8e8-7830-424c-9512-3169b55707f2" />

4.Check logs of a running container
<img width="880" height="360" alt="image" src="https://github.com/user-attachments/assets/dcb0e344-81cf-439e-bd08-b76ae456fcc1" />

5.Run a command inside a running container

<img width="555" height="208" alt="image" src="https://github.com/user-attachments/assets/07e25556-2f2b-4feb-b4a0-ed810b39502f" />


