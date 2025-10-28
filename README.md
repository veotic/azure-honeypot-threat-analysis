# azure-honeypot-threat-analysis
**Made by: Angelo Monge**

### Lab Project Documentation

Objective:
Design and deploy a cloud-based honeypot in Microsoft Azure, effectively simulating a real-world enterprise endpoint, capturing unauthorized access/login attempts, and analyzing attacker behavior by using a centralized log analytics workspace and data visualization in Microsoft Sentinel, essentially their SIEM (Security Information Event Management). This project will demonstrate practical knowledge of cloud security architecture, cyber threat analysis, and SIEM integration. 

*(Image below is the lab map)*
https://github.com/veotic/azure-honeypot-threat-analysis/blob/114fe0a6e0102e328b5284dfa7ad967f1edea946/proj_img_1.png

**Project Overview**
- Platform: Microsoft Azure
- OS: Windows 10 Enterprise 22H2 x64 Gen2
- Host Name: CORP-BACKUP-EAST-1
- Tools & Services used:
  - Azure VM
  - Network Security Groups (NSG)
  - Log Analytics Workspace (LAW)
  - Azure Monitor Agent (AMA)
  - Microsoft Sentinel (SIEM)
  - Kusto Query Language (KQL)
  - GeoIP Watchlist

**1. ) Configuration Process**
- Created a new Azure Resource Group and VNet
- Deployed a VM using Windows 10 Enterprise 22H2 x64 Gen2, named CORP-BACKUP-EAST-1
- Configured a custom Network Security Group that simulates vulnerable inbound access by allowing any malicious traffic
- Disabled Windows Defender Firewall to emulate an unprotected endpoint

**2.) Attack Simulation and Data Capture**
- Exposed the VM entirely to the internet and observed any brute-force attempts
- The image below shows that within the first two hours, the Windows recorded that approximately 19,000 brute forces occurred
- Over the next several days, this will be go up to 50,000+

*(Turning off windows firewall)*
https://github.com/veotic/azure-honeypot-threat-analysis/blob/114fe0a6e0102e328b5284dfa7ad967f1edea946/proj_img_2.png

**3.) SIEM Integration**
- Created a Log Analytics Workspace (LAW) to connect it to the VM using the Azure Monitor Agent Security Events connector
- Verified the ingestion of Security Event logs and confirm any Event ID 4625 (failed login) entires
- Integrated Microsoft Sentinel with LAW to allow any real-time log analysis

**4.) Log Analysis**
- With the image below, it shows the use of KQL to query through the produced dataset
- Imported GeoIP watchlist (geoip-summarized.csv) which had 54,000 rows of IP addresses to identify where the hackers are from
- Utilized KQL queries to see any meaningful correlations

*(LAW after using the Data Collection Rule and we use KQL to query specific details)*
https://github.com/veotic/azure-honeypot-threat-analysis/blob/114fe0a6e0102e328b5284dfa7ad967f1edea946/proj_img_3.png

**5.) Visualization**
- Created a custom Attack Map workbook in Microsoft Sentinel using JSON configurations and KQL
- Mapped the specific locations of login attempts globally to visualize real-time attacker origin points

*(These are the results after a few minutes)*
[https://github.com/veotic/azure-honeypot-threat-analysis/blob/114fe0a6e0102e328b5284dfa7ad967f1edea946/proj_img_4.png](https://github.com/veotic/azure-honeypot-threat-analysis/blob/main/proj_img_4.png?raw=true)

### Conclusion
In the following days I would receive 50k+ attacks. In my observation, it seems that most of these attacks are directed from the Netherlands.








  

