**Task 1: Key-Value Pairs**

Create person.yaml that describes yourself with:
name
role
experience_years
learning (a boolean)

<img width="232" height="102" alt="image" src="https://github.com/user-attachments/assets/147330dd-18bf-477a-a4d3-40681c4a8e83" />

<img width="445" height="168" alt="image" src="https://github.com/user-attachments/assets/29627fb4-159c-4ceb-aaf1-b82ce6a822a1" />

<img width="516" height="475" alt="image" src="https://github.com/user-attachments/assets/2150c9c9-ec6f-42db-9f40-1483f307d447" />


**Task 2: Lists**
Add to person.yaml:

tools — a list of 5 DevOps tools you know or are learning

hobbies — a list using the inline format [item1, item2]

<img width="581" height="212" alt="image" src="https://github.com/user-attachments/assets/e65540d4-59a3-452e-bd1d-254110dce43e" />

<img width="575" height="516" alt="image" src="https://github.com/user-attachments/assets/3f2f9836-d7b8-42fa-a407-3bd3333d72a0" />

<img width="510" height="477" alt="image" src="https://github.com/user-attachments/assets/eca87dca-0e61-48b2-9071-5099acb14a3f" />

 What are the two ways to write a list in YAML?
 
 Lists can be written in two ways : block style and inline style within brackets . but the most preffered being the block style 
 
 due to its convenience .
 

**Task 3: Nested Objects**

Create server.yaml that describes a server:

* server with nested keys: name, ip, port
  
* database with nested keys: host, name, credentials (nested further: user, password)
  
Try adding a tab instead of spaces — what happens when you validate it?

<img width="291" height="197" alt="image" src="https://github.com/user-attachments/assets/4b242510-f225-4de9-8115-b4286fe8c139" />

<img width="388" height="252" alt="image" src="https://github.com/user-attachments/assets/f1ca77b6-5c15-437c-ad94-74c8600e59cf" />

<img width="986" height="653" alt="image" src="https://github.com/user-attachments/assets/a13e114e-35f9-4f85-bcf8-962315de6f54" />

When we use tab instead of space key for spacing, the key-values are formed in the same line (instead of a next lines ). Hence giving an error when verified.

**Task 4: Multi-line Strings**

In server.yaml, add a startup_script field using:

The | block style (preserves newlines)

The > fold style (folds into one line)

Write in your notes: When would you use | vs >?

using | : is block scalar indicator this useful for preserving lengthy texts exctly as they are written

<img width="1416" height="77" alt="image" src="https://github.com/user-attachments/assets/8b602c3d-a38c-499a-9711-261ea328d126" />

<img width="1472" height="56" alt="image" src="https://github.com/user-attachments/assets/c8adad0d-cd2b-4a74-91c6-4f623ff0b909" />

<img width="806" height="478" alt="image" src="https://github.com/user-attachments/assets/62dc2536-d93a-41a3-a652-a5039387a0c3" />

using > : this is a folded multiline indicator this is used interpret the string as a single continuos line 

<img width="1405" height="92" alt="image" src="https://github.com/user-attachments/assets/9674ec55-29b8-4720-a651-17d93388604e" />

<img width="800" height="477" alt="image" src="https://github.com/user-attachments/assets/5142e1ed-626c-4ff0-b58a-1b8a00f0aec0" />

**Task 5: Validate Your YAML**

Install yamllint or use an online validator

Validate both your YAML files

Intentionally break the indentation — what error do you get?

Fix it and validate again

person.yaml:

<img width="742" height="698" alt="image" src="https://github.com/user-attachments/assets/7e3d1da8-73a3-4df1-b896-39eaa8f81c89" />

<img width="581" height="212" alt="image" src="https://github.com/user-attachments/assets/e65540d4-59a3-452e-bd1d-254110dce43e" />

<img width="510" height="477" alt="image" src="https://github.com/user-attachments/assets/eca87dca-0e61-48b2-9071-5099acb14a3f" />

server.yaml :

<img width="1412" height="296" alt="image" src="https://github.com/user-attachments/assets/73505831-027f-44da-bed4-d1f527fa3d42" />

<img width="1417" height="288" alt="image" src="https://github.com/user-attachments/assets/c70f3703-2472-4f9b-ae96-6c0fc4609843" />

<img width="802" height="478" alt="image" src="https://github.com/user-attachments/assets/9eef5a81-e15d-484c-b6d7-130f51a83704" />

**Task 6: Spot the Difference**

Read both blocks and write what's wrong with the second one:

the second block has wrong indentation. the correct way of writing it is :

<img width="277" height="477" alt="image" src="https://github.com/user-attachments/assets/51df8168-46af-480d-990f-bccb87db224f" />


