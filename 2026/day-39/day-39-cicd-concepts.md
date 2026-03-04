**Task 1: The Problem**

Think about a team of 5 developers all pushing code to the same repo manually deploying to production.
Write in your notes:

1.What can go wrong?

ans: 
When more than one developer pushes code manually and deploying to production, there could be high chance 
of facing race condition issues leading to creating inconsistent environments and production downtime and data losses aswell.

2.What does "it works on my machine" mean and why is it a real problem?

ans: 
It simply means that the code is not portable which has dependencies that only the local system has. This is a real problem because
there is no scope for collaboration or development of products.

3.How many times a day can a team safely deploy manually?

ans:
Mostly deployment should be only once a day mannually, there is high risk of environmemnt issues if done multiple times.



**Task 2: CI vs CD**

Research and write short definitions (2-3 lines each):
1. Continuous Integration — what happens, how often, what it catches
2. Continuous Delivery — how it's different from CI, what "delivery" means
3. Continuous Deployment — how it differs from Delivery, when teams use it
Write one real-world example for each.

ans:

Continuous Integration — 

Continious integration (CI) is the process of multiple developers merging thir code changes with main code repository
of a project . 
ex: a developer pushing the code to GitHub triggering a jenkins pipeline. 

Continious Delivery —

Continious delivery is the next step after continious integration, responsible for packaging the artifacts together 
to end users. this build phase is kept 'green' indicating the artifact is ready to deploy at any time.
ex : code commits by a group of people using a pipeling like gitHub actions or jenkins which automatically builds, tests
and deploys to staging

Continuous Deployment —

This is the final phase of the pipeline which ensures automatic launching and distributing software artifact to the
end users. This is done through scripts and tools that automate the process.
ex: any application that releases the changes after automated tests skipping mannual approval ex: netflix, linkedin 



**Task 3: Pipeline Anatomy**

A pipeline has these parts — write what each one does:

* Trigger — what starts the pipeline :
  This is an event that automatically initiates the a workflow of a CICD job.
  
* Stage — a logical phase (build, test, deploy):
  The process of breaking down to managable small units to complete a specific criteria .
  
* Job — a unit of work inside a stage:
  A job is the smallest unit of many set of actions in a larger workflow/pipeline.
  
* Step — a single command or action inside a job:
  It is a single executable command or a task which is part of larger job that belongs to a stage in
  CICD pipeline.
   
* Runner — the machine that executes the job:
  This is an agent which executes the tasks that are defined in the pipeline config. file
  
* Artifact — output produced by a job:
  It is a file that is generated after completion of a job , this could be used at later stages for
  deployment
  


**Task 4: Draw a Pipeline**

Draw a CI/CD pipeline for this scenario:

A developer pushes code to GitHub. The app is tested, built into a Docker image, and deployed to a staging server.

Include at least 3 stages. Hand-drawn and photographed is perfectly fine.

![20260304_153945 1](https://github.com/user-attachments/assets/6aa83c0a-2611-4194-9cc3-850dc3f74e86)


**Task 5: Explore in the Wild**

Open any popular open-source repo on GitHub (Kubernetes, React, FastAPI — pick one you know)

Find their .github/workflows/ folder
Open one workflow YAML file
Write in your notes:

* What triggers it?
  
ans: Events like push triggers the job to execute the jobs . It can also be triggered by scheduling like a cronjob
 
* How many jobs does it have?

ans: It has 2 jobs : 1.build  2.Test 

* What does it do? (best guess)
  
ans: 
-Check out the repository code 

-Set up the necessary environment

-Build the application from the source code.

-Run unit and integration tests to ensure code quality and functionality.


