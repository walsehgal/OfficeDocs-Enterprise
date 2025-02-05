---
title: "Office 365 Network Insights (preview)"
ms.author: kvice
author: kelleyvice-msft
manager: laurawi
ms.date: 03/20/2020
audience: Admin
ms.topic: conceptual
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MET150
ms.collection:
- Ent_O365
- Strat_O365_Enterprise
description: "Office 365 Network Insights (preview)"
---

# Office 365 Network Insights (preview)

**Network insights** are live performance metrics collected from your Office 365 tenant, and available to view only by administrative users in your tenant. Insights are displayed in the Microsoft 365 Admin Center at <https://portal.microsoft.com/adminportal/home#/networkperformance>.

Insights are intended to help in designing network perimeters for your office locations. Each insight provides live details about the performance characteristics for a specific common issue for each geographic location where users are accessing your tenant.

There are five specific network insights that may be shown for each office location:

- [Backhauled network egress](#backhauled-network-egress)
- [Better performance detected for customers near you](#better-performance-detected-for-customers-near-you)
- [Use of a non-optimal Exchange Online service front door](#use-of-a-non-optimal-exchange-online-service-front-door)
- [Use of a non-optimal SharePoint Online service front door](#use-of-a-non-optimal-sharepoint-online-service-front-door)
- [Low download speed from SharePoint front door](#low-download-speed-from-sharepoint-front-door)

>[!IMPORTANT]
>Network insights, performance recommendations and assessments in the Microsoft 365 Admin Center is currently in preview status, and is only available for Office 365 tenants that have been enrolled in the feature preview program.

## Backhauled network egress

This insight will be displayed if the network insights service detects that the distance from a given user location to the network egress is greater than 500 miles (800 kilometers), indicating that Office 365 traffic is being backhauled to a common Internet edge device or proxy.

This insight is abbreviated as "Egress" in some summary views.

![Backhauled network egress](Media/m365-mac-perf/m365-mac-perf-insights-detail-backhauled.png)

### What does this mean?

This identifies that the distance between the office location and the network egress is more than 500 miles (800 kilometers). The office location is identified by an obfuscated client machine location and the network egress location is identified by using reverse IP Address to location databases. The office location may be inaccurate if Windows Location Services is disabled on machines. The network egress location may be inaccurate if the reverse IP Address database information is inaccurate.

Details for this insight include the office location, estimated percentage of total tenant user at the location, the current network egress location, relevance of the egress location, the distance between the location and the current egress point, the date the condition was first detected, and the date the condition was resolved.

### What should I do?

For this insight, we would recommend network egress closer to the office location so that connectivity can route optimally to Microsoft's global network and to the nearest Office 365 service front door. Having close network egress to users office locations also allows for improved performance in the future as Microsoft expands both network points of presence and Office 365 service front doors in the future.

For more information about how to resolve this issue, see [Egress network connections locally](office-365-network-connectivity-principles.md#egress-network-connections-locally) in [Office 365 Network Connectivity Principles](office-365-network-connectivity-principles.md).

## Better performance detected for customers near you

This insight will be displayed if the network insights service detects that a significant number of customers in your metro area have better performance than users in your organization at this office location.

This insight is abbreviated as "Peers" in some summary views.

![Relative network performance](Media/m365-mac-perf/m365-mac-perf-insights-detail-cust-near-you.png)

### What does this mean?

This insight examines the aggregate performance of Office 365 customers in the same city as this office location. This insight is displayed if the average latency of your users is 10% greater than the average latency of neighboring tenants.

### What should I do?

There could be many reasons for this condition, including latency in your corporate network or ISP, bottlenecks, or architecture design issues. Examine the latency between each hop in the route between your office network and the current Office 365 front door. For more information, see [Office 365 Network Connectivity Principles](office-365-network-connectivity-principles.md).

## Use of a non-optimal Exchange Online service front door

This insight will be displayed if the network insights service detects that users in a specific location are not connecting to an optimal Exchange Online service front door.

This insight is abbreviated as "Routing" in some summary views.

![Non-optimal front door](Media/m365-mac-perf/m365-mac-perf-insights-detail-front-door-exo.png)

### What does this mean?

We list Exchange Online service front doors which are suitable for use from the office location city with good performance. If the current test shows use of an Exchange Online service front door not on this list, then we call out this recommendation.

### What should I do?

Use of a non-optimal Exchange Online service front door could be caused by network backhaul before the corporate network egress in which case we recommend local and direct network egress. It could also be caused by use of a remote DNS Recursive Resolver server in which case we recommend aligning the DNS Recursive Resolver server with the network egress.

## Use of a non-optimal SharePoint Online service front door

This insight will be displayed if the network insights service detects that users in a specific location are not connecting to the closest SharePoint Online service front door.

This insight is abbreviated as "Afd" in some summary views.

![Non-optimal front door](Media/m365-mac-perf/m365-mac-perf-insights-detail-front-door-spo.png)

### What does this mean?

We identify the SharePoint Online service front door that the test client is connecting to. Then for the office location city we compare that to the expected SharePoint Online service front door for that city. If it doesn't match, then we make this recommendation.

### What should I do?

Use of a non-optimal SharePoint Online service front door could be caused by network backhaul before the corporate network egress in which case we recommend local and direct network egress. It could also be caused by use of a remote DNS Recursive Resolver server in which case we recommend aligning the DNS Recursive Resolver server with the network egress.

## Low download speed from SharePoint front door

This insight will be displayed if the network insights service detects that bandwidth between the specific office location and SharePoint Online is less than 1 MBps.

This insight is abbreviated as "Throughput" in some summary views.

### What does this mean?

The download speed that a user can get from SharePoint Online and OneDrive for Business service front doors is measured in megabytes per second (MBps). If this value is less than 1 MBps then we provide this insight.

### What should I do?

To improve download speeds, bandwidth may need to be increased. Alternatively, there may be network congestion between user machines at the office location and the SharePoint Online service front door. This is sometimes called congestive loss and it restricts the download speed available to users even if sufficient bandwidth is available.

## China user optimal network egress

This insight will be displayed if your organization has users in China connecting to your Office 365 tenant in other geographic locations. 

### What does this mean?

If your organization has private WAN connectivity, we recommend configuring a network WAN circuit from your office locations in China that has network egress to the Internet in any of the following locations:

- Hong Kong
- Japan
- Taiwan
- South Korea
- Singapore
- Malaysia

Internet egress further away from users than these locations will reduce performance, and egress in China may cause high latency and connectivity issues due to cross-border congestion.

### What should I do?

For more information about how to mitigate performance issues related to this insight, see [Office 365 global tenant performance optimization for China users](https://docs.microsoft.com/office365/enterprise/office-365-networking-china).

## Related topics

[Network performance recommendations in the Microsoft 365 Admin Center (preview)](office-365-network-mac-perf-overview.md)

[Office 365 network assessment (preview)](office-365-network-mac-perf-score.md)

[Office 365 Network Onboarding Tool in the M365 Admin Center (preview)](office-365-network-mac-perf-onboarding-tool.md)
