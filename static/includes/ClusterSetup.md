&NewLine;


### TrueNAS SCALE Systems

Follow this procedure for each TrueNAS SCALE system you want to connect to TrueCommand and use in the cluster.

1. Log in to the SCALE UI and go to **Storage**.
   Ensure a storage pool is available for use in the cluster.
   If not, click **Create Pool** and make a new pool using any available disks.

2. Go to **Network** and look at the **Interfaces** card.

   * Ensure two interfaces are available.
     Note which is the primary interface that allows SCALE UI access and access between SCALE systems, TrueCommand, and Active Directory environments.
     Having two interfaces allows connecting the SCALE systems to Active Directory and using TrueCommand to create and manage the cluster.

   * Ensure the second interface has a static IP address on a different network/subnet that connects all the SCALE systems.
     This interface securely handles all the data-sharing traffic between the clustered systems.

   * Ensure the network has an IP address available.
     TrueCommand creates a virtual IP address (VIP) that allows access to the cluster.
     All cluster nodes (systems) use the same VIP.

   {{< hint type=important >}}
   TrueNAS automatically adds entries to AD DNS for CTDB public IP addresses.
   Administrators should verify the addresses before joining AD to prevent configuration errors.
   {{< /hint >}}

3. Go to **Shares** and look at the **Windows (SMB) Shares** section.
   Take steps to ensure that disabling any critical shares is not disruptive.

Repeat this procedure for each SCALE system you want to add to the cluster.

### Microsoft Active Directory

1. Verify that the Active Directory (AD) environment to pair with the cluster is available and administratively accessible on the same network as the TrueCommand and TrueNAS SCALE systems.

2. Log in to the Windows Server system and open the **Server Manager**.
   Click **Tools** > **DNS** to open the **DNS Manager**.

   {{< trueimage src="/images/TrueCommand/WindowsServerManagerToolsDNS.png" alt="Opening the DNS Manager" id="Opening the DNS Manager" >}}

3. Expand **Reverse Lookup Zones** on the left side menu, then select the **Active Directory-Integrated Primary** zone to use for the cluster.

   {{< trueimage src="/images/TrueCommand/WindowsServerDNSManagerReverseLookupZones.png" alt="Finding the Reverse Lookup Zones" id="Finding the Reverse Lookup Zones" >}}

   If no zone exists, see the Microsoft guide for [creating DNS Zones](https://docs.microsoft.com/en-us/learn/modules/implement-windows-server-dns/3-work-dns-zones-records).

4. Click **Action** > **New Pointer (PTR...)** and configure a **New Resource Record**. Enter the SCALE system IP address and host name, then click **OK**.

   {{< trueimage src="/images/TrueCommand/WindowsServerDNSManagerReverseLookupZonesPointersAdd.png" alt="Add Windows Server DNS Manager Reverse Lookup Zones Pointers" id="Add Windows Server DNS Manager Reverse Lookup Zones Pointers" >}}

Repeat this process for each system intended for clustering.
The new records appear inside the zone as they save.

{{< trueimage src="/images/TrueCommand/WindowsServerDNSManagerReverseLookupZonesPointers.png" alt="Pointers added to the Zone" id="Pointers added to the Zone" >}}

### TrueCommand Container

If not already complete:

1. [Deploy TrueCommand 2.2 or later in a Docker container]({{< relref "/TrueCommand/TCGettingStarted/Install/installtcdocker.md" >}}).
   The system used for the TrueCommand container cannot be any of the TrueNAS SCALE systems intended for the cluster.

2. Enter the TrueCommand IP address in a browser, and create the first user.
   Log in with these user credentials to see the **Dashboard**.

3. Click **New System** and add the credentials for the first SCALE system.
   Use the SCALE root account password.
   When ready, click **ADD AND CONTINUE** and repeat the process for each SCALE system intended for the cluster.
   When complete, each SCALE system has a card on the TrueCommand **Dashboard** that displays system statistics.

{{< hint type=tip >}}
We recommend you back up the SCALE system configuration before creating the cluster.
Backups allow users to quickly restore the system configuration to the initial working state if something goes wrong.

In the TrueCommand **Dashboard**, click on the name of a connected system to open a detailed view of that system.
Click **Config Backups** and **CREATE BACKUP** to store the SCALE configuration file with TrueCommand.
{{< /hint >}}
