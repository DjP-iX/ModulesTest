---
title: "Developer’s Notes"
description: "Comments from the TrueCommand development team."
weight: 15
---

{{< toc >}}

{{< expand "Recent Updates" "v" >}}
> 04/09/2021 - ISCSI creation process completed. Cluster creation routines finished up and streamlined.

> 03/17/2021 - Large update to Cluster creation/management. Requires latest TrueNAS SCALE nightlies to work properly (API's just changed on their end).

> 02/25/2021 - Initial nightly image release for TrueCommand 2.0
{{< /expand >}}

## Nightly Docker Images

Nightly images for TrueCommand are built every 24 hours.
These images are automatically pushed to the “nightly” tag on DockerHub if they pass the automated QA testing procedure.

Download information:

* [DockerHub](https://hub.docker.com/r/ixsystems/truecommand)
* [Example in Documentation]({{< relref "/TCGettingStarted/Install/_index.md" >}}), replace “latest” with “nightly” in the docker pull commands.

### Current Status

The nightly images are always considered a “work-in-progress” toward the next release of TrueCommand.
They should be suitable for adventurous users and developers who are not afraid of diagnosing issues and opening up bug reports with the TrueCommand developers.

Ticket Tracker: [Jira](https://ixsystems.atlassian.net/projects/TC)

#### Summary of changes in version 2.0

*  Version 2.0 is a complete rewrite of the middleware and database used in TrueCommand, as well as a complete re-integration with the TrueNAS middleware for statistics and analysis. Early tests indicate a sharp improvement in the performance of the system (details below), and some of the new features that this enables in TrueCommand 2.0 are:
NAS metrics and state updates in realtime - no more 30s delay!
* The “Storage Explorer” interface lets you inspect the datasets and files on your storage pools, while also giving you easy access to creating and managing snapshots, shares, zvols, and more.
* The “ISCSI Manager” is a new dashboard system that lets you view and create ISCSI volumes in bulk across your entire NAS fleet.
* “Cluster Volumes” is a new dashboard system that lets you view and create clustered datasets which span  across multiple TrueNAS SCALE systems in your fleet.
* Marked performance improvements:
 * Docker image ~50% smaller
 * Network bandwidth usage ~40% less
 * CPU usage ~5% lower
 * Database growth rate \~99% lower

Table of features and current status (Timestamp references when the item status was last updated):

{{< truetable >}}
| Feature | Status | Timestamp | Description |
|:---:|:---:|:---:|:---:|
|Users | **OK** | 02/26/2021 | Create and manage users and user permissions|
|Teams| **OK** | 02/26/2021 | Create and manage teams of users and permissions|
|Systems| **OK** | 02/26/2021 | Register NAS’s and maintain connections/status info |
|Alert Rules|**OK**|02/26/2021 | Create and manage custom alert rules |
|Alert Notices| **OK** | 02/26/2021|Rolling feed of alerts that have been triggered with comment and resolution systems|
|Alert Services| **OK** | 06/07/2021| Submission of new alert notices to external notification systems (email/pagerduty)|
|Reports|**OK**|02/26/2021| Historical charts of system information |
|Logs|**OK**|02/26/2021| Security logs of changes from users |
|System Administration|**OK**|02/26/2021| Configuration of TrueCommand system (SSL certificates, licensing, AD/LDAP, etc)|
|Dashboard|**OK**|06/07/2021|Top-level look at NAS state and information|
|NAS Explorer|**OK**|06/07/2021| Detailed inspection/management of storage on individual NAS’s|
|Cluster Volumes|**OK**|06/07/2021|Create and manage clusters of TrueNAS SCALE systems (glusterfs)|
|ISCSI Manager|**OK**|06/07/2021|Create and manage ISCSI volumes in bulk|
{{< /truetable >}}