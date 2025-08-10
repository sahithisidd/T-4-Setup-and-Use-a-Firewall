# Task 4: Setup and Use a Firewall on Windows

## Objective
The goal of this task was to configure and test basic firewall rules on Windows to allow or block traffic. I specifically tested blocking inbound traffic on port 23 (Telnet) and verified that the rule worked by attempting a local connection.


---

## Steps I Performed

### 1. Installed Nmap/Ncat
I first made sure that Nmap (and its included tool Ncat) was installed on my system.  
Ncat is a networking utility for reading and writing data across networks, similar to Netcat.

The default install location was:
C:\Program Files (x86)\Nmap


---

### 2. Opened Two Command Prompt Windows
To simulate network traffic between two endpoints on the same machine, I used two separate Command Prompt windows.

---

### 3. Started a Listener on Port 23
In the first Command Prompt, I navigated to the Nmap folder and started a listener on TCP port 23:
```bash
cd "C:\Program Files (x86)\Nmap"
ncat -lv 23
```

What this does:

* ncat → runs the Ncat program

* -lv → "listen" mode with verbose output

* 23 → port number to listen on (Telnet)

This meant my computer was now waiting for connections on port 23.

### 4. Connected to the Listener (Before Blocking)
In the second Command Prompt:
```bash
cd "C:\Program Files (x86)\Nmap"
ncat 127.0.0.1 23
```
This connected to my own machine (localhost) on port 23.
At this stage, the connection succeeded because no firewall rule was blocking it.


### 5. Created a Firewall Rule to Block Port 23
I opened Windows Defender Firewall with Advanced Security and created a new inbound rule:

1.Inbound Rules → New Rule

2.Port → TCP → Specific port: 23

3.Block the connection

4.Apply to Domain, Private, and Public profiles

5.Named it "Block Telnet port 23"

### 6. Tested the Connection Again
With the rule active, I ran the same connection command again:
```bash
ncat 127.0.0.1 23
```

This time, it failed — the firewall silently blocked the connection, proving that the rule worked.

### 8. Removed the Test Block Rule
After testing, I deleted the "Block Telnet 23" rule to restore my firewall to its original state.

