**Task 1: DNS – How Names Become IPs**

1.Explain in 3–4 lines: what happens when you type google.com in a browser?

ans:
-> First the browser checks in local cache for the corresponding IP address.

   If not present browser will send request to DNS(Domain Name Service) requesting IP address.

-> Computer sets up a secure connection (HTTPS) with Google’s servers using TCP/IP.

-> The request is routed through Google’s load balancers to the right web server.

-> The web server processes the request, may talk to application servers and databases, 
   and then sends back the webpage you see.

2.What are these record types? Write one line each:

* A: Maps a domain name to an IPv4 address.
  
* AAAA:Maps a domain name to an IPv6 address.
  
* CNAME: (Canonical Name)Forwards one domain or subdomain to another domain. 
  
* MX: (Mail Exchanger) Directs email to the proper mail server.
  
* NS: (Name Server) Identifies the authoritative DNS servers for a zone.

3.Run: dig google.com — identify the A record and TTL from the output

<img width="623" height="388" alt="image" src="https://github.com/user-attachments/assets/c638c4ca-54af-463c-a889-51477fcab4ba" />

A : record gives Ipv4 address 142.250.67.14

TTL(time to live): 201 seconds ~ 3 min.

**Task 2: IP Addressing**

1.What is an IPv4 address? How is it structured? (e.g., 192.168.1.10)

ans:  IPv4 addressing is used to uniquely identify devices on a network and enable communication between them. 

      It is made up of four 8-bit numbers called as octets, separated by a format known as dotted decimal notation.
      
      ex: 142.250.67.14
      
2.Difference between public and private IPs — give one example of each

ans:

|                     public IP                              |                               private IP                           |                          
|------------------------------------------------------------|--------------------------------------------------------------------|
| The public IP address’s scope is global                    |The private IP address only has a local scope in your own network   |
|                                                            |                                                                    |                                                                       
|The ISP assignes a public IP address                        |The router assigns a private IP address that is device specific     | 
|                                                            |                                                                    |    
|Has No network barriers to communinate                      |Only the devices within a specific network can communicate          |
|                                                            |                                                                    |
|Any IP address which is not in the range of Private IP      |Has a range : 10.0.0.0 – 10.255.255.255, 172.16.0.0 – 172.31.255.255| 
|                                                            |                                                                    |
|address. ex:142.250.67.14 {google.com)                      |              192.168.0.0 – 192.168.255.255                         |


                                                          


3.What are the private IP ranges?

ans: 
     10.0.0.0 – 10.255.255.255, 

     172.16.0.0 – 172.31.255.255, 

     192.168.0.0 – 192.168.255.255

4.Run: ip addr show — identify which of your IPs are private

ans: 

<img width="872" height="317" alt="image" src="https://github.com/user-attachments/assets/10cfbfab-62c8-4779-bc4c-cfca3a0671ed" />

127.0.0.1/8  : is public for local host 

172.31.46.244/20 &  172.17.0.1/16 :  is private

**Task 3: CIDR & Subnetting**

1.What does /24 mean in 192.168.1.0/24?

ans: /24 is CIDR notation indicating that the first 24 bits of the 32-bit address are the network prefix, while the last 8 bits are 

     for host devices.

2.How many usable hosts in a /24? A /16? A /28?

ans: /24: 256

     /16: 65,536
     
     /28: 16
     
3.Explain in your own words: why do we subnet?.

ans: Subnet is required to divide a large band of internet and distribute it in the local efficiently to manage the traffic.

4.Quick exercise — fill in:

| CIDR  |  Subnet Mask  | Total Ips | Usable Hosts |                        
|-------|---------------|-----------|--------------|
| /24   |255.255.255.0  |    256    |     254      |        
| /16   |255.255.0.0    |   65,536  |   65,534     |                                                                                                                             
| /28   |255.255.255.240|     16    |      14      |

**Task 4: Ports – The Doors to Services**

1.What is a port? Why do we need them?

ans: A port is a virtual entrypoint into a network used to identify specific processes or services, acting as a "door" that 

     routes data to the correct application

2.Document these common ports:

  22	  : SSH 
  
  80	  : nginx
  
  443	  : Https
  
  53	  : DNS
  
  3306	: MySQL
  
  6379	: Redis
  
  27017 : MongoDB 

3.Run ss -tulpn — match at least 2 listening ports to their services

<img width="1895" height="266" alt="image" src="https://github.com/user-attachments/assets/76cb782a-ddae-457e-bc02-58ed05398800" />

port 22: SSH

port 80: nginx

**Task 5: Putting It Together**

* You run curl http://myapp.com:8080 — what networking concepts from today are involved?
  
  ans:
      * Protocol HTTP
  
      * Localhost : Resolve to loopback IP it resolves to 127.0.0.1
  
      * Port 80 : Apache service
  
* Your app can't reach a database at 10.0.1.50:3306 — what would you check first?
  
  ans:
       * ss -tulpn | grep 3306 - Check if port is open and service is listening.
  
       * systemctl status mysql - Check service status
  
       * nc -zv 10.0.1.50 3306 - Check connectivity
  
       * journalctl -u mysql - Check Logs


  



                        








