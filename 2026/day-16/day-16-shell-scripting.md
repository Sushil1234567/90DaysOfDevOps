**Task 1: Your First Script**

1.Create a file hello.sh

2.Add the shebang line #!/bin/bash at the top

3.Print Hello, DevOps! using echo

4.Make it executable and run it

<img width="420" height="127" alt="image" src="https://github.com/user-attachments/assets/e08d6f54-61b1-42fd-b9a2-d268846cba3e" />

Removing the shebang line may still may execute the script if the script uses syntax or commands specific to shell, but maynot work incase of complex scripts 

leading to portability issues and unexpected behavior.

**Task 2: Variables**

1.Create variables.sh with:

* A variable for your NAME
  
* A variable for your ROLE (e.g., "DevOps Engineer")
  
* Print: Hello, I am <NAME> and I am a <ROLE>

<img width="418" height="140" alt="image" src="https://github.com/user-attachments/assets/0c2b26a3-625a-4ed3-9de4-c224bd0c2cb2" />

<img width="415" height="58" alt="image" src="https://github.com/user-attachments/assets/55fed7d9-eb62-4561-a8c8-e906bf1024fe" />

2.Try using single quotes vs double quotes — what's the difference?

upon using single quotes, the machine does not consider the variable values and echoes the same text given to echo ' '

<img width="422" height="130" alt="image" src="https://github.com/user-attachments/assets/3a9d398a-ece3-425a-b0b1-0037ebb477ee" />

<img width="381" height="67" alt="image" src="https://github.com/user-attachments/assets/a1109aa0-ab63-45f1-b2c6-4de3ee0cd2c2" />

 **Task 3: User Input with read**
 
1.Create greet.sh that:

 * Asks the user for their name using read
   
 * Asks for their favourite tool
   
 * Prints: Hello <name>, your favourite tool is <tool>
 
<img width="482" height="168" alt="image" src="https://github.com/user-attachments/assets/ea4308ee-e390-4543-8b11-bec00a385cbc" />

<img width="402" height="122" alt="image" src="https://github.com/user-attachments/assets/69b58a16-9675-44e9-8759-a30fe4e05e49" />

**Task 4: If-Else Conditions**

1.Create check_number.sh that:

Takes a number using read

Prints whether it is positive, negative, or zero

<img width="360" height="275" alt="image" src="https://github.com/user-attachments/assets/edce34f2-752d-4f0f-9738-0c1b392396ec" />

<img width="446" height="187" alt="image" src="https://github.com/user-attachments/assets/71b1eedd-3858-4090-87ce-9f1eff114e87" />

2.Create file_check.sh that:

Asks for a filename

Checks if the file exists using -f

Prints appropriate message

<img width="298" height="177" alt="image" src="https://github.com/user-attachments/assets/61a14377-305e-4c81-ad11-2a0fd5a924a7" />

<img width="397" height="148" alt="image" src="https://github.com/user-attachments/assets/791ebc92-ccb5-4171-b5cf-0fd5cc77d5e4" />


**Task 5: Combine It All**

Create server_check.sh that:

1.Stores a service name in a variable (e.g., nginx, sshd)

2.Asks the user: "Do you want to check the status? (y/n)"

3.If y — runs systemctl status <service> and prints whether it's active or not

4.If n — prints "Skipped."

<img width="525" height="537" alt="image" src="https://github.com/user-attachments/assets/51a11623-86d8-4a1a-864a-8dd011c96bdb" />


<img width="1168" height="498" alt="image" src="https://github.com/user-attachments/assets/93e09ba0-f9e1-4788-8c8e-5e8c5fbb631c" />

