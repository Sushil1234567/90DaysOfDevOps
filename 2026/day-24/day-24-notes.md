**Task 1: Git Merge — Hands-On**

1.Create a new branch feature-login from main, add a couple of commits to it

2.Switch back to main and merge feature-login into main

3.Observe the merge — did Git do a fast-forward merge or a merge commit?

4.Now create another branch feature-signup, add commits to it — but also add a commit to main before merging

5.Merge feature-signup into main — what happens this time?

<img width="810" height="1002" alt="Image" src="https://github.com/user-attachments/assets/74e2e451-0cef-4361-8045-dfaecf8f0c11" />
<img width="640" height="726" alt="Image" src="https://github.com/user-attachments/assets/4c64bd4f-8df5-40c2-a07b-fa9ca88fd31a" />

6.Answer in your notes:
* What is a fast-forward merge?
  
ans: Fast forward merge is a type of merge that happens when the branch being merged has no additional commits compared to the branch we are merging to.
Git simply moves the pointer of the target branch forward to the latest commit of the source branch avoiding the need to create a merge conflict.

* When does Git create a merge commit instead?
  
ans: Merge commits occur when two branches have different histories i.e each branch has new commit histories that is not present in the other.

* What is a merge conflict? (try creating one intentionally by editing the same line in both branches)

ans: Merge conflict occurs when two different branches modify the same lines in the same file, and Git cannot automatically decide which changes to keep.
Therefore the user is propted to decide and make the decision

**Task 2: Git Rebase — Hands-On**

1.Create a branch feature-dashboard from main, add 2-3 commits

2.While on main, add a new commit (so main moves ahead)

3.Switch to feature-dashboard and rebase it onto main

4.Observe your git log --oneline --graph --all — how does the history look compared to a merge?


<img width="681" height="546" alt="Image" src="https://github.com/user-attachments/assets/8b447b32-6caf-4890-aab7-f8431c92de92" />
<img width="836" height="895" alt="Image" src="https://github.com/user-attachments/assets/caf33f4e-558d-447c-9fb4-ef22e745bf97" />

5.Answer in your notes:
* What does rebase actually do to your commits?

ans:Git rebase is way of rewriting our branch's commit history from our current branch onto the tip of another branch in a sequence.
Rebase takes all the local commits off the branch and pulls in all of the upstreqms changes, then reapplies our commits one by one.

* How is the history different from a merge?
 
ans:Merge preserves the full, nonlinear history with a new merge commit.
Rebase rewrites history to create a linear timeline by reapplying commits.

* Why should you never rebase commits that have been pushed and shared with others?
  
ans:Reabse rewrites the commit history ,when we rebase, it destroys existing commits and replace them with new ones that have different SHA hashes, 
which can cause significant problems, and lost work.

* When would you use rebase vs merge?
  
ans: Git rebase is used to maintain a clean, linear history by moving our feature branch to the tip of the main branch, ideal for local work.
Git merge used to preserve the full history of branches, which is safer for shared public branches .

**Task 3: Squash Commit vs Merge Commit**

1.Create a branch feature-profile, add 4-5 small commits (typo fix, formatting, etc.)

2.Merge it into main using --squash — what happens?

3.Check git log — how many commits were added to main?

4.Now create another branch feature-settings, add a few commits

5.Merge it into main without --squash (regular merge) — compare the history

<img width="648" height="135" alt="Image" src="https://github.com/user-attachments/assets/4f85787d-7103-4af5-9785-adf90a580015" />
<img width="793" height="926" alt="Image" src="https://github.com/user-attachments/assets/31ec5d39-c6fb-4d76-807d-b794131aad60" />
<img width="795" height="982" alt="Image" src="https://github.com/user-attachments/assets/f8a17ca7-b82f-4a21-af85-c8c55c54b89a" />

6.Answer in your notes:
* What does squash merging do?
  
ans: A squash merge is a Git workflow that combines all commits from a feature branch into a single, new commit on the target branch.

* When would you use squash merge vs regular merge?
  
ans: Squash merge is used to combine all feature branch commits into a single main branch, ideal for small task-based branches.
Regular merge should be used to preserve the full, detailed history of all commits, incase of shared public branches.

* What is the trade-off of squashing?
  
ans: Trade-off sqaushing is detailed commit history is lost from feature branch as only one clean and simplified commit will be shown in main branch.

**Task 4: Git Stash — Hands-On**

1.Start making changes to a file but do not commit

2.Now imagine you need to urgently switch to another branch — try switching. What happens?

3.Use git stash to save your work-in-progress

4.Switch to another branch, do some work, switch back

5.Apply your stashed changes using git stash pop

6.Try stashing multiple times and list all stashes

7.Try applying a specific stash from the list
<img width="1200" height="998" alt="Image" src="https://github.com/user-attachments/assets/e42b8e0e-3d1f-4220-8e72-352c8bbf2e9e" />
<img width="650" height="177" alt="Image" src="https://github.com/user-attachments/assets/8eb5ce6c-c361-41ef-9451-c4308352e328" />

8.Answer in your notes:

* What is the difference between git stash pop and git stash apply?
ans: Git stash pop pulls out a particular stash out of many stashes.
And git stash apply restores previously stashed changes to our current working directory and staging area.

* When would you use stash in a real-world workflow?
  
ans:When there is an urgency to switch to other task, leaving an ongoing task use git stash to keep the ongoing task on hold.

**Task 5: Cherry Picking**
1.Create a branch feature-hotfix, make 3 commits with different changes

2.Switch to main

3.Cherry-pick only the second commit from feature-hotfix onto main

4.Verify with git log that only that one commit was applied

![Image](https://github.com/user-attachments/assets/60d1b582-aea9-4836-81de-ce3ed9b1c71b)
![Image](https://github.com/user-attachments/assets/2d5d69f9-809a-4ec4-9ef2-208a722f21f6)

5.Answer in your notes:

* What does cherry-pick do?
  
ans: Cherry pick is used to pick the commit of a specific feature out of many commits from different branch, to pick and implement in our current work.

* When would you use cherry-pick in a real project?
  
ans: When there is a need to implement a change from a specific commit in our current project. 

* What can go wrong with cherry-picking?
  
ans: If the same branch is merged then it will show conflicts due to duplicate commits.
It may show conflicts if the commit depends on previous commits.


