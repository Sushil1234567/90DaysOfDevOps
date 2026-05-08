**Task 1: GitHub-Hosted Runners**

Create a workflow with 3 jobs, each on a different OS:

* ubuntu-latest

* windows-latest

* macos-latest

In each job, print:

* The OS name

* The runner's hostname

* The current user running the job

Watch all 3 run in parallel

Write in your notes: What is a GitHub-hosted runner? Who manages it?

```
.github/workflows/githubHostedRunner.yml
```
```
name: Github Hosted Runner
on: 
 push:
   branches: [main]

jobs:
 Job1:
  runs-on: ubuntu-latest
  
  steps:
   - name: Prints the OS name
     run:  echo "The OS name is ${{ runner.os }}"
   
   - name: Prints runners hostname
     run:  echo "The runners hostname is $HOSTNAME "

   - name: Prints the current user running the job
     run:  echo "The current user running the job is ${{ github.actor }}"  
   

 Job2:
  runs-on: windows-latest
  
  steps:
   - name: Prints the OS name
     run:  echo "The OS name is ${{ runner.os }}"
  
   - name: Prints runners hostname
     run:  echo "The runners hostname is $HOSTNAME "

   - name: Prints the current user running the job
     run:  echo "The current user running the job is ${{ github.actor }}"  
    


 Job3:
  runs-on: macos-latest
  
  steps:
   - name: Prints the OS name
     run:  echo "The OS name is ${{ runner.os }}"
     
   - name: Prints runners hostname
     run:  echo "The runners hostname is $HOSTNAME "

   - name: Prints the current user running the job
     run:  echo "The current user running the job is ${{ github.actor }}"
```
<img width="1882" height="747" alt="image" src="https://github.com/user-attachments/assets/6210fc1b-c296-4300-95c8-6fe09c31f89c" />
<img width="1883" height="852" alt="image" src="https://github.com/user-attachments/assets/c58eb7ab-f8d4-43a3-88c5-720339f3018e" />
<img width="1880" height="767" alt="image" src="https://github.com/user-attachments/assets/91f1ed89-24b2-4886-b64d-47d435df7fe0" />


* GitHub hosted runners are virtual machines to run workflows, they are managed by Microsoft Azure .

-------

**Task 2: Explore What's Pre-installed**

On the ubuntu-latest runner, run a step that prints:

* Docker version

* Python version

* Node version

* Git version

Look up the GitHub docs for the full list of pre-installed software on ubuntu-latest

Write in your notes: Why does it matter that runners come with tools pre-installed?

```
.github/workflows/displayVersion.yml
```
```
name: Installed Versions
on:
 push:
   branches: [main]

jobs:
  Display_Version:
     runs-on: ubuntu-latest

     steps:
       - name: Display Docker Version
         run:  docker --version

       - name: Display Python Version
         run:  python --version

       - name: Display Node Version
         run:  node --version

       - name: Display Git Version
         run:  git --version
```

<img width="1887" height="865" alt="image" src="https://github.com/user-attachments/assets/8dfe3432-1883-465f-819d-ca9b72192b36" />

* GitHub-hosted runners come with preinstalled tools to provide a fast, ready-to-use, and standardized environment for developers. 
By including common software like Git, Docker, and various language runtimes, runners eliminate the need to spend time installing dependencies at the start of every job.

-----

**Task 3: Set Up a Self-Hosted Runner**

Go to your GitHub repo → Settings → Actions → Runners → New self-hosted runner

Choose Linux as the OS

Follow the instructions to download and configure the runner on:

Your local machine, OR

A cloud VM (EC2, Utho, or any VPS)

Start the runner — verify it shows as Idle in GitHub

Verify: Your runner appears in the Runners list with a green dot.

<img width="820" height="690" alt="image" src="https://github.com/user-attachments/assets/393eec63-8b3a-468f-b147-ce9ed24709bc" />
<img width="997" height="311" alt="image" src="https://github.com/user-attachments/assets/6012f472-991c-42de-a9d0-5655e41cf249" />

-----

**Task 4: Use Your Self-Hosted Runner**

Create .github/workflows/self-hosted.yml

Set runs-on: self-hosted

Add steps that:

Print the hostname of the machine (it should be YOUR machine/VM)

Print the working directory

Create a file and verify it exists on your machine after the run

Trigger it and watch it run on your own hardware

Verify: Check your machine — is the file there?
```
.github/workflows/self-hosted.yml
```

```
name: Self Hosted Runner
on:
  push:
    branches: [main]
      
      
jobs:
  Runner:
    runs-on: self-hosted
    
    steps:
      - name: Prints Hostname
        run: hostname
       
      - name: Prints working directory
        run: pwd
       
      - name: Create a file
        run:  touch FileCreated.txt
```


<img width="775" height="785" alt="image" src="https://github.com/user-attachments/assets/fa07505f-7d19-40cb-b91f-5762f6e124dd" />

<img width="1885" height="848" alt="image" src="https://github.com/user-attachments/assets/d3292d28-6d1e-4fa6-b49e-e227cb1ff232" />

<img width="1031" height="200" alt="image" src="https://github.com/user-attachments/assets/15123567-1228-4d68-bdb9-d6e53614cfe7" />

-------

**Task 5: Labels**

Add a label to your self-hosted runner (e.g., my-linux-runner)

Update your workflow to use runs-on: [self-hosted, my-linux-runner]

Trigger it — does it still pick up the job?

Write in your notes: Why are labels useful when you have multiple self-hosted runners?

* Labels help GitHub decide which specific self-hosted runner should execute a job when you have multiple runners.
  Without labels, GitHub may not know which machine is suitable for a particular workflow.

```
.github/workflows/self-hosted.yml
```
```
name: Self Hosted Runner
on:
  push:
    branches: [main]
      
      
jobs:
  Runner:
    runs-on: [self-hosted, custom]
    
    steps:
      - name: Prints Hostname
        run: hostname
       
      - name: Prints working directory
        run: pwd
       
      - name: Create a file
        run:  touch FileCreated.txt

```
<img width="1882" height="852" alt="image" src="https://github.com/user-attachments/assets/31b89070-4361-4643-ad56-df2b634a48da" />
<img width="1013" height="148" alt="image" src="https://github.com/user-attachments/assets/708fb24d-64b6-40ec-9fa9-1ed120bb9cf9" />

----

**Task 6: GitHub-Hosted vs Self-Hosted**

Fill this in your notes:

| | GitHub-Hosted | Self-Hosted |
| ---|---|---|
| Who manages it? | GitHub (fully managed) | 	You (your machine or VM) |
| Cost | Included in free tier minutes; billed beyond that | Free to run; you pay for your own infrastructure |
| Pre-installed tools | Docker, Python, Node, Git, etc. | what is install by us |
| Good for | Most CI/CD tasks, open source, standard builds | Specialized hardware, private networks, GPU jobs, cost optimization at scale |
| Security concern | Isolated ephemeral VM — safe for public repos | Persistent machine — untrusted PRs can run arbitrary code on your hardware |

