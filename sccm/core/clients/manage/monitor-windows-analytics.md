---
title: "Monitor clients with Windows Analytics"
titleSuffix: "Configuration Manager"
description: "Windows Analytics is a set of solutions that run on Operations Management Suite that allow you do draw valuable insights into the current state of your environment by leveraging the Windows telemetry data that is reported by devices in your environment."
ms.custom: na
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: 23
author: aczechowski
ms.author: aaroncz
manager: angrobe

---

# Use Windows Analytics with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) is a set of solutions that run on [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS). These solutions allow you to gain insight into the current state of your environment. Devices in your environment report Windows telemetry data and this data can be accessed and analyzed through solutions in the [Operations Management Suite web portal](https://mms.microsoft.com). By connecting [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) to Configuration Manager, you can directly access the data in the **Monitoring** node of the Configuration Manager console.

The Windows telemetry data used by Windows Analytics is not transferred directly to the Configuration Manager site server. Client computers send Windows telemetry data to the Windows telemetry service. This service then transfers the relevant data to Windows Analytics solutions hosted in one of your organization's OMS workspaces. Configuration Manager can then direct you to relevant data in the web portal with in-context links, or directly display data that is part of solutions that you have connected to Configuration Manager. You can also directly query the data from Operation Management Suite web portal.

>[!Important]
>[Configuration Manager diagnostic and usage data](../../plan-design/diagnostics/diagnostics-and-usage-data.md), which the Configuration Manager site server reports to Microsoft, is separate from Windows Analytics and Windows telemetry.

## Configure Clients to report data to Windows Analytics

For client devices to report data to Windows Analytics, you must configure devices with a Commercial ID key associated with the OMS workspace that hosts your Windows Analytics data. You also must configure devices to report telemetry at a telemetry level appropriate for the specific solutions that you want to use. 

### Configure Windows Analytics client settings
To configure Windows Analytics, in the Configuration Manager console choose **Administration** > **Client Settings**, double-click **Create Custom Device Client Settings**, and then check **Windows Analytics**.  

After navigating to the **Windows Analytics** settings tab, configure the following settings:
  -  **Commercial ID key**  
The commercial ID key maps information from devices you manage to the OMS workspace that hosts your organization's Windows Analytics data. If you have already configured a commercial ID key for use with Upgrade Readiness, use that ID. If you do not yet have a commercial ID key, see [Generate your commercial ID key]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Telemetry level for Windows 10 devices**   
For more information about each Windows 10 telemetry level, see [Configure Windows telemetry in your organization](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > With the 1710 update, you can set the Windows 10 telemetry data collection level to **Enhanced (Limited)**. This setting enables you to gain actionable insight about devices in your environment without devices reporting all of the data in the **Enhanced** telemetry level with Windows 10 version 1709 or later. The Enhanced (Limited) telemetry level includes metrics from the Basic level, as well as a subset of data collected from the Enhanced level relevant to Windows Analytics.


  -  **Opt in to commercial data collection on Windows 7, 8 and 8.1 devices**   
For more information, see [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965).

  -  **Configure Internet Explore data collection**  
On devices running Windows 8.1 or earlier, Internet Explorer data collection can allow Upgrade Readiness to detect web application incompatibilities that could prevent a smooth upgrade to Windows 10. Internet Explorer data collection can be enabled on a per internet zone basis. For more information about internet zones, see [About URL Security Zones](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## Use Upgrade Readiness to identify Windows 10 compatibility issues

Upgrade Readiness (formerly Upgrade Analytics) enables you to analyze device readiness and compatibility with Windows 10. This assessment allows for smoother upgrades. After connecting Configuration Manager to Upgrade Readiness, access this client upgrade compatibility data directly in the Configuration Manager console. Then target devices for upgrade or remediation from the device list.

For more information and details on how to configure and connect to Upgrade Readiness, see [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## Use Windows Analytics to identify gaps in Windows Information Protection Policies

Windows 10 version 1703 and later devices configured with a [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) policy report telemetry on applications that access corporate data in your environment but the WIP policy application rules do not include. Users may need these applications to stay productive, but WIP blocks the users' access. Knowledge that users are accessing corporate data is useful in the maintenance of your Windows Information Protection policies in Configuration Manager. 

Access this Windows Information Protection data using this [Operations Management Suite query](https://go.microsoft.com/fwlink/?linkid=849952).