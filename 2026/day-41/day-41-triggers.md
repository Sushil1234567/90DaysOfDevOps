**Task 1: Trigger on Pull Request**

Create .github/workflows/pr-check.yml

Trigger it only when a pull request is opened or updated against main

Add a step that prints: PR check running for branch: <branch name>

Create a new branch, push a commit, and open a PR

Watch the workflow run automatically

Verify: Does it show up on the PR page?

- yes , it showed up in the PR page.

```
.github/workflows/pr-check.yml

```
```
name: PR Check
on:
  pull_request:
    branches: [main]

jobs:
  Notify:
    runs-on: ubuntu-latest
    steps:
      - name: Print branch name
        run:  |
         echo "PR check running for the branch: ${{ github.head_ref }}"
```

<img width="1920" height="876" alt="image" src="https://github.com/user-attachments/assets/1efae16b-8d22-496b-985e-de08baf274b9" />

-----------


**Task 2: Scheduled Trigger**

Add a schedule: trigger to any workflow using cron syntax

Set it to run every day at midnight UTC

Write in your notes: What is the cron expression for every Monday at 9 AM?



```
.github/workflows/scheduled_job.yml

```
```
name: Scheduled Job
on:
  schedule:
    - cron: '0 0 * * *'

jobs:
  Scheduled Job:
    runs-on: ubuntu-latest

    steps:
      - name: Running on Interval
        run:  echo "this job is set to run every midnight"


```
- Cron Expression for every monday 9AM : 09 * * 1


----------------

**Task 3: Manual Trigger**

Create .github/workflows/manual.yml with a workflow_dispatch: trigger

Add an input that asks for an environment name (staging/production)

Print the input value in a step

Go to the Actions tab → find the workflow → click Run workflow

Verify: Can you trigger it manually and see your input printed?

- yes. this is manually triggered and we can see the input printed.

<img width="1413" height="710" alt="image" src="https://github.com/user-attachments/assets/27f3a232-2787-427b-9977-bc520536237f" />




```
.github/workflows/manual_job.yml

```
```
name: Manual Trigger

on:
  workflow_dispatch:
          inputs:
               environment:
                     description: "Select the environment"
                     required: true
                     default: staging

jobs: 
  Manual_Job:
     runs-on: ubuntu-latest
     steps: 
        - name: Prints the environment 
          run:  echo "Deploying to environment ${{ github.event.inputs.environment }}"

```
          

<img width="1066" height="882" alt="image" src="https://github.com/user-attachments/assets/69506207-3bc2-4207-8a69-320f0f5e78b1" />


----------------------


**Task 4: Matrix Builds**

Create .github/workflows/matrix.yml that:

Uses a matrix strategy to run the same job across:

Python versions: 3.10, 3.11, 3.12

Each job installs Python and prints the version

Watch all 3 run in parallel

Then extend the matrix to also include 2 operating systems — how many total jobs run now?
* [3 versions of python * 2 OS = 6 Jobs are run in total]

```
.github/workflows/matrix.yml

```
```

name: Matrix Strategy
on:
  push:
    branches:
      - main
jobs:
  Matrix:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        python versions: [3.10, 3.11, 3.12]
        os: [windows-latest, macos-latest]

        
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v6
        
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python versions: ${{ matrix.python-version }}
          
      - name: Prints the python version
        run: python --version

```

<img width="1891" height="708" alt="image" src="https://github.com/user-attachments/assets/70faf839-1ad0-4fa7-90be-a3de4a1a4d57" />

<img width="1883" height="861" alt="image" src="https://github.com/user-attachments/assets/8df3aabb-1e87-486f-9efc-b355dfecc276" />

----------

**Task 5: Exclude & Fail-Fast**

In your matrix, exclude one specific combination (e.g., Python 3.10 on Windows)

Set fail-fast: false — trigger a failure in one job and observe what happens to the rest

Write in your notes: What does fail-fast: true (the default) do vs false?

```
.github/workflows/matrix.yml

```

```
name: Matrix Strategy
on:
  push:
    branches:
      - main
jobs:
  Matrix:
    runs-on: ubuntu-latest
    
    strategy:
      fail-fast: false
     
      matrix:
        python versions: [3.10, 3.11, 3.12]
        os: [windows-latest, macos-latest]

        exclude: 
         - python versions: 3.11
           os: macos-latest
         
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v6
        
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python versions: ${{ matrix.python-version }}
          
      - name: Prints the python version
        run: python --version
```



<img width="1902" height="820" alt="image" src="https://github.com/user-attachments/assets/e51e3ecb-907b-4780-88af-7a18fd4b1433" />

----



