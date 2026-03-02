**Task 1: For Loop**

1.Create for_loop.sh that:
Loops through a list of 5 fruits and prints each one

<img width="712" height="206" alt="image" src="https://github.com/user-attachments/assets/8e1f6f4f-0f9c-4b51-a603-82e388748ff0" />

<img width="392" height="142" alt="image" src="https://github.com/user-attachments/assets/f9e4c36a-e891-4234-b96a-9d5c3dc86a1c" />

2.Create count.sh that:
Prints numbers 1 to 10 using a for loop

<img width="236" height="87" alt="image" src="https://github.com/user-attachments/assets/f805b236-9a0b-4cbb-99c1-cf0e5ba92417" />

<img width="393" height="237" alt="image" src="https://github.com/user-attachments/assets/c8e6b4a7-a117-4993-982c-a1cf2c8a69e4" />

**Task 2: While Loop**

1 Create countdown.sh that:
Takes a number from the user
Counts down to 0 using a while loop
Prints "Done!" at the end

<img width="341" height="470" alt="image" src="https://github.com/user-attachments/assets/c9073dff-9964-45db-a795-69c4110b5898" />

<img width="407" height="465" alt="image" src="https://github.com/user-attachments/assets/b621107e-7794-4983-a43a-af5920c0b773" />

**Task 3: Command-Line Arguments**

1.Create greet.sh that:
Accepts a name as $1
Prints Hello, <name>!
If no argument is passed, prints "Usage: ./greet.sh "

<img width="326" height="195" alt="image" src="https://github.com/user-attachments/assets/6523cd54-f10f-4114-838d-f74320525780" />

<img width="387" height="110" alt="image" src="https://github.com/user-attachments/assets/d79927ac-e5cd-4d7e-b37a-e921e8fe414a" />

2.Create args_demo.sh that:
Prints total number of arguments ($#)
Prints all arguments ($@)
Prints the script name ($0)

<img width="163" height="165" alt="image" src="https://github.com/user-attachments/assets/c4f8c9eb-da9e-4d33-b0a7-72864eaaf3f9" />

<img width="633" height="180" alt="image" src="https://github.com/user-attachments/assets/bee6665f-87d5-4d3c-a5f9-d31c98d5b8b2" />

**Task 4: Install Packages via Script**

1.Create install_packages.sh that:
Defines a list of packages: nginx, curl, wget
Loops through the list
Checks if each package is installed (use dpkg -s or rpm -q)
Installs it if missing, skips if already present
Prints status for each package

<img width="567" height="420" alt="image" src="https://github.com/user-attachments/assets/c474a07b-c184-4b95-8fea-58c733d7532e" />

<img width="453" height="125" alt="image" src="https://github.com/user-attachments/assets/1d043277-f589-4284-a28e-78face04a7ae" />


**Task 5: Error Handling**

1.Create safe_script.sh that:

* Uses set -e at the top (exit on error)
  
* Tries to create a directory /tmp/devops-test
  
* Tries to navigate into it
  
* Creates a file inside
  
* Uses || operator to print an error if any step fails
  
Example:
mkdir /tmp/devops-test || echo "Directory already exists"

<img width="552" height="288" alt="image" src="https://github.com/user-attachments/assets/2de76b9c-bc8e-405a-8e2f-8bd7e2635574" />

<img width="1442" height="146" alt="image" src="https://github.com/user-attachments/assets/2a1e8659-0705-4d59-9207-f7bfebc9bdc0" />

2.Modify your install_packages.sh to check if the script is being run as root — exit with a message if not.

<img width="767" height="608" alt="image" src="https://github.com/user-attachments/assets/51d5d98e-0167-48d1-81a1-4c6b64c28924" />

<img width="620" height="182" alt="image" src="https://github.com/user-attachments/assets/67dc2fcf-9a20-4e52-b8f0-8fa44f1809c1" />





