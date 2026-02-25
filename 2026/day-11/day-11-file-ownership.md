**Task 1: Understanding Ownership**

 <img width="555" height="187" alt="image" src="https://github.com/user-attachments/assets/403752ba-97ac-4e3d-8850-93f6481884c6" />

* Run ls -l in your home directory
  Identify the owner and group columns
  Check who owns your files
  What's the difference between owner and group?

  <img width="506" height="152" alt="image" src="https://github.com/user-attachments/assets/3ed2d815-7fb1-47c5-a103-e52cdb37808a" />


  Explanation:
  
  Owner : Is the person who has created the file and has the highest level of control and can modify permissions for all owner, group and others
  
  Group: Group is basically a number of users sharing a common accces to a file or a directory


**Task 2: Basic chown Operations**

   1.Create file devops-file.txt
   2.Check current owner: ls -l devops-file.txt

   <img width="566" height="186" alt="image" src="https://github.com/user-attachments/assets/df72e3db-e5d0-412b-b21d-aa0872253fdc" />

   3.Change owner to tokyo (create user if needed)

   <img width="556" height="178" alt="image" src="https://github.com/user-attachments/assets/7006629d-b279-4dd2-a35d-9e4500fc0bcb" />

   4.Change owner to berlin
   
   5.Verify the changes

   <img width="560" height="177" alt="image" src="https://github.com/user-attachments/assets/c94b08ff-eaec-4c67-8c34-4758760f3e03" />


**Task 3: Basic chgrp Operations**
 
  1.Create file team-notes.txt
  
   <img width="525" height="52" alt="image" src="https://github.com/user-attachments/assets/825f21e5-b590-4d62-8241-a80f0dfc3b8f" />

  2.Check current group: ls -l team-notes.txt

   <img width="555" height="187" alt="image" src="https://github.com/user-attachments/assets/2736e871-d726-4254-b92b-246db9678779" />

  3.Create group: sudo groupadd heist-team

   <img width="543" height="51" alt="image" src="https://github.com/user-attachments/assets/bfce5e43-9003-4cd0-85c8-1cd5e52467e6" />

  
  4.Change file group to heist-team

  <img width="587" height="50" alt="image" src="https://github.com/user-attachments/assets/004391b5-c83a-45f2-ae0f-692fdb438725" />

   Verify the change

   <img width="587" height="181" alt="image" src="https://github.com/user-attachments/assets/152b8484-d068-40f6-8e55-a9e45ff20a43" />

**Task 4: Combined Owner & Group Change** 

  1.Create file project-config.yaml
  2.Change owner to professor AND group to heist-team (one command)
  3.Create directory app-logs/
  4.Change its owner to berlin and group to heist-team

  <img width="725" height="277" alt="image" src="https://github.com/user-attachments/assets/05c8053c-f071-4408-8165-33af7f6d79bd" />


**Task 5: Recursive Ownership**

  1. Create directory structure:
     
     mkdir -p heist-project/vault
     
     mkdir -p heist-project/plans
     
     touch heist-project/vault/gold.txt
     
     touch heist-project/plans/strategy.conf

   3. Create group planners: sudo groupadd planners

   4. Change ownership of entire heist-project/ directory:

      Owner: professor
      
      Group: planners
      
      Use recursive flag (-R)

  5. Verify all files and subdirectories changed: ls -lR heist-project/

      <img width="678" height="721" alt="image" src="https://github.com/user-attachments/assets/8d507898-72e4-4f80-955d-fadceceadb04" />

  
**Task 6: Practice Challenge**

  1.Create users: tokyo, berlin, nairobi (if not already created)

  2.Create groups: vault-team, tech-team

  3.Create directory: bank-heist/

  4.Create 3 files inside:

    touch bank-heist/access-codes.txt
    
    touch bank-heist/blueprints.pdf
    
    touch bank-heist/escape-plan.txt
    
  5.Set different ownership:

    access-codes.txt → owner: tokyo, group: vault-team
    
    blueprints.pdf → owner: berlin, group: tech-team
    
    escape-plan.txt → owner: nairobi, group: vault-team
    
    Verify: ls -l bank-heist/


  <img width="771" height="450" alt="image" src="https://github.com/user-attachments/assets/20b38948-0b47-4f2a-b43f-a6810eee0ba7" />

  
