**Task 1: Understand workflow_call**

Before writing any code, research and answer in your notes:

What is a reusable workflow?

* A reusable workflow in GitHub Actions is a central workflow template that multiple pipelines can call instead of duplicating the same CI/CD logic everywhere
  
What is the workflow_call trigger?

* workflow_call is the action of being called from another worflow for a particular cation to be invoked.
  
How is calling a reusable workflow different from using a regular action (uses:)?

# regular uses:
* used INSIDE steps
* reuses/calls small action/step
* Performs one task
* Can Be Public Marketplace Components from GitHub Marketplace.
  
     ex- uses: actions/checkout@v4
  
* Behaves as a helper function
  
* Actions Inputs:
           uses: actions/setup-node@v4
  
           with:
           node-version: 20
  

# worflow-call uses:
* Used directly under jobs
* resuses/calls an ENTIRE workflow pipeline
* Runs multiple jobs/steps
* Are Usually Internal Pipelines used for organization-wide standards.
  
  ex- uses: my-company/platform/.github/workflows/security-scan.yml@main
  
* Behaves as a full pipeline template
  
* Workflow Inputs:
  
       jobs:
  
          deploy:
  
             uses: org/repo/.github/workflows/deploy.yml@main
  
             with:
  
               environment: production

Where must a reusable workflow file live?

A reusable workflow file must always be stored inside:
 
     .github/workflows/

because GitHub Actions only detects reusable workflows from that directory.

------------

**Task 2: Create Your First Reusable Workflow**

Create `.github/workflows/reusable-build.yml`:
1. Set the trigger to `workflow_call`
2. Add an `inputs:` section with:
   - `app_name` (string, required)
   - `environment` (string, required, default: `staging`)
3. Add a `secrets:` section with:
   - `docker_token` (required)
4. Create a job that:
   - Checks out the code
   - Prints `Building <app_name> for <environment>`
   - Prints `Docker token is set: true` (never print the actual secret)

**Verify:** This file alone won't run — it needs a caller. That's next.

```
.github/workflows/reusable-build.yml
```
```
name: ReusableBuild
on: 
  workflow_call: 
    inputs:
      app_name: 
        required: true
        type: string
        
      environment: 
        required: true
        type: string
        default: staging

    secrets: 
      docker-token: 
        required: true

jobs:
  ReusableJob:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
        
      - name: Print 
        run: |
          echo " Building $GITHUB_REPOSITORY for $ENV_NAME "
          echo " Docker token is set : true "

```

-------

**Task 3: Create a Caller Workflow**

Create .github/workflows/call-build.yml:

1. Trigger on push to main

2. Add a job that uses your reusable workflow

3. Push to main and watch it run



```
.github/workflows/call-build.yml
```
```
name: Call Workflow
on: 
 push: 
   branches: [main]

jobs:
 build:
  uses: ./.github/workflows/reusable-build.yml
  
  with:
    app_name : "my-web-app" 
    environment: "production"

  secrets: 
      docker-token: ${{ secrets.DOCKER_TOKEN }}  
```

Verify: In the Actions tab, do you see the caller triggering the reusable workflow? Click into the job — can you see the inputs printed?

* yes, the caller triggers the reusable worflow .

<img width="1202" height="873" alt="image" src="https://github.com/user-attachments/assets/2dc274e7-c327-423e-b9ac-e8f68bf6c8c2" />

--------

**Task 4: Add Outputs to the Reusable Workflow**

Extend reusable-build.yml:

Add an outputs: section that exposes a build_version value

Inside the job, generate a version string (e.g., v1.0-<short-sha>) and set it as output

In your caller workflow, add a second job that:

Depends on the build job (needs:)

Reads and prints the build_version output

Verify: Does the second job print the version from the reusable workflow?



```
.github/workflows/reusable-build.yml
```
```
name: ReusableBuild
on: 
  workflow_call: 
    inputs:
      app_name: 
        required: true
        type: string
        
      environment: 
        required: true
        type: string
        default: staging

    secrets: 
      docker-token: 
        required: true
    
    outputs: 
      build_version: 
        value : ${{ jobs.ReusableJob.outputs.build_version }}    

jobs:
  ReusableJob:    
    runs-on: ubuntu-latest
    
    outputs:
      build_version: ${{ steps.version.outputs.Version }}
      
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print 
        run: |
          echo " Building $GITHUB_REPOSITORY for ${{ inputs.environment }} "
          echo " Docker token is set : true "

      - name: Generate & set Version
        id:   version
        run:  | 
          SHORT_SHA=${GITHUB_SHA:0:5}
          VERSION="v$SHORT_SHA" 
          echo "Version=$VERSION" >> $GITHUB_OUTPUT
```

```
.github/workflows/call-build.yml
```
```
name: Call Workflow
on: 
 push: 
   branches: [main]

jobs:
 build:
  uses: ./.github/workflows/reusable-build.yml
  
  with:
    app_name : "my-web-app" 
    environment: "production"

  secrets: 
      docker-token: ${{ secrets.DOCKER_TOKEN }}  

 second_job: 
   runs-on: ubuntu-latest   
   needs:   build
   steps:
     - name: Print Build Version
       run:  | 
        echo "Version: ${{ needs.build.outputs.build_version }}"
```

<img width="827" height="296" alt="image" src="https://github.com/user-attachments/assets/b7180d06-f318-4b94-b6a8-7bddb8827f3b" />
<img width="737" height="368" alt="image" src="https://github.com/user-attachments/assets/2eba7722-79c4-445d-bec2-e95ff1b84e43" />

Verify: Does the second job print the version from the reusable workflow?
 * yes , the seconf job prints the version worflow

-----------

**Task 5: Create a Composite Action**

Create a custom composite action in your repo at .github/actions/setup-and-greet/action.yml:

Define inputs: name and language (default: en)

Add steps that:

Print a greeting in the specified language

Print the current date and runner OS

Set an output called greeted with value true

Use the composite action in a new workflow with uses: ./.github/actions/setup-and-greet

```
.github/actions/setup-and-greet/action.yml
```
```
name: Composite Action
description: "greets user"

inputs:
 name: 
   description: "persons name"
   required: true
   
 language:
  description: "greeting language"
  default: english
  required: false

outputs:
 greeted: 
  description: "Prints greet message"
  value: ${{ steps.greet.outputs.greeted }} 
  
runs:
  using: "composite"
  steps:
   - name: Greet
     id:   greet
     shell: bash
     run: |
       if [ "${{ inputs.language }}" = "english" ]; then
        echo "Hello ${{ inputs.name }}"
     
       elif [ "${{ inputs.language }}" = "hindi" ]; then
        echo "Namastey ${{ inputs.name }}"

       else 
        echo "wrong input"
       fi

       echo "CURRENT_OS: ${{ runner.os }} & CURRENT_DATE: $(date +%d-%m-%y)"
       echo "greeted=true" >> $GITHUB_OUTPUT  
```

```
.github/workflows/actionworkflow.yml
```
```
name: Action Workflow
on:
 push:
   branches: [ main ]

jobs:
  Call-CompositeAction:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v4
        
      - name: Calls Greet
        id: greet
        uses: ./.github/actions/setup-and-greet/
        with:
          name: ${{ github.actor }}
          language: hindi

      - name: Prints the message
        run: |
          echo "Greeted: ${{ steps.greet.outputs.greeted }}"
```

<img width="1032" height="792" alt="image" src="https://github.com/user-attachments/assets/34832b98-3dda-4bba-962f-a18996ec541c" />

Verify: Does your custom action run and print the greeting?
* yes it prints the greeting
----------------------------------

### Task 6: Reusable Workflow vs Composite Action
Fill this in your notes:

| | Reusable Workflow | Composite Action |
|---|---|---|
| Triggered by | `workflow_call` | `uses:` in a step |
| Can contain jobs? | yes(multiple)  | no ((only a list of steps) |
| Can contain multiple steps? | yes | yes |
| Lives where? | .github/workflows/file.yml | .github/actions/setup-and-greet/action.yml |
| Can accept secrets directly? | yes | no(must pass them as standard inputs) |
| Best for | standardizing processes, Standardizing large pipelines across repos | Step-Level Code Sharing, Packaging small, step-level tasks |
