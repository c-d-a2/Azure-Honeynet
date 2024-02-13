## Azure-Honeynet
Honeynet built using the azure cloud platform.


## Introduction

In this project, I created a mini honeynet in Azure. I ingested log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, applied some security controls (NIST 800-53) to harden the environment, measured metrics for another 24 hours, then showed the results below. The metrics that are displayed are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 12/13/2023 19:04:29
Stop Time 12/14/2023 19:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 20494
| Syslog                   | 8099
| SecurityAlert            | 4
| SecurityIncident         | 158
| AzureNetworkAnalytics_CL | 3818

![Alt Text](./before_controls/linux-ssh-fail.png)
![Alt Text](./before_controls/nsg-mal.png)
![Alt Text](./before_controls/winrdp-fail.png)


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 12/15/2023 14:04:29
Stop Time	12/16/2023 14:04:29
I had no results from my the maps because there were no metrics to plot on the map  which validates the effectiveness of security controls and highlights the danger of leaving your devices wide open on the internet without the proper controls. 
| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 0
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0
