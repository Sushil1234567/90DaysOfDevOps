**Task 1: Install and Configure Git**

Ready with the git setup!

**Task 2: Create Your Git Project**

1.Create a new folder called devops-git-practice

2.Initialize it as a Git repository

3.Check the status — read and understand what Git is telling you

4.Explore the hidden .git/ directory — look at what's inside

<img width="738" height="472" alt="image" src="https://github.com/user-attachments/assets/defbd9df-420c-418c-ba88-b90b8dcc8a4d" />

git status : shows the current branch name and  the information regarding the status of any file created i.e untracked, modified, or pending commit .

             Since , there is no files created yet, hence showing the present branch and no commits.

.git/ : this is a hidden folder tagged with a git repository , which is the core of any git repository this holds the data neccesary for version control


**Task 3: Create Your Git Commands Reference**

1.Create a file called git-commands.md inside the repo

2.Add the Git commands you've used so far, organized by category:

* Setup & Config
* Basic Workflow
* Viewing Changes
  
3.For each command, write:

* What it does (1 line)
* An example of how to use it

created: git-commands.md

**Task 4: Stage and Commit**

1.Stage your file

2.Check what's staged

3.Commit with a meaningful message

4.View your commit history

<img width="836" height="590" alt="image" src="https://github.com/user-attachments/assets/392d2ecf-38b2-4a84-bbd8-a1066ade33b4" />


**Task 5: Make More Changes and Build History**

1.Edit git-commands.md — add more commands as you discover them

2.Check what changed since your last commit

3.Stage and commit again with a different, descriptive message

4.Repeat this process at least 3 times so you have multiple commits in your history

5.View the full history in a compact format

<img width="855" height="502" alt="image" src="https://github.com/user-attachments/assets/c4890902-f236-4ac9-8a59-abcf55788d84" />

**Task 6: Understand the Git Workflow**

Answer these questions in your own words (add them to a day-22-notes.md file):

1.What is the difference between git add and git commit?

ans: 'git add' moves the changes from unstaged area (working directory-where we edit files) into the staging area. and 
      
     'git commit' takes everything from the staging area to the local git repository with a commit id as a permanent lock.

2.Whatdoes the staging area do? Why doesn't Git just commit directly?

ans: Staging area acts as an intermidiate between unstaged and the final commit . This is the place where any changes are first 'recognised' by the system

     and then verified and moved to commit. The commit process divides the process into two phases i.e stage and commit , 
     
     this is to give the users control over tracking the precise
     
     changes saved in the project
     
3.What information does git log show you?
ans: git log displays the commit history of the changes to the repositoy along with the commit id and commit message in descending order

     (reversed chronological order) i.e the latest commit on the top and first commit in the bottom
     
4.What is the .git/ folder and what happens if you delete it?

ans: Deleting the .git/ folder will result in removing all the version control data and config files from the local project, and the project will 

     no longer be able to track by git.
     
5.What is the difference between a working directory, staging area, and repository?

ans: working directory: the unstaged / untracked state where changes are made but not yet recognised(staged) by the git VC system.

     Staged area is where the changes are brought into notice by the system (staged) by doing :git add filename
     
     Repository is the final destination of all the changes that were made in the unstaged -> staged -> commit .
