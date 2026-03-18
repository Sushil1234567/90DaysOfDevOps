**Task 1: Git Reset — Hands-On**

1.Make 3 commits in your practice repo (commit A, B, C)
<img width="702" height="647" alt="Image" src="https://github.com/user-attachments/assets/659328cf-abc8-4eeb-ba7a-4de5de61a39b" />

2.Use git reset --soft to go back one commit — what happens to the changes?

<img width="648" height="167" alt="Image" src="https://github.com/user-attachments/assets/7db41da7-7cc7-427c-88ce-7e3491259958" />

3.Re-commit, then use git reset --mixed to go back one commit — what happens now?
<img width="677" height="212" alt="image" src="https://github.com/user-attachments/assets/9b2a753e-a432-4c56-b9bf-a20f4d7bf2e4" />
<img width="691" height="390" alt="image" src="https://github.com/user-attachments/assets/4de029a6-1bea-4b1d-9697-39932e6bdf60" />

4.Re-commit, then use git reset --hard to go back one commit — what happens this time?
<img width="677" height="485" alt="image" src="https://github.com/user-attachments/assets/af764d25-d24a-482f-84c6-a71cabbacadb" />

5.Answer in your notes:
* What is the difference between --soft, --mixed, and --hard?
  
ans: 

git reset --soft undoes your last commit(s) but keeps all your changes staged and ready to be committed again.
It moves the branch pointer backward, but leaves your working directory and staging area untouched. 

git reset --mixed  is like an "undo" button that undoes a commit and any git add commands,
but keeps the actual file changes in the working directory

git reset --hard permanently deletes all local, uncommitted modifications (both staged and unstaged) and resets your branch's history to match a specified commit.
 
* Which one is destructive and why?
  
ans: git reset --hard is destructive because it permanently deletes all changes and resets branch history .

* When would you use each one?
ans:

--soft : When we want to uncommit changes, but keep all modifications staged, ready for a new commit

--mixed: When we want to uncommit and unstage changes, but keep the files intact in our working directory so we can reorganize what to stage next

--hard: Use this when an experimental feature has gone completely wrong, and you want to completely abandon all local progress and start fresh from a previous commit

* Should you ever use git reset on commits that are already pushed?
  
ans: Yes, we can use git reset on commits that are already pushed, but it is highly discouraged on shared branches because it rewrites the commit history and can cause problems for team members

**Task 2: Git Revert — Hands-On**

1.Make 3 commits (commit X, Y, Z)

<img width="665" height="398" alt="image" src="https://github.com/user-attachments/assets/ddc2ec80-bcaf-40d3-87c8-52667d639ecd" />

2.Revert commit Y (the middle one) — what happens?

<img width="607" height="452" alt="image" src="https://github.com/user-attachments/assets/e8dbc8b0-9819-47ee-bb4f-1ff6ba31d111" />
<img width="716" height="71" alt="image" src="https://github.com/user-attachments/assets/d52d635e-6dc6-4a2b-8381-2aee1f31d984" />

while reverting , this shows a merge conflict and prompts to resolve and commit again. and forms a new commit .

3.Check git log — is commit Y still in the history?

<img width="595" height="218" alt="image" src="https://github.com/user-attachments/assets/62d736a3-7e56-4d11-a66b-e2ba87efe6be" />

yes, commit Y is also shown in history along with the new commit .

4.Answer in your notes:

* How is git revert different from git reset?
  
git revert command creates a new commit that undoes the changes from a previous commit.

git reset undoes changes by moving the current branch's pointer (HEAD) back to an earlier commit in your history. It rewrites the project's history from that point forward.

* Why is revert considered safer than reset for shared branches?
  
git revert is safer than git reset primarily because it preserves the project's history by creating a new "undo" commit, rather than modifying or deleting existing commits.

* When would you use revert vs reset?
  
git reset used for local, unshared changes where you can safely rewrite history.

git revert used for changes that have been pushed to a shared or public branch to maintain history integrity. 


**Task 3: Reset vs Revert — Summary**
|                                    |                        git reset                      |                    git revert                  |
|------------------------------------|-------------------------------------------------------|------------------------------------------------|
| What it does                       |Rewrites history and undoes changes from the specified |Preserves history, adds a new commit that       |
|                                    |commit.                                                |reverses the specified commit’s changes.        |
|Removes commit from history?        |                            yes                        |                        no                      |
|Safe for shared/pushed branches?    |                            no                         |                        yes                     |
|When to use                         |To completely remove commit and its changes.           |To preserve history while safely undoing changes|


**Task 4: Branching Strategies**

Research the following branching strategies and document each in your notes with:

How it works (short description)A simple diagram or flow (text-based is fine) When/where it's used Pros and cons

1.GitFlow — 

* master : Always reflects the production‑ready state.
* develop : Always reflects a state with the latest delivered development changes for the next release.
* release : Created from develop when the desired release state is met and assigned a release number. Minor fixes can be made here. Eventually merged into both master and develop.
* feature : Created from develop for new feature development. Merged back into develop once complete.
* hotfix : Created from master to fix urgent bugs. Changes are merged back into both master and develop.
* Used for a large team with scheduled releases.
* Pros : Everything perfectly tracked.
* Cons : Can be complex and difficult to manage.

2.GitHub Flow — simple, single main branch + feature branches

* main : Production ready state.
* feature branches : Created from main. Develop and test the feature, submit for review, approve, and merge back into main.
* Ideal for continuous deployment/continuous delivery (CD) workflows.
* Pros : Simple, lightweight.
* Cons : Not properly structured. Can become messy if not disciplined, since everything merges directly into main.


3.Trunk-Based Development — everyone commits to main, short-lived branches
* trunk/main : The single branch where all developers commits frequently. Always reflects the latest working state.
* short lived feature branches : Short lived branches created for a change, merged back quickly.
* Ideal for startup.
* Pros : Simple, fast.
* Cons : Risky if anyone pushed unstable code directly to trunk.

4.Answer:

Which strategy would you use for a startup shipping fast?

ans: trunk based

Which strategy would you use for a large team with scheduled releases?

ans : git flow

Which one does your favorite open-source project use? (check any repo on GitHub)

ans: trank based

