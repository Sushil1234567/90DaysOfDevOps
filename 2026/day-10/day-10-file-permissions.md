**Master file permissions and basic file operations in Linux.**

**Task 1: Create Files**

* Create empty file devops.txt using touch

  <img width="410" height="48" alt="image" src="https://github.com/user-attachments/assets/f0dd69a7-8016-4d1f-81c6-7e934a827790" />

* Create notes.txt with some content using cat or echo

  <img width="476" height="77" alt="image" src="https://github.com/user-attachments/assets/e7fc0c80-6c89-4523-aa4c-80ebff00c9b2" />

* Create script.sh using vim with content: echo "Hello DevOps"

  <img width="368" height="131" alt="image" src="https://github.com/user-attachments/assets/fcfb5768-d6a4-43ef-8854-27f480a89a07" />
  
* Verify: ls -l to see permissions

  <img width="507" height="133" alt="image" src="https://github.com/user-attachments/assets/88c4b08e-69e2-476b-afec-3e9c48776812" />


**Task 2: Read Files**

* Read notes.txt using cat

  <img width="373" height="67" alt="image" src="https://github.com/user-attachments/assets/fc69238d-7b61-4b62-9dc9-cabce6d0b92c" />

* View script.sh in vim read-only mode
  
 <img width="377" height="25" alt="image" src="https://github.com/user-attachments/assets/e09be9d0-e310-4480-8a78-cdbf3ed04ef7" />
 <img width="212" height="152" alt="image" src="https://github.com/user-attachments/assets/a12642c5-8f19-465b-9a05-2ecff3edf20f" />

* Display first 5 lines of /etc/passwd using head
  
  <img width="447" height="137" alt="image" src="https://github.com/user-attachments/assets/b608394b-6a18-4e8e-acc4-388b152465a3" />

* Display last 5 lines of /etc/passwd using tail

<img width="542" height="130" alt="image" src="https://github.com/user-attachments/assets/4ede1ca3-99cb-4643-a2f3-acdaaff274ed" />


**Task 3: Understand Permissions**  

* Check your files:  devops.txt notes.txt script.sh
  
  What are current permissions? Who can read/write/execute?

  <img width="523" height="167" alt="image" src="https://github.com/user-attachments/assets/53f22d88-6e6a-49d0-806e-0483a70f35c8" />

  devops.txt: -rw-rw-r-- : 420420400 i.e owner can read and write but cannot execute
  
                                         group can read and write but cannot execute
  
                                         others can only read

  notes.txt : -rw-rw-r-- : 420420400 i.e owner can read and write but cannot execute
  
                                         group can read and write but cannot execute
  
                                         others can only read

  script.sh: -rw-rw-r-- : 420420400 i.e owner can read and write but cannot execute
  
                                         group can read and write but cannot execute
  
                                         others can only read

  
**Task 4: Modify Permissions** 

* Verify: ls -l after each change

* Make script.sh executable → run it with ./script.sh
  
  <img width="502" height="127" alt="image" src="https://github.com/user-attachments/assets/02851f86-77e3-498a-9f12-5f4c0051fdf2" />

  <img width="348" height="57" alt="image" src="https://github.com/user-attachments/assets/a0977ad5-64d8-4a25-9603-5eed29b57ad7" />


* Set devops.txt to read-only (remove write for all)

  <img width="502" height="122" alt="image" src="https://github.com/user-attachments/assets/8e958cd1-4af0-40bf-baa4-d7614b5479c0" />

  
* Set notes.txt to 640 (owner: rw, group: r, others: none)

  <img width="505" height="142" alt="image" src="https://github.com/user-attachments/assets/1f5b86d0-fde7-4d13-b6e2-3ac95ab62e4c" />

  
* Create directory project/ with permissions 755
  
  <img width="506" height="173" alt="image" src="https://github.com/user-attachments/assets/e0cf5171-d36d-4c9c-841c-fef7bd6a3c15" />

  **Task 5: Test Permissions**

* Try writing to a read-only file - what happens?

  <img width="477" height="92" alt="image" src="https://github.com/user-attachments/assets/6be75070-5097-409f-b4d8-e81967152cc6" />

* Try executing a file without execute permission

 <img width="465" height="100" alt="image" src="https://github.com/user-attachments/assets/7e119914-3bfd-42be-945a-7e0d0c75fd54" />

* Document the error messages

  error: permission denied.

         since the permission were not set for the above actions to performed on them. Permission was denied accordingly.


END.


 
      


  
  
  

  
  
 

    


    
  
