**Task 1: Basic Functions**
Create functions.sh with:
A function greet that takes a name as argument and prints Hello, <name>!
A function add that takes two numbers and prints their sum
Call both functions from the script

<img width="466" height="457" alt="image" src="https://github.com/user-attachments/assets/698d5be0-63a1-4a40-8d95-2f37d89260b1" />

<img width="433" height="130" alt="image" src="https://github.com/user-attachments/assets/3758218f-c34c-4c2b-9ae9-7828a5214b4a" />


;**Task 2: Functions with Return Values**
Create disk_check.sh with:
A function check_disk that checks disk usage of / using df -h
A function check_memory that checks free memory using free -h
A main section that calls both and prints the results

<img width="277" height="436" alt="image" src="https://github.com/user-attachments/assets/0e357b06-db56-4d86-8b57-61433fbfe3d6" />

<img width="732" height="185" alt="image" src="https://github.com/user-attachments/assets/b16e5a90-e413-41ed-9a19-22309fb5a1b6" />

**Task 3: Strict Mode — set -euo pipefail**
1.Create strict_demo.sh with set -euo pipefail at the top
2.Try using an undefined variable — what happens with set -u?
3.Try a command that fails — what happens with set -e?
4.Try a piped command where one part fails — what happens with set -o pipefail?

<img width="422" height="343" alt="image" src="https://github.com/user-attachments/assets/20896c2c-1dfc-4a2a-bd5e-d84d91296cb9" />

<img width="431" height="97" alt="image" src="https://github.com/user-attachments/assets/3f310fc8-477e-47ab-9e56-1671f569bf29" />

Document: What does each flag do?

* set -e → when enabled, the script terminates as soon as there is any error .
* set -u → when enabled, the bash treats the unset variables as errors
* set -o pipefail → if any command fails in the pipeline, set o pipefail handles this by sending a non-zero exit code . 



**Task 4: Local Variables**

1.Create local_demo.sh with:
A function that uses local keyword for variables
Show that local variables don't leak outside the function
Compare with a function that uses regular variables

<img width="536" height="422" alt="image" src="https://github.com/user-attachments/assets/8b0679a2-391a-49a0-826e-47c50f7aecb6" />

<img width="607" height="132" alt="image" src="https://github.com/user-attachments/assets/88a87a6f-8640-440b-859e-98595d4bf18c" />

**Task 5: Build a Script — System Info Reporter**
Create system_info.sh that uses functions for everything:

1.A function to print hostname and OS info
2.A function to print uptime
3.A function to print disk usage (top 5 by size)
4.A function to print memory usage
5.A function to print top 5 CPU-consuming processes
6.A main function that calls all of the above with section headers
7.Use set -euo pipefail at the top
Output should look clean and readable.

<img width="436" height="976" alt="image" src="https://github.com/user-attachments/assets/963fd929-e357-46a1-9490-5d61656b585a" />

<img width="642" height="443" alt="image" src="https://github.com/user-attachments/assets/aa682b1d-352e-4e43-ba1e-7aaaceff296d" />

<img width="837" height="687" alt="image" src="https://github.com/user-attachments/assets/8775f56d-a16f-4dba-b364-eddf8c911251" />

