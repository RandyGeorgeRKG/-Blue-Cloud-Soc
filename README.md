
# Building a SOC + Honeynet in Azure (Live Traffic)
![Randy's Cyber Cloud Honeynet](https://github.com/user-attachments/assets/c1cd0c26-c1be-4b0a-b563-8f7f01030a1b)


## Introduction

Howdy! Thanks for checking out my SOC Project. The purpose of this project is to demonstrate to IT and business professionals the critical importance of implementing robust cybersecurity controls and protocols to counteract today's evolving threat landscape.
In this project, I created a honeynet within the Azure environment, where I ingested logs from multiple resources into Log Analytics. I then connected my Log Analytics workspace to Azure Sentinel to track incidents across the environment. This setup allowed me to generate attack maps and create incidents, offering real-time visibility into security events.
Initially, I deployed the honeynet with minimal security controls, leaving the environment vulnerable for 24 hours to capture baseline security metrics. This approach enabled me to generate logs that underscore the importance of well-configured firewalls, strong password policies, and other security measures. Afterward, I applied security controls to harden the SOC environment, significantly reducing the attack surface.
The metrics reflecting these improvements are listed below.

<li>AzureNetworkAnalytics_CL (Malicious flows allowed into our honeynet)</li>
<li>SecurityIncident (Incidents created by Sentinel)</li>
<li>SecurityEvent (Windows Event Logs)</li>
<li>SecurityAlert (Log Analytics alerts triggered)</li>
<li>Syslog (Linux Event Logs)</li>

## Architecture Before Hardening / Security Controls
![Public internet ](https://github.com/user-attachments/assets/0444a4a5-8b4b-43c3-9645-de4305d1215a)


## Architecture After Hardening / Security Controls
![Harden network ](https://github.com/user-attachments/assets/27fc337a-4f7d-4209-9374-b19148401d87)


The Mini honeypot lab consist of these components below 

<li>Microsoft Sentinel</li>
<li>Azure Storage Account</li>
<li>Azure Key Vault</li>
<li>Log Analytics Workspace</li>
<li>Virtual Machines (2 Windows, 1 Linux)</li>
<li>Network Security Group (NSG)</li>
<li>Virtual Network (VNet)</li>

<br>
</br>In the initial configuration, as represented by the "Before" diagram and metrics, all resources within the honeynet environment were exposed to the internet. Both the virtual machines and network security group firewalls were configured with open access, leaving them fully accessible from external sources. This exposure extended to all other resources within the environment, illustrating a highly vulnerable state prior to the implementation of security controls <br>
</br>

In the "After" diagram and metrics, I strengthened the environment by implementing controls aligned with NIST 800-53 standards. This hardening process involved blocking all malicious web traffic and securing the environment with robust firewall rules and strong password policies. These measures effectively enhanced the security posture of the environment, significantly reducing its exposure to potential threats.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/1qvswSX.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/G1YgZt6.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/ESr9Dlv.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-03-15 17:04:29
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 19470
| Syslog                   | 3028
| SecurityAlert            | 10
| SecurityIncident         | 348
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
