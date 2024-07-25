# Building a Security Operations Center + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I constructed a small-scale honeynet within Azure, gathering log data from diverse sources into a Log Analytics workspace. This data was utilized by Microsoft Sentinel to generate attack maps, activate alerts, and initiate incident responses. I conducted security metric assessments within the vulnerable environment over a 24-hour period, implemented security measures to fortify the environment, and subsequently conducted another 24-hour metric assessment. Below, I present the outcomes of these assessments:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The mini honeynet architecture deployed in Azure includes the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

Before assessing the metrics, all resources were set up to be accessible from the internet. The Virtual Machines had their Network Security Groups and built-in firewalls configured with open rules, allowing unrestricted access. Furthermore, all other resources were deployed with public endpoints that were visible and accessible directly from the internet, eliminating the need for private endpoints.

Following the initial metrics assessment, Network Security Groups were enhanced by restricting all traffic except for connections originating from my admin workstation. Additionally, all other resources were protected by their built-in firewalls and secured using Private Endpoints.

## Attack Maps Before Hardening / Security Controls

![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/y9wtirP.jpg)<br>

![Linux Syslog Auth Failures](https://i.imgur.com/RfW9xYQ.jpg)<br>

![Windows RDP/SMB Auth Failures](https://i.imgur.com/IhcUdkA.jpg)<br>

## Metrics Before Hardening / Security Controls

Below is the table displaying the metrics we recorded within our insecure environment over a 24-hour period:
Start Time 2024-07-18 02:38:43
Stop Time 2023-07-19 02:38:43

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 25767
| Syslog                   | 7166
| SecurityAlert            | 9
| SecurityIncident         | 180
| AzureNetworkAnalytics_CL | 1633

## Attack Maps Before Hardening / Security Controls

```None of the map queries yielded results because there were no instances of malicious activity during the 24-hour period after implementing security measures.```

## Metrics After Hardening / Security Controls

The table below presents the metrics we monitored in our environment for an additional 24 hours after implementing security controls:
Start Time 2024-07-21 22:28:09
Stop Time	2024-07-22 22:28:09

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8928
| Syslog                   | 10
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this Azure project, I created a miniature honeynet environment where various log sources were consolidated into a Log Analytics workspace. Using Microsoft Sentinel, I configured automated responses to detect and manage security incidents based on these logs. Initially, I gathered metrics from the vulnerable setup before implementing stringent security protocols. After the controls were applied, I conducted another round of metrics analysis, revealing a marked reduction in security events and incidents. This outcome underscored the effectiveness of the security enhancements in safeguarding the environment.

It's important to note that under conditions of multiple users within the network, we might have observed a greater volume of security events and alerts during the initial 24-hour post-implementation period of these security measures.
