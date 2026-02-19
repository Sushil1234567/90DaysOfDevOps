**You will create a short practice note by actually running basic commands and capturing what you see:**

* Check running processes:

  ps -a
  
  <img width="726" height="168" alt="image" src="https://github.com/user-attachments/assets/dd2d485f-d3e2-4f59-a5da-bfed579c70c3" />

  ps -ef | grep ssh
  
  <img width="1920" height="106" alt="image" src="https://github.com/user-attachments/assets/a9fb6eab-3acf-4779-bf26-03069e8929ba" />




  * Inspect one systemd service:
    
    systemctl status

    <img width="1116" height="678" alt="image" src="https://github.com/user-attachments/assets/cfed2945-48e6-4bd0-9f04-4276710bfd88" />


    systemctl show

     <img width="1896" height="827" alt="image" src="https://github.com/user-attachments/assets/841258e8-6555-4ab7-8530-8e6ef54fff32" />

    
     systemctl list-units
    
     <img width="1891" height="986" alt="image" src="https://github.com/user-attachments/assets/16fc68da-4293-47f8-81b7-d77a3282a648" />

  * Capture a small troubleshooting flow: cron jobs
    
    systemctl status cron.service  : checks the service status if the service is running

    <img width="1097" height="397" alt="image" src="https://github.com/user-attachments/assets/48a42375-104e-48c4-ae6a-322e465f8723" />

    journalctl -u cron.service : track he logs of the service

    <img width="1340" height="967" alt="image" src="https://github.com/user-attachments/assets/73312dc7-fa85-4990-ad1a-3b91d99b2fe4" />

    

