# Internet Protocol Troubleshooting Commands 🌐

---

## Lab Overview & Objectives 🎯

In this lab, I will:
- ✅ Practice essential networking troubleshooting commands
- ✅ Understand how each command maps to OSI model layers
- ✅ Identify real-world customer scenarios for each command
- ✅ Apply commands to diagnose connectivity issues
---

## Scenario 📋

**My Role:** New Network Administrator troubleshooting customer issues

As a network administrator, I need to master common troubleshooting commands to diagnose and resolve customer connectivity problems efficiently. This lab provides hands-on practice with the most frequently used networking commands.

---

## Accessing the Lab Environment 🔑

1. At the top of these instructions, selected **Start Lab**
2. Waited for "Lab status: ready" message
3. Selected **AWS** to open the AWS Management Console
4. Arranged browser tabs for side-by-side viewing

---

## Task 1️⃣: Connect to Amazon Linux EC2 Instance via SSH 🔌

### For Windows Users (PuTTY):

1. Selected the **Details** drop-down menu above instructions
2. Selected **Show** to display Credentials window
3. Downloaded the **labsuser.ppk** file
4. Made note of the **PublicIP** address
5. Downloaded and installed **PuTTY** from https://www.putty.org/
6. Opened putty.exe and configured:
   - Host Name: `ec2-user@<public-ip-address>`
   - Connection > SSH > Auth: Browsed and selected `labsuser.ppk`
7. Clicked **Open** and **Yes** when prompted


<img width="645" height="596" alt="Screenshot 2026-02-22 201353" src="https://github.com/user-attachments/assets/302d234c-e644-4ccc-968f-0e6d7ba69416" />


---

## Task 2️⃣: Practice Troubleshooting Commands by OSI Layer 📊

### Troubleshooting Commands and OSI Model Correlation:

| OSI Layer | Layer Name | Troubleshooting Command | Purpose |
|-----------|------------|------------------------|---------|
| Layer 3 | Network | `ping`, `traceroute` | Test IP connectivity and path |
| Layer 4 | Transport | `netstat`, `telnet` | Check ports and connections |
| Layer 7 | Application | `curl` | Test application-layer services |


---

### Layer 3 Commands: Network Layer 🌍

#### Command 1: `ping` - Test Basic Connectivity

**Customer Scenario Example:**
> *"The customer has launched an EC2 instance. To test connectivity to and from it, run the ping command. You can use this command to test connectivity and ensure that it allows Internet Control Message Protocol (ICMP) requests on the security level, such as security groups and network ACLs."*

**Command Syntax:**
```bash
ping <destination> [options]
```

**Common Options:**
| Option | Description |
|--------|-------------|
| `-c <count>` | Send specified number of packets |
| `-i <interval>` | Wait interval seconds between packets |
| `-s <packetsize>` | Specify packet size |
| `-W <deadline>` | Time to wait for response |

**Practice Exercise:**

In the Linux terminal, run:
```bash
ping 8.8.8.8 -c 5
```
<img width="1900" height="1013" alt="Screenshot 2026-02-22 202248" src="https://github.com/user-attachments/assets/8f2fd6c7-7682-46d4-a783-764a27062b9e" />

**Expected Output:**
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=115 time=11.3 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=115 time=11.1 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=115 time=10.9 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=115 time=11.2 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=115 time=11.0 ms

--- 8.8.8.8 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 10.9/11.1/11.3/0.141 ms
```


**What I Learned:**
- ✅ Ping confirms IP-level connectivity
- ✅ 0% packet loss indicates stable connection
- ✅ Round-trip time (RTT) shows latency
- ✅ ICMP must be allowed through firewalls/security groups

**Troubles Scenarios for ping:**
| Symptom | Possible Cause |
|---------|----------------|
| 100% packet loss | No route, firewall blocking, or target down |
| High latency | Network congestion, distance, or bandwidth issues |
| Intermittent loss | Unstable connection or network saturation |

---

#### Command 2: `traceroute` - Trace Network Path

**Customer Scenario Example:**
> *"The customer is having latency issues. They say that their connection is taking a long time, and they are having packet loss. They aren't sure if it is related to AWS or their internet service provider (ISP). To investigate, you can run the traceroute command from their AWS resource to the server that they are trying to reach."*

**Command Syntax:**
```bash
traceroute <destination> [options]
```



**Common Options:**
| Option | Description |
|--------|-------------|
| `-n` | Show IP addresses, don't resolve hostnames |
| `-w <seconds>` | Wait time for response |
| `-m <hops>` | Maximum number of hops |
| `-p <port>` | Use specific port |

**Practice Exercise:**

In the Linux terminal, run:
```bash
traceroute 8.8.8.8
```

<img width="1900" height="1013" alt="Screenshot 2026-02-22 202248" src="https://github.com/user-attachments/assets/ff2ab3ea-644b-4110-b5fb-3879c7b65d83" />

**Expected Output:**
```
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  ip-10-0-0-1.ec2.internal (10.0.0.1)  0.456 ms  0.432 ms  0.412 ms
 2  100.66.4.81 (100.66.4.81)  0.981 ms  0.967 ms  0.951 ms
 3  100.66.6.126 (100.66.6.126)  1.112 ms  1.098 ms  1.082 ms
 4  100.66.16.66 (100.66.16.66)  1.234 ms  1.218 ms  1.202 ms
 5  100.66.8.160 (100.66.8.160)  1.456 ms  1.442 ms  1.426 ms
 6  52.93.39.119 (52.93.39.119)  1.678 ms  1.662 ms  1.646 ms
 7  52.93.39.86 (52.93.39.86)  2.101 ms  2.087 ms  2.071 ms
 8  52.93.39.72 (52.93.39.72)  2.345 ms  2.329 ms  2.313 ms
 9  72.14.215.194 (72.14.215.194)  10.567 ms  10.551 ms  10.535 ms
10  108.170.251.129 (108.170.251.129)  11.234 ms  11.218 ms  11.202 ms
11  216.239.43.117 (216.239.43.117)  11.567 ms  11.551 ms  11.535 ms
12  8.8.8.8 (8.8.8.8)  11.890 ms  11.874 ms  11.858 ms
```



**What I Learned:**
- ✅ Each line is a "hop" (router along the path)
- ✅ Three times per hop show packet round-trip times
- ✅ `***` indicates a failed hop (no response)
- ✅ Latency spikes help identify problem segments

**Interpreting Traceroute Results:**

| Observation | Interpretation |
|-------------|----------------|
| Consistent low latency at all hops | Healthy network path |
| Sudden latency increase at specific hop | Possible geographic distance or congestion |
| `***` at multiple consecutive hops | Router configured not to respond or packet loss |
| Latency increases near end | Issue near destination |
| Latency increases near beginning | Issue near source (LAN/ISP) |

**Troubleshooting with traceroute:**
- If packet loss occurs toward the destination → Server/ISP issue
- If packet loss occurs toward the source → AWS/LAN issue

---

### Layer 4 Commands: Transport Layer 🔌

#### Command 3: `netstat` - Network Statistics

**Customer Scenario Example:**
> *"Your company is running a routine security scan and found that one of the ports on a certain subnet is compromised. To confirm, you run the netstat command on a local host on that subnet to confirm if the port is listening when it shouldn't be."*

**Command Syntax:**
```bash
netstat [options]
```

**Common Options:**
| Option | Description |
|--------|-------------|
| `-t` | Show TCP connections |
| `-u` | Show UDP connections |
| `-l` | Show listening sockets |
| `-p` | Show process using socket |
| `-n` | Show numerical addresses (no resolution) |
| `-a` | Show all connections |

**Practice Exercise 1 - Established Connections:**

In the Linux terminal, run:
```bash
netstat -tp
```




**Expected Output:**
```
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 ip-10-0-0-10.ec2.:ssh 203.0.113.45:54321      ESTABLISHED 1234/sshd: ec2-user 
tcp        0      0 ip-10-0-0-10.ec2.:ssh 203.0.113.46:54322      ESTABLISHED 1235/sshd: ec2-user 
tcp6       0      0 ip-10-0-0-10.ec2.:ssh 203.0.113.47:54323      ESTABLISHED 1236/sshd: ec2-user
```


**Practice Exercise 2 - Listening Services:**

In the Linux terminal, run:
```bash
netstat -tlp
```

**Expected Output:**
```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN      1234/sshd           
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN      1234/sshd           
tcp        0      0 0.0.0.0:http            0.0.0.0:*               LISTEN      2234/httpd          
tcp6       0      0 [::]:http               [::]:*                  LISTEN      2234/httpd
```

**Practice Exercise 3 - Numeric Listening Ports:**

In the Linux terminal, run:
```bash
netstat -ntlp
```

**Expected Output:**
```
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1234/sshd           
tcp6       0      0 :::22                   :::*                    LISTEN      1234/sshd           
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      2234/httpd          
tcp6       0      0 :::80                   :::*                    LISTEN      2234/httpd
```

**What I Learned:**

| Command | Purpose |
|---------|---------|
| `netstat -tp` | Shows active established connections |
| `netstat -tlp` | Shows services currently listening for connections |
| `netstat -ntlp` | Shows listening services with port numbers only (faster) |

**Security Use Cases:**
- ✅ Identify unexpected listening ports (potential malware)
- ✅ Confirm expected services are running
- ✅ Track active connections to/from the host
- ✅ Troubleshoot "port already in use" errors

---

#### Command 4: `telnet` - Test Port Connectivity

**Customer Scenario Example:**
> *"The customer has a secure web server and has custom security group rules and network ACL rules configured. However, they are concerned that port 80 is open even though it shows their security settings indicate that their security group is blocking this port. You can run telnet to ensure that the connection is refused."*

**First, Install telnet:**

In the Linux terminal, run:
```bash
sudo yum install telnet -y
```

**Command Syntax:**
```bash
telnet <hostname/IP> <port>
```

**Practice Exercise - Test HTTP Port 80:**

In the Linux terminal, run:
```bash
telnet www.google.com 80
```

<img width="1900" height="1017" alt="Screenshot 2026-02-22 202420" src="https://github.com/user-attachments/assets/95c5d3aa-5a0c-40de-b09e-6aa81a32dbdf" />

**Expected Output:**
```
Trying 142.250.190.36...
Connected to www.google.com.
Escape character is '^]'.

GET / HTTP/1.1
Host: www.google.com

HTTP/1.1 200 OK
Date: Mon, 02 Mar 2026 15:30:45 GMT
Expires: -1
Cache-Control: private, max-age=0
Content-Type: text/html; charset=ISO-8859-1
Server: gws
Content-Length: 12345
... (HTML content follows) ...
```


**To exit telnet:** Press `Ctrl + ]` then type `quit` and press Enter.

**Interpreting Telnet Results:**

| Result | Meaning |
|--------|---------|
| `Connected to...` | Port is open and accessible |
| `Connection refused` | Port is closed or blocked by firewall |
| `Connection timed out` | No route to host or host down |
| `Unable to connect` | DNS resolution or network issue |

**What I Learned:**
- ✅ Telnet tests TCP connectivity to specific ports
- ✅ Can be used for basic protocol testing (HTTP, SMTP, etc.)
- ✅ Helps verify security group and NACL rules
- ✅ Distinguishes between "blocked" and "down" scenarios

**Troubleshooting Scenarios:**

| Test Command | Expected if Working | Expected if Blocked |
|--------------|---------------------|---------------------|
| `telnet example.com 80` | "Connected" message | "Connection refused" |
| `telnet example.com 443` | "Connected" message | "Connection refused" |
| `telnet example.com 22` | "Connected" message | "Connection refused" |

---

### Layer 7 Commands: Application Layer 📱

#### Command 5: `curl` - Test Application Layer

**Customer Scenario Example:**
> *"The customer has an Apache server running, and they want to test if they are getting a successful request (200 OK), which indicates that their website is running successfully. You run a curl request to see if the customer's Apache server returns a 200 OK."*

**Command Syntax:**
```bash
curl [options] <URL>
```

**Common Options:**
| Option | Description |
|--------|-------------|
| `-I` or `--head` | Fetch headers only (HEAD request) |
| `-i` | Include headers in output (GET request) |
| `-k` | Ignore SSL certificate errors |
| `-v` or `--verbose` | Verbose output (shows details) |
| `-L` | Follow redirects |
| `-o <file>` | Output to file instead of stdout |
| `-O` | Save with remote file name |
| `-H` | Add custom header |

**Practice Exercise - Verbose Test:**

In the Linux terminal, run:
```bash
curl -vLo /dev/null https://aws.com
```

<img width="1900" height="1017" alt="Screenshot 2026-02-22 202420" src="https://github.com/user-attachments/assets/676f533c-f39f-43cc-aa9f-51d426d9ed45" />



**Expected Output:**
```
*   Trying 13.32.148.32:443...
* Connected to aws.com (13.32.148.32) port 443 (#0)
* ALPN: offers h2
* ALPN: offers http/1.1
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_128_GCM_SHA256
* ALPN: server accepted http/1.1
* Server certificate:
*  subject: C=US; ST=Washington; L=Seattle; O=Amazon Web Services; CN=aws.com
*  start date: Jan 15 00:00:00 2026 GMT
*  expire date: Feb 14 23:59:59 2027 GMT
*  issuer: C=US; O=Amazon; CN=Amazon RSA 2048 M02
*  SSL certificate verify ok.
> GET / HTTP/1.1
> Host: aws.com
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: text/html
< Content-Length: 123456
< Connection: keep-alive
< Date: Mon, 02 Mar 2026 15:35:22 GMT
< Server: Server
< Last-Modified: Mon, 02 Mar 2026 10:15:00 GMT
< ETag: "123456-abc123def456"
< Accept-Ranges: bytes
< 
{ [123456 bytes data]
* Connection #0 to host aws.com left intact
```


**Practice Exercise - Check Headers Only:**

```bash
curl -I https://aws.com
```

**Expected Output:**
```
HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 123456
Connection: keep-alive
Date: Mon, 02 Mar 2026 15:36:45 GMT
Server: Server
Last-Modified: Mon, 02 Mar 2026 10:15:00 GMT
ETag: "123456-abc123def456"
Accept-Ranges: bytes
```

**What I Learned:**

| curl Response | Meaning |
|----------------|---------|
| `200 OK` | Website is working correctly |
| `301/302` | Page has moved (redirect) |
| `403 Forbidden` | Access denied (permissions issue) |
| `404 Not Found` | Page doesn't exist |
| `500 Internal Server Error` | Server-side error |
| `503 Service Unavailable` | Server overloaded or down |
| `Connection refused` | Service not running or blocked |

**Common curl Troubleshooting Scenarios:**

| Scenario | Command | What to Look For |
|----------|---------|------------------|
| Website down? | `curl -I https://example.com` | HTTP status code |
| SSL issues? | `curl -vk https://example.com` | Certificate details |
| Redirects? | `curl -IL https://example.com` | All redirect locations |
| Load time? | `curl -w "@curl-format.txt" -o /dev/null -s https://example.com` | Timing details |
| Custom headers? | `curl -H "Host: example.com" http://1.2.3.4` | Virtual host testing |

---

## Troubleshooting Command Quick Reference 📋

### Command Summary Table:

| Command | OSI Layer | Primary Use | Example |
|---------|-----------|-------------|---------|
| `ping` | Layer 3 | Basic connectivity test | `ping 8.8.8.8 -c 5` |
| `traceroute` | Layer 3 | Path and latency analysis | `traceroute 8.8.8.8` |
| `netstat` | Layer 4 | Port and connection status | `netstat -tlp` |
| `telnet` | Layer 4 | Port-specific connectivity | `telnet google.com 80` |
| `curl` | Layer 7 | Application layer testing | `curl -I https://aws.com` |

### Troubleshooting Methodology Flowchart:

```
START: User reports connectivity issue
        ↓
[Layer 3] Can you ping the destination?
        ↓
    YES → Continue to next layer
    NO  → Check routing, firewalls, security groups
        ↓
[Layer 4] Can you telnet to specific port?
        ↓
    YES → Continue to next layer
    NO  → Check port blocking, service status
        ↓
[Layer 7] Does curl return 200 OK?
        ↓
    YES → Application is working
    NO  → Check web server, application config
        ↓
SOLUTION IDENTIFIED
```

### Error Interpretation Guide:

| Error Message | Likely Cause | Command to Verify |
|---------------|--------------|-------------------|
| "Destination Host Unreachable" | No route to host | `traceroute` |
| "Connection timed out" | Firewall blocking or host down | `telnet` |
| "Connection refused" | Port closed or service not running | `netstat -tlp` on server |
| "Network is unreachable" | Interface down or no default route | `ip route` |
| "100% packet loss" | Network disconnection | Check physical/cloud connectivity |
| "403 Forbidden" | Permissions issue | `curl -I` to check server response |
| "500 Internal Error" | Application error | Check application logs |

---

## Real-World Customer Scenarios 🎭

### Scenario 1: EC2 Instance Cannot Connect to Internet

**Customer Complaint:** "My EC2 instance can't reach the internet."

**Troubleshooting Approach:**

```bash
# Step 1: Test basic connectivity
ping 8.8.8.8 -c 3
# If fails, check security groups and route tables

# Step 2: Trace the path
traceroute 8.8.8.8
# Identify where packets stop

# Step 3: Check if specific ports are blocked
telnet google.com 80
# Verify HTTP access

# Step 4: Test application layer
curl -I https://aws.com
# Check HTTP response
```
---

## Lab Completion Summary ✅

### Commands Practiced:

| Command | Successfully Executed | Understood Output |
|---------|----------------------|-------------------|
| `ping` | ✅ | ✅ |
| `traceroute` | ✅ | ✅ |
| `netstat -tp` | ✅ | ✅ |
| `netstat -tlp` | ✅ | ✅ |
| `netstat -ntlp` | ✅ | ✅ |
| `telnet` | ✅ | ✅ |
| `curl` | ✅ | ✅ |

### Key Learning Outcomes:

| Layer | Command | What I Can Now Troubleshoot |
|-------|---------|-----------------------------|
| Layer 3 | `ping` | Basic connectivity, packet loss, latency |
| Layer 3 | `traceroute` | Network path, hop-by-hop latency, routing issues |
| Layer 4 | `netstat` | Listening services, active connections, open ports |
| Layer 4 | `telnet` | Port-specific accessibility, firewall rules |
| Layer 7 | `curl` | Web server responses, HTTP status codes, SSL issues |

### Troubleshooting Mindset:

1. **Start at the bottom (Layer 3)** and work your way up
2. **Isolate the problem** by testing each layer
3. **Use the right tool** for each layer
4. **Interpret results correctly** to identify root cause
5. **Document findings** for future reference

---

## Important Notes ⚠️

### Command Availability:
- `ping` and `traceroute` are usually pre-installed
- `telnet` may need installation (`sudo yum install telnet`)
- `netstat` is part of net-tools package
- `curl` is usually pre-installed on Amazon Linux

### Security Considerations:
- **ICMP (ping)** may be blocked by security groups/NACLs
- **Telnet** sends data in plaintext (use for testing only)
- **Netstat** shows all connections (sensitive information)
- **Curl** with `-k` ignores SSL warnings (testing only)

### When Commands "Fail":
| Command | "Failure" Output | What It Really Means |
|---------|------------------|----------------------|
| `ping` | "100% packet loss" | No connectivity OR ICMP blocked |
| `traceroute` | `*** *** ***` | Router doesn't respond to traceroute |
| `telnet` | "Connection refused" | Port is closed (good for security) |
| `curl` | "Failed to connect" | Service down or blocked |

---

## Additional Resources 📚

- [ping man page](https://linux.die.net/man/8/ping)
- [traceroute man page](https://linux.die.net/man/8/traceroute)
- [netstat man page](https://linux.die.net/man/8/netstat)
- [telnet man page](https://linux.die.net/man/1/telnet)
- [curl documentation](https://curl.se/docs/manpage.html)
- [AWS VPC Troubleshooting Guide](https://docs.aws.amazon.com/vpc/latest/userguide/troubleshooting.html)
- [EC2 Network Troubleshooting](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/TroubleshootingInstancesConnecting.html)

---

## Conclusion 🎉

I have now successfully:

- ✅ Connected to an EC2 instance via SSH
- ✅ Practiced Layer 3 commands: `ping` and `traceroute`
- ✅ Practiced Layer 4 commands: `netstat` and `telnet`
- ✅ Practiced Layer 7 commands: `curl`
- ✅ Learned to interpret command outputs
- ✅ Understood real-world customer scenarios for each command
- ✅ Developed a layered troubleshooting methodology

**Key Takeaway:** Troubleshooting networking issues requires a systematic approach moving up the OSI model layers. Each command provides specific insights, and together they form a complete toolkit for diagnosing and resolving customer connectivity problems.

---
