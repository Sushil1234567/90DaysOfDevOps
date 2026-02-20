**Linux File System Hierarchy & Scenario-Based Practice**

* Scenario 1: Service Not Starting

A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.

Solution:

Step 1: Command : systemctl status myapp 

        Reason: the command is used to check the real time status of the application service if active, stopped or failed

Step 2: Command : systemctl list-unit --type=myapp

        Reason: this command is used to see if the service is in the running services list

Step 3: Command : systemctl is-enabled myapp

        Reason: this command is used to see if the service is enabled mode

Step 4: Command: journalctl -u myapp -n 50

        Reason: this command is used to check the jornal logs of the top 


* Scenario 2: High CPU Usage

Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?

Solution:

Step 1: Command: ps aux --sort=-%cpu 

        Reason: this command is used to check the cpu usage in memory percentage along with process ID (PID)
        
                sorted in descending order with the process consuming highest memory listed at the top -to bottom

         

* Scenario 3: Finding Service Logs

A developer asks: "Where are the logs for the 'docker' service?"
The service is managed by systemd.
What commands would you use?

Solution:

Step 1: Command: systemctl check status docker

        Reason: this command is used to check the status of docker if it is active or inactive.

Step 2: Command: journalctl -u docker -n 50

        Reason: this command is used to check the last 50 logs ( to check any errors if any)    

Step 3: Command:  journalctl -u docker -f

        Reason: this command is used to track live logs (real time logs)

        

Scenario 4: File Permissions Issue

A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?

Solution:

Step 1: Command: ls -l backup.sh

        Reason: this command shows the contents in a directory in a list format along with permission


Step 2: Command: chmod +x backup.sh  or  chmod 777 backup.sh

        Reason: this command permits all the user ( owner, group other ) all the access i.e read , write and excute.


        






