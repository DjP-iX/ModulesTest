---
title: "Storage"
description: "Tutorials for configuring the various features contained within the Storage area of the TrueNAS SCALE web interface."
geekdocCollapseSection: true
weight: 5
aliases:
 - /scale/scaletutorials/storage/pools/
related: false
---

The SCALE Storage section has controls for pool, snapshot, and disk management.
The storage section also has options for datasets, zvols, and permissions.

## Storage Overview

![StorageSCALE](/images/SCALE/Storage/StorageDashboardWithPool.png "TrueNAS SCALE Storage")

The **Import Pool** button lets users reconnect pools exported/disconnected from the current system or created on another system.
This also reconnects pools after users reinstall or upgrade the TrueNAS system.

The **Disks** button lets users manage, wipe, and import storage disks that TrueNAS will use for ZFS data storage.

The **Create Pool** button creates ZFS data storage “pools” from physical disks to efficiently store and protect data.

The Storage screen displays all the pools that users have created on the system.
Statistics and status are shown for each pool, along with buttons to manage the different elements of the pool.

The articles in this section offer specific guidance for the different storage management options.

## Storage Articles

{{< children depth="2" description="true" >}}
