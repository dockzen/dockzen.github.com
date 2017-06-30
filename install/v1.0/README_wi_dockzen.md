# Install Dockzen Host OS #
It is very easy way to use dockzen. Light-weight Host OS(based on Tizen) is including all packages and it shows you the docker world rapidly.  


## Pre-condition ##
>Target : Raspberry pi3  
>Host-OS : Light-weight Tizen

## Process ##
### Step 1. Flash SD card
- Download Tizen Host OS   
- Format SD card   
`$ sudo ./sd_fusing_rpi3.sh -d ./dev/sdX -format`
- Flash boot into SD card  
`$ sudo ./sd_fusing_rpi3.sh -d ./dev/sdX   -b tizen-boot-20170629.tar.gz`
- Flash Tizen OS into SD card  
`$ sudo ./sd_fusing_rpi3.sh -d ./dev/sdX   -b tizen-minimal_20170629.tar.gz`

### Step 2. Bring up Raspberrypi3

### Step 3. Network Setting
- Set IP configuration through tool

Tizen support connmanctl as a network-mgr tool 
   
    # connmanctl  
    connmanctl > services  
    * AR Wired ethernet_X_cable
    connmanctl > config  ethernet_X_cable --ipv4 manual 10.10.10.10 255.255.255.0 10.10.10.1
    connmanctl > config  ethernet_XX_cable --nameservers 2.2.2.2
- Enable wifi or ethernet   

Tizen support wifi_test cli tool

    # wifi_test 
    1
    Event received from stdin
    Wifi init succeeded
    Operation succeeded!
    3
    Event received from stdin
    Operation succeeded!
    [ 35.759546] brcmfmac: power management disabled
    [ 35.776402] IPv6: ADDRCONF(NETDEV_UP): wlan0: link is not ready
    Wi-Fi Activation Succeeded
    Device state changed callback, state : Activated
    Event received from stdin 

- Check IP using 'ifconfig'

### Step 4. Check Containers info
`tizen_headless.json : tizen platform container`  
`dockzen_agent.json : agent container`  
These files say that which containers should be run and managed.  
You can find these in */etc/dockzen/config/image/*.  
Agent container has functionalites of remote management via cloud server.

    root@localhost:~# docker service ls
    IDNAME   MODEREPLICAS  IMAGE
    h9tuffapxqev  agent  replicated  1/1   10.113.62.204:443/dockzen-agent-arm:v1.0
    qhyku7vejmxr  tizen  replicated  1/1   10.113.62.204:443/headless:v0.1

### Step 5. Check Dash board (Optional)
Dockzen-agent has connection with dedicated cloud server.  
You can get containers information from device via web pages in cloud server. currently we doesn't open the enrolled cloud server and we have a plan to expose soon.
