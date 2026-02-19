The core components of Linux ?
    The Core of Linux comprises of following components : 
       *Kernel: Kernel is the core component of Operating system located in the middle of harware and user space. This acts a mediator between the hardaware and software ensuring smooth communication.
       *User Space: This is the basically the area were the non-kernel applications run.
       *systemd/init: Both are used to initialise (start) Linux services to manage and monitor system services. Difference being systemd is used in modern linux flavours like Ubuntu, Centos etc. 
                      and init was used in older flavours of linux like redhat-Linux.


How processes are created and managed?
    A process is simply a program in execution, whatever command we run- a process is created for it. The linux kernel manages the process.
    example: 
    user runs a command -> shell sends a request to kernel -> kernel creates a new process -> process gets a unique PID(process ID)

What systemd does and why it matters?
    systemd starts the system services to manage and monitor . 
    It matters to :
                  *ensure the services are running , 
                  *improving reliability
                  *fastens boot time
      
    
