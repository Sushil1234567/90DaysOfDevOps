**Task 1: Understanding Branches**

1.What is a branch in Git?

ans: A Git branch is a movable pointer to a specific commit, which creates a separate, independent line of development within a project.
It allows developers to make changes, add features, or fix bugs in an isolated environment without affecting the main codebase.
     
2.Why do we use branches instead of committing everything to main?

ans: Branches are created because it isolates new work from the stable, production-ready code. Branching enables parallel development, 
allowing multiple developers to work on features or fixes simultaneously without interfering with each other

3.What is HEAD in Git?

ans: HEAD is a pointer or symbolic reference to the commit you are currently working on.

4.What happens to your files when you switch branches?

ans: On switching branches, git updates your working directory to match the commit of the new branch, changing, 
adding, or deleting files to reflect that specific version.

**Task 2: Branching Commands — Hands-On**

In your devops-git-practice repo, perform the following:

1.List all branches in your repo

2.Create a new branch called feature-1

3.Switch to feature-1

4.Create a new branch and switch to it in a single command — call it feature-2

5.Try using git switch to move between branches — how is it different from git checkout?

6.Make a commit on feature-1 that does not exist on main

7.Switch back to main — verify that the commit from feature-1 is not there

8.Delete a branch you no longer need

9.Add all branching commands to your git-commands.md

<img width="916" height="957" alt="image" src="https://github.com/user-attachments/assets/0aee597e-4a5f-43cf-86fe-d9b394d94d8b" />

<img width="760" height="810" alt="image" src="https://github.com/user-attachments/assets/1b3586a7-0ce9-4e69-863e-7c6b7c89fbaf" />

<img width="1890" height="322" alt="image" src="https://github.com/user-attachments/assets/0655e0f0-bad9-44f0-a844-e7fae24cae61" />

**Task 3: Push to GitHub**

1.Create a new repository on GitHub (do NOT initialize it with a README)

2.Connect your local devops-git-practice repo to the GitHub remote

3.Push your main branch to GitHub

4.Push feature-1 branch to GitHub

5.Verify both branches are visible on GitHub

6.Answer in your notes: What is the difference between origin and upstream?

ans: Git origin is the default name for the primary remote repository we work with, while upstream is a conventional name 
for the original repository in a forked workflow, typically used for pulling in updates.
<img width="1045" height="176" alt="image" src="https://github.com/user-attachments/assets/ad0396f5-3c6c-456d-bfab-ecfdcd1f333a" />

<img width="955" height="686" alt="image" src="https://github.com/user-attachments/assets/77897c91-11a6-4aac-b8e7-cd9e94fff78e" />

<img width="1050" height="640" alt="image" src="https://github.com/user-attachments/assets/2520ee1c-618e-4f9e-91ef-d8ceb8cc1bb0" />

<img width="716" height="320" alt="image" src="https://github.com/user-attachments/assets/67d65bbc-f7f1-4d00-94c0-e16c9ffb30e0" />

<img width="1905" height="877" alt="image" src="https://github.com/user-attachments/assets/ee6bb8bc-8245-4c5f-af8d-afd05edcd09c" />

**Task 4: Pull from GitHub**

1.Make a change to a file directly on GitHub (use the GitHub editor)

2.Pull that change to your local repo

3.Answer in your notes: What is the difference between git fetch and git pull?

ans: The core difference is that git fetch downloads remote changes without modifying our local working files, 
while git pull downloads and automatically integrates (rebases) those changes into our current branch
<img width="786" height="838" alt="image" src="https://github.com/user-attachments/assets/eb82d9f8-9ae8-4de2-82b8-100803de10f2" />

<img width="652" height="227" alt="image" src="https://github.com/user-attachments/assets/8b559595-53f3-4dde-b77f-89610ff2a7c3" />

<img width="1902" height="642" alt="image" src="https://github.com/user-attachments/assets/260b76b0-e0df-4265-b81a-631d0d68b603" />

**Task 5: Clone vs Fork**

1.Clone any public repository from GitHub to your local machine

2.Fork the same repository on GitHub, then clone your fork

3.Answer in your notes:

* What is the difference between clone and fork?
  
ans: Clone: Taking the copy of the whole repo from remote to our local when it doesnot exist in our local previously.

Fork: Taking the copy of a repo to our github account and continue working (without taking it down till local ) .
  
* When would you clone vs fork?
  
ans: Cloning is done to make changes in the copied repo ( write access ) and then allows to push and merge with the main repo ,
forking is done only incase we need to make any open source contribution to a speific project without directly allowing us to make
changes on the main repo.

* After forking, how do you keep your fork in sync with the original repo?
  
ans: To keep in sync with the origibal repo , simply sync the fork and upgrade the branch -option present on the Github UI   
<img width="945" height="217" alt="image" src="https://github.com/user-attachments/assets/7f042c12-6b79-4935-840f-ede57d9aa10f" />

