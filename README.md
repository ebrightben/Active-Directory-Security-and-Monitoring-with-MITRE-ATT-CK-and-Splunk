
<h1> Active Directory Security and Monitoring with MITRE ATT&CK and Splunk</h1>



<h2>Description</h2>
The project aimed to develop an Active Directory (AD) environment simulating a realistic enterprise network, complete with various security monitoring capabilities. The main focus was to enhance understanding of cybersecurity tools, techniques, and threat detection by utilizing MITRE ATT&CK techniques to generate events for analysis in Splunk.
<br />


<h2>Languages, Environments and Utilities Used</h2>

### **Virtual Machines:**  
Four virtual machines were deployed in **VirtualBox** to create a comprehensive lab environment:

- **Ubuntu Server:**  
  - Configured with **Splunk** for data ingestion and monitoring.

- **Windows 2022 Server:**  
  - Set up as the **Active Directory (AD) Domain Controller**.  
  - Installed with **Sysmon** and **Splunk’s Universal Forwarder** for event logging and monitoring.

- **Windows 10 Workstation:**  
  - Installed with **Sysmon** and the **Universal Forwarder** to simulate endpoint activities and user behaviors.

- **Kali Linux:**  
  - Used as an **attack machine** to execute various security tests against the environment.

---

### **Splunk Configuration:**
- **Splunk Enterprise** was installed on the **Ubuntu server** and configured to receive logs from the Windows machines.  
- Key configurations were made within **`inputs.conf`** to allow the collection of:  
  - **Application Logs**  
  - **Security Logs**  
  - **System Logs**  
  - **Sysmon Logs**  

- All collected logs were stored under a dedicated **endpoint index** for easy filtering and event search in Splunk.

---

### **Security Tools:**

- **Crowbar:**  
  - Used to test for **RDP brute-force detection** by attempting logins on the Windows machines.

- **MITRE ATT&CK:**  
  - Integrated into the environment by installing **Atomic Red Team** on the **Windows 10 machine**.  
  - Simulated a range of adversarial techniques by executing **PowerShell commands**, aligning the tests with MITRE ATT&CK framework techniques.


<h2>Program walk-through:</h2> 
 Active Directory & Splunk Security Lab Synopsis

This project involved setting up a cybersecurity lab that integrates **Active Directory (AD)**, **Splunk**, **MITRE ATT&CK** and **Crowbar** techniques to simulate, detect, and analyze security events. The lab environment includes virtual machines for **Windows Server 2022**, **Windows 10**, **Kali Linux**, and **Ubuntu (Splunk server)**. Throughout the process, I configured **universal forwarders** and **Sysmon** on the **Windows 10** and **Windows 2022 server** machines to forward security logs to Splunk for real-time monitoring and analysis.

---

## Phase 1: Initial Setup and Splunk Installation

I began the setup by creating a virtual environment using **Oracle VirtualBox**. On the **Ubuntu VM**, I installed **Splunk Enterprise** to act as the central logging server. I ensured that shared folders between the host and the virtual machine were correctly configured to make file management seamless.

I downloaded the appropriate **Splunk .deb package** for Linux and added my user to the `vboxsf` group, ensuring I had access to shared directories for the installation.

### Network Diagram Created  
![Network Diagram](https://imgur.com/UIaKqtz.png)

### Virtual Machines Configured  
![VMs Configured](https://imgur.com/JFPADiF.png)

### Splunk Installed on Ubuntu  
![Splunk Installed](https://imgur.com/B9jc1wX.png)

### Static IP Set for Splunk  
![Static IP](https://imgur.com/Z3ggj83.png)

---

## Phase 2: Universal Forwarder and Sysmon Installation on Windows Servers

In this phase, I installed the **universal forwarder** on both the **Windows 10** and **Windows Server 2022** machines. This forwarder ensures that security logs from both machines are sent directly to Splunk.

Additionally, I installed **Sysmon** (System Monitor) on both the Windows client and server to generate detailed security logs, such as process creations and network connections. Sysmon’s data is sent through the forwarder to Splunk, providing crucial visibility into system events for incident detection and response.

### Universal Forwarder and Sysmon Installed  
![UF and Sysmon](https://imgur.com/MdL0RUB.png)

### Both Client and Server Forward Logs to Splunk  
![Logs Sent to Splunk](https://imgur.com/wJ7mnMu.png)

---

## Phase 3: Active Directory Configuration

Next, I deployed **Windows Server 2022** as the **Domain Controller (DC)** and configured **Active Directory (AD)**. I added multiple **Organizational Units (OUs)** to logically separate accounts and created specific users, including **Erin Smith** and **John Jacob**, to simulate employee identities. Both users were given **Remote Desktop (RDP)** access privileges for later testing.

I also joined a **Windows 10 VM** to the AD domain to function as a client machine. This allowed me to simulate interactions between endpoints and the domain controller.

### Active Directory Domain Established  
![AD Established](https://imgur.com/gZ1eWI2.png)

### Organizational Units and Users Created  
![OUs Created](https://imgur.com/ZyrZSNO.png)  
![Users Added](https://imgur.com/75O9sVx.png)

### Windows 10 Added to Domain as Client Machine  
![Windows 10 Added to Domain](https://imgur.com/A1tx3tv.png)

---

## Phase 4: Red Team Simulations Using Crowbar

For red-team testing, I used **Crowbar** on the **Kali Linux machine** to perform **RDP brute force attacks** against the Windows machines. Using a subset of passwords from the **rockyou.txt** wordlist, I successfully authenticated as **John Jacob** and **Erin Smith** over RDP. These events were captured and logged within Splunk, ensuring end-to-end visibility of the attack path.

### Using Crowbar for RDP Brute Force Attack  
![Crowbar Attack](https://imgur.com/DHIv3kz.png)

### Event Captured in Splunk  
![Splunk Event](https://imgur.com/zVBaeiM.png)

---

## Phase 5: Running Atomic Red Team Tests

To further simulate real-world attacks, I installed **Atomic Red Team** on the **Windows 10 machine**. Atomic Red Team provided access to specific MITRE ATT&CK tests, such as **T1136 (Create Account)**, to generate relevant security events. I executed **T1136.001 (Local Account Creation)**, which triggered **4720 and 4726 events** in Splunk, confirming that the account creation and deletion were successfully monitored.

### Installed Atomic Red Team on Windows 10  
![Atomic Red Team Install](https://imgur.com/miLevTb.png)

### Found the File for Creating Local Account  
![File Found](https://imgur.com/pao91As.png)  
![Account Created](https://imgur.com/gUsoy6Z.png)

### Security Event Captured in Splunk  
![Security Event](https://imgur.com/h2Vs6EH.png)

---

## Conclusion

This project successfully demonstrated the deployment of an integrated cybersecurity lab using **Active Directory, Splunk, and Sysmon**. With the **universal forwarder** installed on both **Windows systems**, logs from Sysmon and other event channels were indexed into Splunk, providing **real-time visibility and analysis**.

The use of **Kali Linux** for red-team simulations and **Atomic Red Team** for MITRE ATT&CK testing allowed me to validate the lab’s capability to detect and log suspicious activity. This hands-on experience has strengthened my understanding of logging, monitoring, and incident detection, providing valuable insights into enterprise security operations.






