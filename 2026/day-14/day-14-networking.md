**Quick Concepts (write 1–2 bullets each)**

OSI layers (L1–L7) vs TCP/IP stack (Link, Internet, Transport, Application)

ans: * OSI has 7 leayers[ physical-> datalink-> network-> transport-> session-> presentation-> application ]

     * TCP/IP has 4 layers [ application layer, transport layer , internet , network access ]

     * The OSI layers are individiual layers whereas the TCP has combinely merged few OSI layers to individual TCP layers like :

      -[application + presentation + session ]-> Application Layer

      -[Transport]-> Transport layer

      -[Network]-> Internet Layer

      -[Datalink+Physical]-> Network Access layer

     
Where IP, TCP/UDP, HTTP/HTTPS, DNS sit in the stack


ans: * IP-> Internet Layer

     * TCP/UDP-> Transport layer
     
     * HTTP/HTTPS-> Application layer
     
     * DNS-> Application layer

One real example: “curl https://example.com = App layer over TCP over IP”
 
<img width="1897" height="671" alt="image" src="https://github.com/user-attachments/assets/3e2fe45d-15fa-4251-8580-8fc5303db2a6" />


**Hands-on Checklist**

* Identity: hostname -I 

  <img width="402" height="37" alt="image" src="https://github.com/user-attachments/assets/2b07eb98-0f5b-4530-92db-a8965a72879b" />

  **Observation**: hostname -I displays the IP address of the machine/system i.e 172.31.46.244 172.17.0.1
  
* Reachability: ping <target>

  <img width="1030" height="210" alt="image" src="https://github.com/user-attachments/assets/a8c70687-a5bb-4ecf-bfba-5cfcce1e04de" />
  
  **Observation**: ping www.omegawatches.com  Shows how long it takes for packets to reach host ·

* Path: traceroute <target>

  <img width="1737" height="210" alt="image" src="https://github.com/user-attachments/assets/c8353d61-ef31-4fc8-8e2b-a87987381b05" />

  **Observation**: shows the packets from IP to host ,60 byte packets with 30 hops ( which is a default for most cases )

* Ports: ss -tulpn

  <img width="1895" height="261" alt="image" src="https://github.com/user-attachments/assets/8040c9d7-99b7-49f5-a81f-724cc9c156af" />

  **Observation**: service ssh: is listening to port 22 & service nginx is listening to port 80

* Name resolution: dig <domain>

  <img width="692" height="422" alt="image" src="https://github.com/user-attachments/assets/4bc9b041-2ad2-486b-8c5b-8cf6ed04fc79" />

  **Observation**: Domanin resolves to 23.55.244.186

 * HTTP check: curl -I <http/https-url>
   
   <img width="975" height="245" alt="image" src="https://github.com/user-attachments/assets/34d6683b-a1c7-4610-a367-0cdb77251e61" />

   **Observation**: received HTTP/2 200 .which is a success code indicating the server is responding 

 * Connections snapshot: netstat -an | head
   
   <img width="737" height="212" alt="image" src="https://github.com/user-attachments/assets/88cdf80b-b068-4196-ab32-406f4db2adc9" />

   **Observation**: Listen :4 entries ports( 80,22,38745,53). Established :1 entry

**Mini Task: Port Probe & Interpret**

1.Identify one listening port from ss -tulpn (e.g., SSH on 22 or a local web app).

2.From the same machine, test it: nc -zv localhost <port> (or curl -I http://localhost:<port>).

3.Write one line: is it reachable? If not, what’s the next check? (e.g., service status, firewall).

<img width="1855" height="275" alt="image" src="https://github.com/user-attachments/assets/24430d92-affa-48cc-b6a3-0000a720c60f" />

the connection succeeds.

* if it is not reachable , run :

  Check service status - systemctl status ssh

  Check logs - journlctl -u ssh

  Check firewall - sudo ufw status

**Reflection**

* Which command gives you the fastest signal when something is broken?

ans : Ping command gives fastest signal if something is broken.

* What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?

ans: DNS runs on application layer , if it fails we can check the next layer i.e transport layer and internet layers . 

     by running the following commands:  
     
     -> dig, 
     
     -> nslookup
     
     -> ping
     
     -> ss -tulpn
     
     If http 500 shows:  It is application layer. Since we got response(500) it means internet and transport layers are fine. 
     
     Check at Application layer.
     
     -> systemctl status service
     
     ->journalctl -u service
     
     ->tail -f /var/log/service/error.log
     
 * Two follow-up checks you’d run in a real incident.

   -Check firewall :

    sudo ufw status, sudo iptables -L -n -v

   -Service helth check:

    systemctl status <service>

   -Connectivity test :

    curl -I http://<server-ip>:<port>,nc -zv <server-ip> <port>
