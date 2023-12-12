# Allocation and Limits

## Storage Allocations

See our [Storage page](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989618/Storage) for:

* More detailed information on storage allocations and policies
* Information on [how to use xdisk](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989618/Storage#Storage-UsingXdisk)
* Information on using [UArizona Google Drive with HPC](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989618/Storage#Storage-Tier2)

When you obtain a new HPC account, you will be provided with storage.  The shared storage (/home, /groups, /xdisk) is accessible from any of the three production clusters: Puma, Ocelote and ElGato. The temporary (/tmp) space is unique to each compute node.

| Persistence | Location        | Allocation                                                                 | Usage                                                                                                                  |
| ----------- | --------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Permanent   | /home/uxx/netid | 50GB                                                                       | Individual allocations specific to each user.                                                                          |
|             | /groups/PI      | 500GB                                                                      | Allocated as a communal space to each PI and their group members.                                                      |
| Temporary   | /xdisk/PI       | up to 20TB                                                                 | Requested at the PI level. Available for up to 150 days with one 150 day extension possible for a total of 300 days.   |
|             | /tmp            | \~1400GB NVMe (Puma) \~840GB spinning (Ocelote) \~840GB spinning (El Gato) | Local storage specific to each compute node. Usable as a scratch space for compute jobs. Not accessible once jobs end. |

***

## CPU Time Allocations <a href="#allocationandlimits-cputimeallocations" id="allocationandlimits-cputimeallocations"></a>

### Overview <a href="#allocationandlimits-overview" id="allocationandlimits-overview"></a>

All University of Arizona Principal Investigators (PIs; aka Faculty) that register for access to the UA High Performance Computing (HPC) receive these free allocations on the HPC machines which is shared among all members of their team. Currently all PIs receive:

| HPC Cluster | Standard Monthly Allocation per PI | Windfall                        |
| ----------- | ---------------------------------- | ------------------------------- |
| Puma        | 100,000 CPU Hours per month        | Unlimited but can be pre-empted |
| Ocelote     | 70,000 CPU Hours per month         | Unlimited but can be pre-empted |
| El Gato     | 7,000 CPU Hours per month          | Unlimited but can be pre-empted |

### Best practices <a href="#allocationandlimits-bestpractices" id="allocationandlimits-bestpractices"></a>

1. Use your standard allocation first! The standard allocation is guaranteed time on the HPC. It refreshes monthly and does not accrue (if a month's allocation isn't used it is lost).
2. Use the windfall queue when your standard allocation is exhausted. Windfall provides unlimited CPU-hours, but jobs in this queue can be stopped and restarted (pre-empted) by standard jobs.
3. If your group consistently needs more time than the free allocations, consider the [HPC buy-in program](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75990323/Buy-In).
4. Last resort for tight deadlines: PIs can request a special project allocation once per year ([https://portal.hpc.arizona.edu/portal/](https://portal.hpc.arizona.edu/portal/); under the Support tab). Requesting a special project will provide qualified hours which are effectively the same as standard hours.
5. For several reasons we do not offer checkpointing.  It may be desirable to have this capability in your code.

### How Allocations are Charged <a href="#allocationandlimits-howallocationsarecharged" id="allocationandlimits-howallocationsarecharged"></a>

The number of CPU hours a job consumes is determined by the number of CPUs it is allocated multiplied by its requested walltime. When a job is submitted, the CPU hours it requires are automatically deducted from the account. If the job ends early, the unused hours are automatically refunded.

For example, a job requesting 50 CPUs for 10 hours will be charged 500 CPU hours. When the job is submitted, all 500 CPU hours are deducted from the user's account, however, if the job only runs for 5 hours and then completes, the unused 250 hours would be refunded.

This accounting is the same regardless of which type of node you request. Standard, GPU, and high memory nodes are all charged using the same model and use the same allocation pool. If you find you are being charged for more CPUs that you are specifying in your submission script, it may be [an issue with your job's memory request](https://uarizona.atlassian.net/wiki/display/UAHPC/Running+Jobs+with+SLURM#RunningJobswithSLURM-TotalJobMemoryvs.CPUCount).

Allocations are refreshed on the first day of each month. Unused hours from the previous month do not roll over.

### How to Use Your Allocation <a href="#allocationandlimits-howtouseyourallocation" id="allocationandlimits-howtouseyourallocation"></a>

To use your allocation, you will include your account and partition information as a SLURM directive in your batch script. The formatting for this can be found in our [R](https://public.confluence.arizona.edu/display/UAHPC/Running+Jobs+with+SLURM#RunningJobswithSLURM-JobPartitionRequestsJobPartitionRequests)[unning Jobs with SLURM documentation](https://uarizona.atlassian.net/wiki/display/UAHPC/Running+Jobs+with+SLURM#RunningJobswithSLURM-JobPartitionRequestsJobPartitionRequests).

### How to Find Your Remaining Allocation <a href="#allocationandlimits-howtofindyourremainingallocation" id="allocationandlimits-howtofindyourremainingallocation"></a>

To view your remaining allocation, use the command **`va`** in a terminal. For example:

```bash
(elgato) [user@gpu5 ~]$ va
Windfall: Unlimited
 
PI: parent_974 Total time: 7000:00:00
    Total used*: 1306:39:00
    Total encumbered: 92:49:00
    Total remaining: 5600:32:00
    Group: group1 Time used: 862:08:00 Time encumbered: 92:49:00
    Group: group2 Time used: 0:00:00 Time encumbered: 0:00:00
 
*Usage includes all subgroups, some of which may not be displayed here
```

| Field               | Description                                                                                                                                                                                                                                                    |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Total used:`       | The total number of CPU hours used by the group for the current month. This includes [all the subgroups that are managed by your PI](https://uarizona.atlassian.net/wiki/display/UAHPC/Research+and+Class+Groups), not just the subgroups you are a member of. |
| `Total time:`       | The total number of CPU hours available on the cluster each month                                                                                                                                                                                              |
| `Total remaining:`  | The total number of CPU hours that are unencumbered/unused                                                                                                                                                                                                     |
| `Total encumbered:` | The total number of CPU hours that are reserved by active (pending/running) jobs.                                                                                                                                                                              |
| `Group:`            | Hours used broken down by the groups your PI manages. Only usage for the groups you are a member of will be shown.                                                                                                                                             |

### SLURM Batch Queues <a href="#allocationandlimits-slurmbatchqueues" id="allocationandlimits-slurmbatchqueues"></a>

The batch queues, also known as partitions, on the different systems are the following:

| Queue          | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| standard       | Used to consume the monthly allocation of hours provided to each group |
| windfall       | Used when standard is depleted but subject to preemption               |
| high\_priority | Used by 'buy-in' users for purchased nodes                             |
| qualified      | Used by groups who have a temporary special project allocation         |

### Job Limits <a href="#allocationandlimits-joblimits" id="allocationandlimits-joblimits"></a>

To check group, user, and job limitations on resource usage, use the command **`job-limits $YOUR_GROUP`** in the terminal.

### Special Allocations <a href="#allocationandlimits-specialallocations" id="allocationandlimits-specialallocations"></a>

Sometimes you may need an extra allocation for a conference deadline or paper submission.  Or something else.  We can offer a temporary allocation according to the guidelines here: [Special Projects](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75990534/Special+Projects)

