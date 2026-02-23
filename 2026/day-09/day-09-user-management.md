Linux User & Group Management Challenge

* Task 1: Create Users
  
  Create three users with home directories and passwords:
  
  tokyo
  
  berlin
  
  professor

  <img width="727" height="940" alt="image" src="https://github.com/user-attachments/assets/4d0b99b2-3133-4f54-ad9b-15e6204583c8" />
  

  * Task 2: Create Groups
  
  Create two groups:

  developers

  admins

  <img width="466" height="56" alt="image" src="https://github.com/user-attachments/assets/c19e00e2-9d5d-42d3-9b1b-f1a90c78d666" />


  <img width="290" height="112" alt="image" src="https://github.com/user-attachments/assets/265a56c9-1130-4166-98f6-e50a5f54872d" />


* Task 3: Assign to Groups
  
  Assign users:
  
  tokyo → developers
  
  berlin → developers + admins (both groups)
  
  professor → admins
  
  Verify: Use appropriate command to check group membership


<img width="540" height="38" alt="image" src="https://github.com/user-attachments/assets/35b53b5e-038f-4d5d-b09d-7aacfc3acc59" />


<img width="625" height="22" alt="image" src="https://github.com/user-attachments/assets/04ebfbdf-9996-463a-8e39-b82e37279e36" />


<img width="536" height="36" alt="image" src="https://github.com/user-attachments/assets/8b4e4c31-b96f-44a6-96a7-bcb1f74b2910" />


<img width="290" height="65" alt="image" src="https://github.com/user-attachments/assets/cd607804-0539-46a9-b627-eb11e9db443c" />



* Task 4: Shared Directory

  Create directory: /opt/dev-project
  
  Set group owner to developers
  
  Set permissions to 775 (rwxrwxr-x)
  
  Test by creating files as tokyo and berlin
  
  Verify: Check permissions and test file creation

  <img width="673" height="295" alt="image" src="https://github.com/user-attachments/assets/b7b5b441-60ad-4dcf-89e2-3d9d201c208d" />

  <img width="528" height="57" alt="image" src="https://github.com/user-attachments/assets/325c5efb-c04f-434b-8bab-f3ee73cf032c" />


* Task 5: Team Workspace
  
  Create user nairobi with home directory
  
  Create group project-team
  
  Add nairobi and tokyo to project-team
  
  Create /opt/team-workspace directory
  
  Set group to project-team, permissions to 775
  
  Test by creating file as nairobi

  <img width="896" height="871" alt="image" src="https://github.com/user-attachments/assets/cbe20427-c999-4676-b3dd-8cd25f1c0bdc" />


  



  


  





