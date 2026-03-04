
**Task 2: Hello Workflow**
<img width="882" height="486" alt="image" src="https://github.com/user-attachments/assets/4801f8d3-c9c1-4e86-92fa-70725c666d30" />
<img width="912" height="437" alt="image" src="https://github.com/user-attachments/assets/cbb40cfb-cafa-4c68-8d77-e53a5dd5662a" />
<img width="1857" height="882" alt="image" src="https://github.com/user-attachments/assets/bf4699ef-3977-4044-b3a0-69ba408009e2" />

**Task 3: Understand the Anatomy**
* on: indicates the dependency on prior action of an event  ( ex: on: push ) 
* jobs: indicates the tasks to be done ( ex: build job, test job, execute job )
* runs-on: indicates the environment/platform/server/stage where the script must get executed ( ubuntu, windows , CentOS )
* steps: indicates the serial processes of a job lined to complete one after another ( steps under a job ) 
* uses: this checks out the source code repository into the runner's virtual machine
* run: used print under echo " "
* name: (on a step) : unique id used as a reference for a step

**Task 4: Add More Steps**

Update hello.yml to also:

* Print the current date and time
* Print the name of the branch that triggered the run (hint: GitHub provides this as a variable)
* List the files in the repo
* Print the runner's operating system

<img width="788" height="500" alt="image" src="https://github.com/user-attachments/assets/ac139ad5-6e3d-404a-8009-20a5c94ae823" />

<img width="945" height="765" alt="image" src="https://github.com/user-attachments/assets/70438236-6878-4e1e-bae5-6b3cf55d3a91" />


**Task 5: Break It On Purpose**
Add a step that runs a command that will fail (e.g., exit 1 or a misspelled command)
Push and observe what happens in the Actions tab
Fix it and push again
Write in your notes: What does a failed pipeline look like? How do you read the error?

<img width="1067" height="576" alt="image" src="https://github.com/user-attachments/assets/9c85f03c-993a-4ca8-a868-444ff8a776e2" />

- i was unable to figure out the purpose of 'uses' key in the yaml . i learned and fixed there.

