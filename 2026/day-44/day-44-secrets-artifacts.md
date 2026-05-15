**Task 1: GitHub Secrets**

Go to your repo → Settings → Secrets and Variables → Actions

Create a secret called MY_SECRET_MESSAGE

Create a workflow that reads it and prints: The secret is set: true (never print the actual value)

```
.github/workflows/secretmessage.yml
```
```
name: My Secret Message
on:
 push:

jobs:
  check_secrets:
    runs-on: ubuntu-latest
    steps:
      - name: Checks if secret exists or not
        env:  
          SECRET: ${{ secrets.MY_SECRET_MESSAGE }}
        run: |
          if [ -n "$SECRET" ]; then
             echo "The secret is set : true"
          else
             echo "No Secrets found"
          fi 

  print_secrets:
    runs-on: ubuntu-latest
    steps:
      - name: Prints the secrets
        env:  
          SECRET: ${{ secrets.MY_SECRET_MESSAGE }}
        run:  echo "$SECRET"
```
<img width="1077" height="676" alt="image" src="https://github.com/user-attachments/assets/2f2b8e2b-46c8-4fa4-88c3-216af7a2486e" />


Try to print ${{ secrets.MY_SECRET_MESSAGE }} directly — what does GitHub show?

* Github prints the content in: *** , as a hidden value.
<img width="1110" height="658" alt="image" src="https://github.com/user-attachments/assets/86be9808-8d94-4fd0-8160-50d6b4a10f16" />


* Write in your notes: Why should you never print secrets in CI logs?
  
Secrets should never be printed in CI logs for preventing public users from knowing the sensitive values and variables of our repository.

------

**Task 2: Use Secrets as Environment Variables**

Pass a secret to a step as an environment variable

Use it in a shell command without ever hardcoding it

Add DOCKER_USERNAME and DOCKER_TOKEN as secrets (you'll need these on Day 45)

```
.github/workflows/env_var_secrets.yml
```
```
name: Environmnet Variable Secrets
on: 
 push:

   
jobs:
  variable:
    runs-on: ubuntu-latest
    steps:
      - name: Passing variables
        env:
          DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
          DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
        run: |
          echo "$DOCKER_USERNAME" > envfile.txt
          echo "$DOCKER_TOKEN" >> envfile.txt
```
<img width="1070" height="741" alt="image" src="https://github.com/user-attachments/assets/f3cdadad-9bf2-43f7-973a-d6cccbc1da4a" />

----


**Task 3: Upload Artifacts**

1.Create a step that generates a file — e.g., a test report or a log file

2.Use actions/upload-artifact to save it

3.After the workflow runs, download the artifact from the Actions tab

Verify: Can you see and download it from GitHub?
* yes, this can be downloaded and see the logs in the downloaded file

```
.github/workflows/upload.yml
```
```
name: Upload Artifacts
on: 
 push:
   branches: [main]

jobs:
  Upload:
    runs-on: ubuntu-latest
    steps:
      - name: Generates Logs
        run: |
          echo "Timestamp: $(date)" > logfile.txt
          echo "Runner OS: $RUNNER_OS" >> logfile.txt
      - name: Upload Logs
        uses: actions/upload-artifact@v4
        with:
          name: execution-logs
          path: logfile.txt
        
```
<img width="1882" height="836" alt="image" src="https://github.com/user-attachments/assets/3dde7f47-d1b7-4a16-86c7-2b33a7ef66e3" />

----

**Task 4: Download Artifacts Between Jobs**

Job 1: generate a file and upload it as an artifact

Job 2: download the artifact from Job 1 and use it (print its contents)

Write in your notes: When would you use artifacts in a real pipeline?

* Cross-Job Data Sharing:
  To pass compiled code or build outputs from one isolated job to another
  (e.g., Job 1 builds a production-ready application, and Job 2 pulls that build to deploy it to a server).
  
* Pipeline Speed Optimization:
  To separate long-running build phases from deployment/test phases.
  You compile the software once, save it as an artifact, and reuse that exact same file across multiple parallel testing jobs.
  
* Auditing and Compliance:
 To permanently save critical deployment logs, security scan results, or test coverage reports
 so external teams or regulators can download them later from the GitHub UI.

```
.github/workflows/downloadartifacts.yml
```
```
name: Download Artifacts
on: 
 push:
   branches: [main]

jobs:
  Job-1:
    runs-on: ubuntu-latest
    steps:
      - name: Generate Logs
        run: |
          echo "---Generating Logs---" > generate.txt
          echo "Workspace path: $GITHUB_WORKSPACE" >> generate.txt
          echo "Username: $GITHUB_ACTOR" >> generate.txt

      - name: Upload Logs
        uses: actions/upload-artifact@v4
        with:
          name: generated-logs
          path: generate.txt

  Job-2:
    runs-on: ubuntu-latest
    needs: Job-1
    steps:
      - name: Download Logs
        uses: actions/download-artifact@v4
        with:
          name: generated-logs
          path: download-folder/
          
      - name: Print Logs 
        run:  cat download-folder/generate.txt
```
<img width="1187" height="855" alt="image" src="https://github.com/user-attachments/assets/8129657c-1127-4d5f-98ca-75670b6d5efa" />
<img width="1223" height="691" alt="image" src="https://github.com/user-attachments/assets/4c309b3f-950f-4a5f-8602-26612e2a2718" />

-----

**Task 5: Run Real Tests in CI**

Take any script from your earlier days (Python or Shell) and run it in CI:

1.Add your script to the github-actions-practice repo

2.Write a workflow that:

* Checks out the code
* Installs any dependencies needed
* Runs the script
* Fails the pipeline if the script exits with a non-zero code
  
3.Intentionally break the script — verify the pipeline goes red

4.Fix it — verify it goes green again

```
.github/workflows/ci_test.yml
```
```
name: CI workflow Test

on:
 push: 

jobs:
  test_job:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository code
      uses: actions/checkout@v4

    - name: Setup Python
      uses: actions/setup-python@v5
      with:
         python-version: "3.11"

    - name: Install dependencies
      run: pip install -r requirements.txt

    - name: Make script executable
      run: chmod 777 system_info.sh
        
    - name: Run the script
      run: ./system_info.sh

```

<img width="1071" height="872" alt="image" src="https://github.com/user-attachments/assets/fa516d1f-6383-46b0-af19-a84556a11491" />
<img width="680" height="810" alt="image" src="https://github.com/user-attachments/assets/05048f30-a8af-4d7f-9f6a-95e1eb1e2c05" />

-----

**Task 6: Caching**

1.Add actions/cache to a workflow that installs dependencies

2.Run it twice — observe the time difference

3.Write in your notes: What is being cached and where is it stored?

* Python packages downloaded by pip from requirements.txt. is cached here
  
* it is stored On GitHub Actions servers,restored to the runner at ~/.cache/pip.

<img width="1471" height="395" alt="image" src="https://github.com/user-attachments/assets/9340e62f-a709-42cb-bf12-33ed9369513b" />


----

What I lerned from Secret Management

* Store sensitive data (like API keys, tokens, passwords) in GitHub Actions Secrets, not in code.

* They are encrypted, injected at runtime, and never exposed in logs.

