# Install Dockzen Packages on Host OS #
It is for the users to preserve their own host OS.  
We assume that your environment is ready to run docker especially kernel. and you can install dockzen packages step by step.

## Pre-condition
>Target : Raspberry pi3

## Process

### Step 1. Bring up Raspberrypi3
We assume your Host OS and Kernel are installed properly.  
(we use Linux Kernel 4.9.x)

### Step 2. Network Setting
- Set IP configuration through tool
- Enable wifi or ethernet

### Step 3. Install Docker and dockzen packages
#### docker-engine relatives
- *rpm -Uvh docker-runc-1.0.0-2.armv7l.rpm*
- *rpm -Uvh docker-containerd-0.2.3-0.armv7l.rpm*
- *rpm -Uvh docker-engine-1.13.1-dz.armv7l.rpm*
#### dockzen relatives
- *rpm -Uvh dockzen-launcher-1.0.0-0.armv7l.rpm*

### Step 4. Modify insecure-registry (Optional)
- create config file : /etc/docker/daemon.json    
	`{"insecure-registries":["10.113.62.204:443"] }`  
If you have your insecured cloud server, this should be set.

### Step 5. Reboot and check Containers info
`- tizen_headless.json : tizen platform container`  
`- dockzen_agent.json : agent container`  
These files say that which containers should be run and managed.  
You can find these in */etc/dockzen/config/image/*.  
Agent container has functionalites of remote management via cloud server.

    root@localhost:~# docker service ls
    IDNAME   MODEREPLICAS  IMAGE
    h9tuffapxqev  agent  replicated  1/1   10.113.62.204:443/dockzen-agent-arm:v1.0
    qhyku7vejmxr  tizen  replicated  1/1   10.113.62.204:443/headless:v0.1

### Step 6. Check Dash board (Optional)
Dockzen-agent has connection with dedicated cloud server.  
You can get containers information from device via web pages in cloud server. currently we doesn't open the enrolled cloud server and we have a plan to expose soon.
