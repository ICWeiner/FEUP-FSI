# **Week #3**

## **Identification and Cataloging of a CVE**

### **Identification**
- **CVE-2019-18915**

- [Local privilege escalation](https://encyclopedia.kaspersky.com/glossary/privilege-escalation/) This exploits are used to escalate privileges from Admin to SYSTEM.


-  Affected Local systems:
   - Microsoft Windows 10
   - The exploit was only tested in **Microsoft Windows 10** and may work on older versions


### **Cataloging**

- HP was notified on the 7th of October, 2019

- HP PSRT product team "will address the issue in next release" on the   13th January, 2020

- Vulnerability was publicly disclosed on the 11th February.

- According to [NVD](https://nvd.nist.gov/vuln/detail/CVE-2019-18915) 7.8.


### **Exploit**

- The HP System Event service "HPMSGSVC.exe" will load an arbitrary EXE and execute it with SYSTEM integrity.
HPMSGSVC.exe runs a background process that delivers push notifications.

- The problem is that HP Message Service will load and execute any arbitrary executable named "Program.exe"
if found in the users c:\ drive.

- This results in arbitrary code execution persistence mechanism if an attacker can place an EXE in this location and can be used to escalate privileges from Admin to SYSTEM.


### **Atacks**

- If given physical access to a machine with this vulnerability, the attacker can place any sort of malicious program on the target machine, potentially gaining opening for further attacks remotely or getting access to any file on the system
