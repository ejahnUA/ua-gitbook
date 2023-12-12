# Rental Storage

## Overview <a href="#rentalstorage-overview" id="rentalstorage-overview"></a>

{% hint style="info" %}
* <mark style="color:red;">This service is not intended for controlled or regulated research data, such as HIPAA/ePHI, ITAR, or CUI</mark>
* <mark style="color:red;">**Rental storage is not mounted on HPC compute or login nodes.**</mark>
{% endhint %}

The storage we offer is configured with consideration given to the direct relationship between capacity, performance and cost. We offer a rental storage solution that has less performance and so is affordable for researchers to rent. This storage array is located in the Research Data Center and is mounted on our data transfer nodes (filexfer.hpc.arizona.edu) so that makes it more accessible than most other options.

If you have any questions, contact our consultants using [ServiceNow](https://uarizona.service-now.com/sp?id=sc\_cat\_item\&sys\_id=2983102adbd23c109627d90d689619c6\&sysparm\_category=84d3d1acdbc8f4109627d90d6896191f)

***

## Pricing <a href="#rentalstorage-pricing" id="rentalstorage-pricing"></a>

### Billing <a href="#rentalstorage-billing" id="rentalstorage-billing"></a>

Researchers must provide a KFS account for this service. Charges will be applied at the end of the academic year (June).

### Cost Per Year <a href="#rentalstorage-costperyear" id="rentalstorage-costperyear"></a>

The effective yearly cost to researchers is $47.35 per TB.&#x20;

The first-year rate is $94.50 per TB, and RII will provide matching funds for first-year allocations to make the actual first-year cost to researchers $47.35. These matching funds will be applied automatically, so in practice you will only see the $47.35 rate. The ongoing rate after year one is $47.35 per TB per year.

### Size Modifications <a href="#rentalstorage-sizemodifications" id="rentalstorage-sizemodifications"></a>

If the size of your allocation is modified, you will be billed for the maximum amount of space reserved during that fiscal year.

***

## Access and Transfers <a href="#rentalstorage-accessandtransfers" id="rentalstorage-accessandtransfers"></a>

#### Data Location <a href="#rentalstorage-datalocation" id="rentalstorage-datalocation"></a>

Your rental space will be on a storage array in our data center. Your space will be mounted on our data transfer nodes (hostname: **filexfer.hpc.arizona.edu**) as:

```bash
/rental/pi_netid
```

where `pi_netid` is the NetID of the faculty member who requested the allocation. **Rental storage is not mounted on HPC compute or login nodes**.

#### Data Transfers <a href="#rentalstorage-datatransfers" id="rentalstorage-datatransfers"></a>

You can use [Globus](https://uarizona.atlassian.net/wiki/display/UAHPC/Globus?src=contextnavpagetreemode), sftp, or scp to move data that is external to the data center.

You may also ssh into filexfer.hpc.arizona.edu to use mv or cp to transfer files between your HPC directories (/home, /groups, or /xdisk) and /rental. For large copies done using this method, we recommend using a `screen` session to prevent timeouts. For example:

```bash
[netid@home ~]$ ssh netid@filexfer.hpc.arizona.edu
Authorized uses only. All activity may be monitored and reported.
Last login: Fri Sep 15 10:53:27 2023
[netid@sdmz-dtn-3 ~]$ cd /rental/pi/netid/example
[netid@sdmz-dtn-3 example]$ screen
[netid@sdmz-dtn-3 example]$ cp -r /xdisk/pi/CONTAINERS/ $PWD/CONTAINERS
[netid@sdmz-dtn-3 example]$ ls
CONTAINERS
[netid@sdmz-dtn-3 example]$ exit # exits screen session
[netid@sdmz-dtn-3 example]$ exit # exits filexfer node
logout
Come again soon!
Connection to filexfer.hpc.arizona.edu closed.
[netid@home ~]$
```

***

## Requesting Rental Storage <a href="#rentalstorage-requestingrentalstorage" id="rentalstorage-requestingrentalstorage"></a>

{% hint style="info" %}
Allocations up to 20TB in size can be requested through the user portal. For allocations larger than 20TB, [contact our consulting team for help](https://uarizona.service-now.com/sp?id=sc\_cat\_item\&sys\_id=2983102adbd23c109627d90d689619c6\&sysparm\_category=84d3d1acdbc8f4109627d90d6896191f).
{% endhint %}

{% hint style="info" %}
It can take a few days to process the request is it has to route through the Financial Services Office (FSO). You will receive an email confirmation once it is complete.
{% endhint %}

1. PIs or [Storage Delegates](https://uarizona.atlassian.net/wiki/display/UAHPC/Storage#xdisk-delegate) can request rental storage on behalf of their group. To do so, navigate to [https://portal.hpc.arizona.edu](https://portal.hpc.arizona.edu/) in your browser, then choose the Storage tab

<figure><img src="../../.gitbook/assets/Screenshot 2023-06-21 at 11.19.51 AM.png" alt=""><figcaption></figcaption></figure>

2. Select **Submit Rental Storage Request** under the **Rental Storage** heading and fill out the form.
3. Once your space has been created, you will receive an email notification. You can access it on a filexfer node (hostname: filexfer.hpc.arizona.edu) under /rental/\<PI>. You can make transfers to your active HPC storage (/xdisk, /groups, or /home) either by ssh-ing into the filexfer node and using a mv or cp, by running an scp, sftp using the filexfer hostname, or by [using the Globus endpoint](https://uarizona.atlassian.net/wiki/display/UAHPC/Transferring+Data#Globus-rental-endpoint) **UA Rental Storage Filesystem**.

***

## Resizing Your Allocation

{% hint style="info" %}
Resizing allocations up to 20TB can be done the user portal. For allocations larger than 20TB, [contact our consulting team for help](https://uarizona.service-now.com/sp?id=sc\_cat\_item\&sys\_id=2983102adbd23c109627d90d689619c6\&sysparm\_category=84d3d1acdbc8f4109627d90d6896191f).
{% endhint %}

Your rental allocation can be resized [through the user portal ](https://portal.hpc.arizona.edu/portal/)by navigating to the **Storage** tab and selecting **Modify Rental Quota** under the **Rental Storage** heading.

<figure><img src="../../.gitbook/assets/Screen Shot 2023-01-18 at 9.09.10 AM.png" alt=""><figcaption></figcaption></figure>

***

## Checking Your Usage <a href="#rentalstorage-checkingyourusage" id="rentalstorage-checkingyourusage"></a>

You can check your allocation's size and current usage either through the user portal or on the command line.

<details>

<summary>User Portal (PIs Only)</summary>

In the [user portal](https://portal.hpc.arizona.edu/portal/), navigate to the **Storage** tab and select **Check Rental Quota** from under the **Rental Storage** tab



</details>

asd
