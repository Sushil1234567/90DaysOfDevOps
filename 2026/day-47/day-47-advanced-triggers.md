### Task 1: Pull Request Event Types
Create `.github/workflows/pr-lifecycle.yml` that triggers on `pull_request` with **specific activity types**:
1. Trigger on: `opened`, `synchronize`, `reopened`, `closed`
2. Add steps that:
   - Print which event type fired: `${{ github.event.action }}`
   - Print the PR title: `${{ github.event.pull_request.title }}`
   - Print the PR author: `${{ github.event.pull_request.user.login }}`
   - Print the source branch and target branch
3. Add a conditional step that only runs when the PR is **merged** (closed + merged = true)

Test it: create a PR, push an update to it, then merge it. Watch the workflow fire each time with a different event type.

## Trigger: opened

```
.github/workflows/pr-lifecycle.yml
```
```
name: PR Events
on:
 pull_request: 
   types: [opened]
   branches: [main]


jobs:
  Event-Details:
    runs-on: ubuntu-latest
    steps:
      - name: Print Event Type
        run:  echo "Event type:- ${{ github.event.action }}"

      - name: Print PR title
        run:  echo "PR title:- ${{ github.event.pull_request.title }}"

      - name: Print Source Branch
        run:  echo "Source branch:- ${{ github.head_ref }}"

      - name: Print Target Branch
        run:  echo "Target branch:- ${{ github.base_ref }}"

      - name: Print PR Merge Status
        if:   github.event.pull_request.merged == true
        run:  echo "Merge Complete"
```
<img width="1867" height="866" alt="image" src="https://github.com/user-attachments/assets/5d788936-8ab8-4850-a70e-9d43e03c2ce5" />

## Trigger: synchronize
```
.github/workflows/pr-lifecycle.yml
```
```
name: PR Events
on:
 pull_request: 
   types: [synchronize]
   branches: [main]


jobs:
  Event-Details:
    runs-on: ubuntu-latest
    steps:
      - name: Print Event Type
        run:  echo "Event type:- ${{ github.event.action }}"

      - name: Print PR title
        run:  echo "PR title:- ${{ github.event.pull_request.title }}"

      - name: Print Source Branch
        run:  echo "Source branch:- ${{ github.head_ref }}"

      - name: Print Target Branch
        run:  echo "Target branch:- ${{ github.base_ref }}"

      - name: Print PR Merge Status
        if:   github.event.pull_request.merged == true
        run:  echo "Merge Complete"
```
<img width="1860" height="865" alt="image" src="https://github.com/user-attachments/assets/9c583ed4-da52-409f-a97f-f9aaed7f557a" />

## Trigger: reopened
```
.github/workflows/pr-lifecycle.yml
```
```
name: PR Events
on:
 pull_request: 
   types: [reopened]
   branches: [main]


jobs:
  Event-Details:
    runs-on: ubuntu-latest
    steps:
      - name: Print Event Type
        run:  echo "Event type:- ${{ github.event.action }}"

      - name: Print PR title
        run:  echo "PR title:- ${{ github.event.pull_request.title }}"

      - name: Print Source Branch
        run:  echo "Source branch:- ${{ github.head_ref }}"

      - name: Print Target Branch
        run:  echo "Target branch:- ${{ github.base_ref }}"

      - name: Print PR Merge Status
        if:   github.event.pull_request.merged == true
        run:  echo "Merge Complete"
```
<img width="1872" height="856" alt="image" src="https://github.com/user-attachments/assets/07607bc8-130a-4dca-b5b7-a6072bf14bb9" />

## Trigger: closed
```
.github/workflows/pr-lifecycle.yml
```
```
name: PR Events
on:
 pull_request: 
   types: [closed]
   branches: [main]


jobs:
  Event-Details:
    runs-on: ubuntu-latest
    steps:
      - name: Print Event Type
        run:  echo "Event type:- ${{ github.event.action }}"

      - name: Print PR title
        run:  echo "PR title:- ${{ github.event.pull_request.title }}"

      - name: Print Source Branch
        run:  echo "Source branch:- ${{ github.head_ref }}"

      - name: Print Target Branch
        run:  echo "Target branch:- ${{ github.base_ref }}"

      - name: Print PR Merge Status
        if:   github.event.pull_request.merged == true
        run:  echo "Merge Complete"
```
<img width="1852" height="862" alt="image" src="https://github.com/user-attachments/assets/13120339-4073-4c22-9631-28c3f88c245f" />

**Note:** The 'Merge Complete' step only ran when the PR was merged and closed, unlike the previous scenarios (opened/synchronized/reopened) 
          where the task was finished asper the event type and wrapped off . i.e the last step was dependent on the event type which only ran 
          after PR is merged+closed= true
          
-----
### Task 2: PR Validation Workflow
Create `.github/workflows/pr-checks.yml` — a real-world PR gate:
1. Trigger on `pull_request` to `main`
2. Add a job `file-size-check` that:
   - Checks out the code
   - Fails if any file in the PR is larger than 1 MB
3. Add a job `branch-name-check` that:
   - Reads the branch name from `${{ github.head_ref }}`
   - Fails if it doesn't follow the pattern `feature/*`, `fix/*`, or `docs/*`
4. Add a job `pr-body-check` that:
   - Reads the PR body: `${{ github.event.pull_request.body }}`
   - Warns (but doesn't fail) if the PR description is empty

**Verify:** Open a PR from a badly named branch — does the check fail?
* Yes, the check fails when it doesnt have the pattern: `feature/*`, `fix/*`, or `docs/*`

```
.github/workflows/pr-checks.yml
```
```
name: PR Validation
on:
 pull_request: 
  branches: [main]

jobs: 
  file-size-check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Checks if sny file greater than 1MB
        run: |
         Limit=1048576
         for i in $( git diff --name-only origin/main...HEAD )
         do
           Size=$( stat -c %s "$i" )
           if [ "$Size" -gt "$Limit" ];then
               echo "File size: $Size"
               echo "File is larger"
               exit 1
           fi
         done  
         
  branch-name-check:
    runs-on: ubuntu-latest
    steps:
      - name: Read the branch name
        run:  echo "Branch:- ${{ github.head_ref }}"

      - name: Validate file
        run:  |
         for i in $GITHUB_HEAD_REF;do
           if [[ "$i" != feature/* && "$i" != fix/* && "$i" != docs/* ]];then
               echo "Invalid pattern: $i"
               exit 1
           fi
         done

  pr-body-check:
    runs-on: ubuntu-latest
    steps:
      - name: Reads the PR body
        run:  echo "${{ github.event.pull_request.body }}"

      - name: Check PR body
        if:   ${{ github.event.pull_request.body == '' }}
        run:  echo "PR body is empty"
```
<img width="1871" height="787" alt="image" src="https://github.com/user-attachments/assets/c7258def-34e4-479c-b9f1-f70fc4fac0ba" />
<img width="1870" height="807" alt="image" src="https://github.com/user-attachments/assets/254a5fc7-5e70-4e0b-ac5a-3146484f1013" />

-----

### Task 3: Scheduled Workflows (Cron Deep Dive)
Create `.github/workflows/scheduled-tasks.yml`:
1. Add a `schedule` trigger with cron: `'30 2 * * 1'` (every Monday at 2:30 AM UTC)
2. Add **another** cron entry: `'0 */6 * * *'` (every 6 hours)
3. In the job, print which schedule triggered using `${{ github.event.schedule }}`
4. Add a step that acts as a **health check** — curl a URL and check the response code

Write in your notes:
- The cron expression for: every weekday at 9 AM IST
  * 0 9 * * 0-5
  
  i.e:
  0 minutes
  9 hours
  0-5 days (mon-fri)
    
- The cron expression for: first day of every month at midnight
  * 0 0 1 * *

  i.e:
  0 minutes
  0 hours
  day 1 
    
- Why GitHub says scheduled workflows may be delayed or skipped on inactive repos
  * GitHub states that scheduled workflows may be delayed, skipped, or entirely paused
    on inactive repositories primarily as a resource management and cost-saving measure.

**Important:** Also add `workflow_dispatch` so you can test it manually without waiting for the schedule.

```
.github/workflows/scheduled-tasks.yml
```
```
name: Scheduled Workflow
on:
 schedule:
   - cron: 30 2 * * 1
   - cron: 0 */6 * * *
   
 workflow_dispatch:
   

jobs:
  Health-Check:
    runs-on: ubuntu-latest 
    steps:
      - name: Check Health
        uses: jtalk/url-health-check-action@v5
        with:
          url: https://crontab.guru/
          max-attempts: 5
          retry-delays: 3s
```

<img width="1128" height="577" alt="image" src="https://github.com/user-attachments/assets/7a453b1f-aecd-4eb0-a3ce-aa3c8c8acd24" />

-----

### Task 4: Path & Branch Filters
Create `.github/workflows/smart-triggers.yml`:
1. Trigger on push but **only** when files in `src/` or `app/` change:
   ```yaml
   on:
     push:
       paths:
         - 'src/**'
         - 'app/**'
   ```
2. Add `paths-ignore` in a second workflow that skips runs when only docs change:
   ```yaml
   paths-ignore:
     - '*.md'
     - 'docs/**'
   ```
3. Add branch filters to only trigger on `main` and `release/*` branches
4. Test it: push a change to a `.md` file — does the workflow skip?

```
.github/workflows/smart-triggers.yml
```
```
name: Smart Triggers
on:
 push:
  paths:
   - 'src/**'
   - 'app/**'
  branches: [main]

jobs:
   detect-changes:
      runs-on: ubuntu-latest
      steps:
         - uses: actions/checkout@v4
           with: 
            fetch-depth: 0

         - name: Print Changed Directories
           run: |
            #changedfiles=$(git diff --name-only HEAD~1 HEAD)
                                 #OR 
            changedfiles=$(git diff --name-only ${{ github.event.before }} ${{ github.sha }})

            for i in $changedfiles
            do
             if [[ "$i" == src/* ]];then
              echo "Directory: src"
             elif [[ "$i" == app/* ]];then
              echo "Directory: app"
             fi
            done 

#   OR  

#name: Smart Triggers
#on:
# push:
#  paths:
#   - 'src/**'
#   - 'app/**'

#jobs:
#   detect-changes:
#      runs-on: ubuntu-latest
#      steps:
#         - uses: actions/checkout@v4
         
#         - name: Get Changed files
#           id:   changed-files
#           uses: tj-actions/changed-files@v6

#         - name: Print Directories
#           run: | 
#             for i in ${{ steps.changed-files.outputs.all_changed_files }}
#             do 
#              if [[ "$i" == src/* ]];then
#               echo "Directory: src"
#              elif [[ "$i" == app/* ]];then
#               echo "Directory: app"
#              fi 
#             done
```
<img width="1887" height="862" alt="image" src="https://github.com/user-attachments/assets/0e69abeb-6e56-4f7b-b49c-d9e10aa4d779" />

```
.github/workflows/path-ignore.yml
```
```
name: Path Ignore
on:
 push:
   paths-ignore:
     - '*.md' 
     - 'docs/**'
   branches: [main] 

jobs:
  Message:
    runs-on: ubuntu-latest
    steps:
      - name: Prints the message
        run:  echo "Not pushed to md or docs"
```
<img width="1892" height="862" alt="image" src="https://github.com/user-attachments/assets/2874451c-52ba-4652-ba4b-f81ad38824e0" />

Write in your notes: When would you use `paths` vs `paths-ignore`?
* paths: is used to trigger a workflow only when files in specific paths are modified.
* paths-ignore: is used to prevent a workflow from running when all modified files are in specified paths that should be ignored, such as documentation or markdown files.

-----------------------
### Task 5: `workflow_run` — Chain Workflows Together
Create two workflows:
1. `.github/workflows/tests.yml` — runs tests on every push
2. `.github/workflows/deploy-after-tests.yml` — triggers **only after** `tests.yml` completes successfully:
   ```yaml
   on:
     workflow_run:
       workflows: ["Run Tests"]
       types: [completed]
   ```
3. In the deploy workflow, add a conditional:
   - Only proceed if the triggering workflow **succeeded** (`${{ github.event.workflow_run.conclusion == 'success' }}`)
   - Print a warning and exit if it failed
```
.github/workflows/tests.yml
```
```
name: Run Tests
on:
 push:
   branches: [main]

jobs:
  Tests:
   runs-on: ubuntu-latest
   steps:
     - name: Print Message
       run:  echo "Test Run Success !(before deploy)"
```
```
.github/workflows/deploy-after-tests.yml
```
```
name: Deploy aftertest
on:
 workflow_run: 
  workflows: ["Run Tests"]
  types: [completed]

jobs:
  Deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Message on completion
        if:   ${{ github.event.workflow_run.conclusion == 'success' }}
        run:  echo "Deploy Success !"

      - name: Message on failure
        if:   ${{ github.event.workflow_run.conclusion != 'success' }}
        run:  echo "::Warning::Failed & skipped !"
              exit 1


#OR
#jobs:
#  deploy:
#    if: ${{ github.event.workflow_run.conclusion == 'success' }}
#    runs-on: ubuntu-latest

#    steps:
#      - run: echo "Deploying application..."

#  warning:
#    if: ${{ github.event.workflow_run.conclusion != 'success' }}
#    runs-on: ubuntu-latest

#    steps:
#      - run: |
#          echo "::warning::Tests failed. Deployment skipped."
#          exit 1
             
```
<img width="1888" height="741" alt="image" src="https://github.com/user-attachments/assets/afd88ea2-eac5-4aab-b849-7fa2c7da2ac3" />

**Verify:** Push a commit — does the test workflow run first, then trigger the deploy workflow?
* Yes, the deploy workflow runs only after the test workflow .
-----

### Task 6: `repository_dispatch` — External Event Triggers
1. Create `.github/workflows/external-trigger.yml` with trigger `repository_dispatch`
2. Set it to respond to event type: `deploy-request`
3. Print the client payload: `${{ github.event.client_payload.environment }}`
4. Trigger it using `curl` or `gh`:
   ```bash
   gh api repos/<owner>/<repo>/dispatches \
     -f event_type=deploy-request \
     -f client_payload='{"environment":"production"}'
   ```
```
.github/workflows/external-trigger.yml
```
```
name: ExternalTrigger
on: 
  repository_dispatch: 
   types: [deploy-request]

jobs:
  PrintPayload:
   runs-on: ubuntu-latest
   steps: 
     - name: Print the client payload
       run: echo "${{ github.event.client_payload.environment }}"
```
<img width="1885" height="1017" alt="image" src="https://github.com/user-attachments/assets/2ed7c67b-a8c6-41cd-a7b8-c53676fd99a5" />


- Write in your notes: When would an external system (like a Slack bot or monitoring tool) trigger a pipeline?
  
 when we curl or gh the payload to the github repository , this triggers the repository_dispatch event hence the pipeline is tiggered via esternal trigger

***Explanation of workflow_run vs workflow_call in your own words***

* ***workflow_run*** is an internal trigger, not an external one.
  It occurs automatically when one GitHub Actions workflow completes and requests another workflow in the same repository to run.
  
* ***workflow_call*** event is also an internal trigger, It is used to create Reusable Workflows, allowing one workflow to directly call another, similar to calling a function in programming.

* How workflow_call Works:
  
  The Caller: A standard workflow in the repository reaches out to a central, reusable workflow file.
  
  The Receiver: The reusable workflow template must have on: workflow_call at the top to accept the invocation.
  
  The Execution: The called workflow runs inline as a job inside the caller workflow, sharing the same execution context.


### workflow_call  vs  workflow_run  vs  repository_dispatch
 
| Event Type | Trigger Source | Primary Use Case |
|---|---|---|
| workflow_run | Internal (Event-driven) | Chaining separate pipelines sequentially (e.g., Run B after A finishes). |
| workflow_call | Internal (Direct invocation) | Reusing central YAML templates across multiple pipelines to avoid duplication. |
| repository_dispatch | External (curl, Slack, API) | Triggering a pipeline from outside GitHub.  |

