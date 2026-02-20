# run a troubleshooting drill #
Target service / process : cron.service

* Environment basics :
  
 ->uname -a : prints system related information like kernel version, and OS build.

  <img width="1105" height="37" alt="image" src="https://github.com/user-attachments/assets/bfd10847-be05-45ef-9e78-6a1f5fcb7f48" />


 ->lsb_release -a :shows linux distribution and version information
 
   <img width="392" height="107" alt="image" src="https://github.com/user-attachments/assets/1fd329bc-8918-4c35-bdbf-6075f35db5b3" />



 * Filesystem sanity:
   
   ->mkdir /tmp/runbook-demo : create a directory runbook-demo

     <img width="442" height="41" alt="image" src="https://github.com/user-attachments/assets/bd5c2f5f-891a-47bf-825f-d4a2d53e7562" />

   ->cp /etc/hosts /tmp/runbook-demo/hosts-copy : copy and renaming the file 'hosts' to 'hosts-copy' under /tmp/runbbok-demo

     <img width="637" height="25" alt="image" src="https://github.com/user-attachments/assets/de82ef2d-e1d4-466b-a3ab-e75969a9823f" />

   ->ls -l /tmp/runbook-demo : check if the file is copyied and renamed and the permissions are normal.
   
     <img width="495" height="57" alt="image" src="https://github.com/user-attachments/assets/36b63ebd-f618-4bee-8820-5a2c1593ebce" />
   

 * CPU / Memory:
   
   ->top/htop : displays real time linux processes

   <img width="906" height="362" alt="image" src="https://github.com/user-attachments/assets/894fc77d-ef04-449b-980b-2d6b0824cb24" />

   ->ps -o pid,pcpu,pmem,comm -p : Shows CPU and memory usage for a specific process.
   
   <img width="342" height="75" alt="image" src="https://github.com/user-attachments/assets/d017f0cb-4a8f-4b2c-939d-5996cbabdaf7" />

   ->free -h : Displays system memory usage in a human-readable format (RAM and swap).

     <img width="728" height="88" alt="image" src="https://github.com/user-attachments/assets/929e8a9e-b81f-432b-a6ac-605a65203340" />

   

* Disk / IO :

  ->df -h :Shows disk usage of all mounted filesystems in human-readable format (GB/MB)

  <img width="582" height="198" alt="image" src="https://github.com/user-attachments/assets/d7b37379-2a69-476e-8bc3-3f7f69d323f5" />

  ->du -sh /var/log : Shows the total size of /var/log (or any directory) in human-readable format.

  <img width="433" height="56" alt="image" src="https://github.com/user-attachments/assets/f229803a-fe41-4576-bdf1-866c95088fa0" />

  ->iostat :Shows CPU and disk I/O statistics, including read/write rates per device.
  
  <img width="858" height="312" alt="image" src="https://github.com/user-attachments/assets/2511ec63-a32c-45e1-b7da-7f8be796fe43" />

  ->vmstat :Shows memory, CPU, and I/O statistics over time.

  <img width="763" height="102" alt="image" src="https://github.com/user-attachments/assets/a58feafb-4efd-4eae-bdfc-95ef7cf4ee98" />

  ->dstat  :Combines CPU, disk, network, memory statistics in real-time.

   <img width="606" height="321" alt="image" src="https://github.com/user-attachments/assets/2bbf01af-98bb-49e5-be90-de01719a071c" />

* Network :

     ->ss -tulpn/netstat -tulpn : Shows all listening TCP/UDP ports along with the process name and PID.
     
     <img width="1891" height="285" alt="image" src="https://github.com/user-attachments/assets/29480964-6802-4b0d-a916-e1c5f5fd50c3" />

     <img width="1852" height="407" alt="image" src="https://github.com/user-attachments/assets/a9091653-144f-4234-8ca3-cfc768490840" />


     ->curl -I /ping : Sends a HEAD request to a URL or service endpoint to check connectivity and response headers.

     <img width="1902" height="478" alt="image" src="https://github.com/user-attachments/assets/84c0b423-2d85-45d1-bdff-51a007be1eff" />



* Logs :

    ->journalctl -u -n 50 -> Shows the last 50 log entries for the ssh service from systemd journal.
    
    <img width="1081" height="897" alt="image" src="https://github.com/user-attachments/assets/2f1143c3-17b3-4da4-a051-f76635fd664b" />

    ->tail -n 50 /var/log/auth.log -> Shows the last 50 lines of the authentication log file

    <img width="1672" height="897" alt="image" src="https://github.com/user-attachments/assets/39a35943-ba27-48c7-8aa1-4c0896f76f94" />


END.

    





     
  



   

   
   


   
    

 

