**Task 1: Multi-Job Workflow**

Create .github/workflows/multi-job.yml with 3 jobs:

* build — prints "Building the app"
* test — prints "Running tests"
* deploy — prints "Deploying"
  
Make test run only after build succeeds. Make deploy run only after test succeeds.

Verify: Check the workflow graph in the Actions tab — does it show the dependency chain?

```
.github/workflows/multi-job.yml
```

```
name: Multi-Job
on: 
  push:
     branches: [main]

jobs:
  Build:
     runs-on: ubuntu-latest
     steps:
       - name: Step 1
         run:  echo "Building the App"

  Test:
     runs-on: ubuntu-latest
     needs: Build
     steps:
       - name: Step 2
         run:  echo "Running Tests"

  Deploy:
     runs-on: ubuntu-latest
     needs: Test
     steps:
       - name: Step 3
         run:  echo "Deploying"
```

<img width="1892" height="562" alt="image" src="https://github.com/user-attachments/assets/187dd709-5669-4d5d-9747-0d6ad6e322b1" />

------------------

**Task 2: Environment Variables**

In a new workflow, use environment variables at 3 levels:

Workflow level — APP_NAME: myapp

Job level — ENVIRONMENT: staging

Step level — VERSION: 1.0.0

Print all three in a single step and verify each is accessible.

```
.github/workflows/environment_variables.yml
```
```
name: Environment Variables
on:
  push:
     branches: [main]

env:
  APP_NAME: myapp

jobs:
  Scope:
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: staging
      
    steps:
      - name: Prints the variable at workflow , job and step level
        env:   
          VERSION: 1.0.0
        run: |
         echo "App is: $APP_NAME "
         echo "Environment is: $ENVIRONMENT "
         echo "Version is: $VERSION "

      - name: Verify access of the variables
        run: |
         echo "$APP_NAME :workflow variables are accessible from all steps level"
         echo "$ENVIRONMENT :job variables are accessible from all steps level"
         echo "$VERSION :step variables are not accessible from all steps level "
```

<img width="1903" height="825" alt="image" src="https://github.com/user-attachments/assets/de949663-3687-461c-8524-bb07daf1d9bf" />
<img width="1877" height="828" alt="image" src="https://github.com/user-attachments/assets/4cfad619-5fc4-4804-b625-f4942e665154" />

* Variables from workflow level → accessible from all jobs and steps

* Variables from job level → accessible from all steps in that job

* Variables from step level → accessible ONLY within that same step

**Then use a GitHub context variable — print the commit SHA and the actor (who triggered the run).**
```
.github/workflows/environment_variables.yml
```
```
name: Environment Variables
on:
  push:
     branches: [main]

env:
  APP_NAME: myapp

jobs:
  Scope:
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: staging
      
    steps:
      - name: Prints the variable at workflow , job and step level
        env:   
          VERSION: 1.0.0
        run: |
         echo "App is: $APP_NAME "
         echo "Environment is: $ENVIRONMENT "
         echo "Version is: $VERSION "

      - name: Verify access of the variables
        run: |
         echo "$APP_NAME :workflow variables are accessible from all steps level"
         echo "$ENVIRONMENT :job variables are accessible from all steps level"
         echo "$VERSION :step variables are not accessible from all steps level "
           
      - name: Using Github Context Variables
        run:  |
         echo "Commit SHA: ${{ github.sha }}
         echo "This workflow is triggered by: ${{ github.actor }}
```

<img width="1880" height="816" alt="image" src="https://github.com/user-attachments/assets/d904db83-be21-4067-a21b-3301180b1862" />

-------------------

**Task 3: Job Outputs**

Create a job that sets an output — e.g., today's date as a string

Create a second job that reads that output and prints it

Pass the value using outputs: and needs.<job>.outputs.<name>

Write in your notes: Why would you pass outputs between jobs?

* Because in GitHub Actions, each job runs independently often on different machines/runners.

Common reasons to pass outputs between jobs

* Reuse computed values
* Make decisions in later jobs
* Share generated data
* Avoid duplication
* Create job dependencies


```
.github/workflows/job-outputs.yml
```
```
name: Job Outputs
on:
 push:
   branches: [main]

jobs:
  set_date:
    
    runs-on: ubuntu-latest
    steps:
      - name: Set todays date
        id:   today
        run:  echo "d=$(date)" >> $GITHUB_OUTPUT

    outputs:
      date: ${{ steps.today.outputs.d }}
          

  show_date:
    runs-on: ubuntu-latest
    needs: set_date
    steps:
      - name: Show the set date
        run:  echo "${{ needs.set_date.outputs.date }}"
```

<img width="1897" height="568" alt="image" src="https://github.com/user-attachments/assets/75218a30-6e50-48e3-8c6e-0d8e51a150c8" />

<img width="1902" height="680" alt="image" src="https://github.com/user-attachments/assets/ee26d89b-2919-47ce-ac9f-ed66caccaf0a" />

------

**Task 4: Conditionals**

In a workflow, add:

A step that only runs when the branch is main

A step that only runs when the previous step failed

A job that only runs on push events, not on pull requests

A step with continue-on-error: true — what does this do?

* continue-on-error: true   keeps the workflow continued till end despite any failure in between .

```
.github/workflows/conditions.yml
```
```
name: Conditions
on:
 push:
   branches: [main]

jobs:
  MultipleSteps:
    runs-on: ubuntu-latest
    steps:
      - name: This runs only when the branch is main
        if:   github.ref_name == 'main'
        run:  echo "This is main branch"

      - name: Failing step for the next step !
        run:  exit 1

      - name: Runs if when the previous step fails 
        if:   failure()
        run:  echo "This ran because the previos step failed"

      
        
  RunsOnPush:
    runs-on: ubuntu-latest
    if:      github.event_name == 'push'
    steps:
      - name: Prints the message
        run:  echo "Ran when event is push"

      - name: Failing step for next step !  
        run:  exit 1
        continue-on-error: true

      - name: Prints even if previous step failed
        run:  echo "Workflow continues"
        
```

<img width="1892" height="852" alt="image" src="https://github.com/user-attachments/assets/388b2a72-5339-4baa-b95b-3be22246c213" />
<img width="1891" height="851" alt="image" src="https://github.com/user-attachments/assets/aa63840c-aecc-4dbf-9daa-e7d4a00db292" />

----
**Task 5: Putting It Together**

Create .github/workflows/smart-pipeline.yml that:

Triggers on push to any branch

Has a lint job and a test job running in parallel

Has a summary job that runs after both, prints whether it's a main branch push or a feature branch push, and prints the commit message

```
.github/workflows/smart-pipeline.yml
```
```
name: Smart Pipeline
on: 
 push:

jobs:
  Lint:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "Job: ${{ github.job }}"

  Test:
    runs-on: ubuntu-latest
    steps:
      - run: |
          echo "Job: ${{ github.job }}"

  Summary:
    runs-on: ubuntu-latest
    needs: [Lint,Test]
    steps:
      - name: Prints the branch name and the commit message
        run: |
          echo "Branch name: ${{ github.ref_name }}"
          echo "Commit message:" ${{ github.event.head_commit.message }}

```
<img width="1223" height="672" alt="image" src="https://github.com/user-attachments/assets/0f069c8b-35b6-4f0b-ada2-cac219dedafa" />

----

