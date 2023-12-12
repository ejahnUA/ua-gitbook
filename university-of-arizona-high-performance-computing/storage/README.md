# Storage

## **Where Should I Store My Data?** <a href="#storage-whereshouldistoremydata" id="storage-whereshouldistoremydata"></a>

1. Data undergoing active analyses should be stored in HPC's local [High Performance Storage](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75990091/HPC+High+Performance+Storage).
2. Large amounts of data not requiring immediate access from our HPC compute nodes can be stored at reasonable rates on our [Rental Storage](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989740/Rental+Storage).
3. RDAS is a [research data service](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989154/Research+Desktop+Attached+Storage) which supports the mounting of SMB shares. The supported operating systems are **MacOS**, **Linux**, and **Windows**. It provides 5TB of free storage.&#x20;
4. Research data not requiring immediate access should be stored in [General Research Data Storage (Tier 2)](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989566/AWS+Tier+2+Storage). \
   For example:
   1. Large datasets where only subsets are actively being analyzed
   2. Results no longer requiring immediate access
   3. Backups (highly encouraged!)
5. Data that require HIPAA-compliance can be [stored on Soteria](https://uarizona.atlassian.net/wiki/spaces/UAHPC/pages/75989667/Secure+HPC) (currently in the pilot phase).

Storage Option Summary

| Storage Option          | Purpose                                                                                                                             | Capacity                             | Cost                                                                                               | Restricted Data?             | Access                                               | Duration                                                  | Backup   |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------- | ---------------------------- | ---------------------------------------------------- | --------------------------------------------------------- | -------- |
| Primary Storage         | Research data. Supports compute. Directly attached to HPC                                                                           | /home 50GB /groups 500GB /xdisk 20TB | Free                                                                                               | Not for restricted data      | Directly mounted to HPC. Also uses Globus and DTNs   | Long term. Aligns with HPC purchase cycle                 | No       |
| R-DAS                   | Research Desktop Attached Storage - SMB shares                                                                                      | 5 TB                                 | Free                                                                                               | Not for restricted data      | Mounted to workstations as shares                    | Long term                                                 | No       |
| Rental Storage          | Research data. Large datasets. Typically for staging to HPC                                                                         | Rented per Terabyte per year         | Rental rate: $47.35 per TB per year                                                                | Not for restricted data      | Uses Globus and DTNs. Copy data to Primary           | Long term. Aligns with HPC purchase cycle                 | No       |
| Tier 2                  | Typically research data. Unused data is archived                                                                                    | 15GB to TB's                         | Tier-based system. First 1TB of active data and archival data are free. Active data > 1TB is paid. | Not for restricted data      | Uses Globus and AWS command line interface           | Typically long term since use of Glacier is free and slow | Archival |
| ReData                  | [Research data](https://data.library.arizona.edu/data-management/services/research-data-repository-redata). Managed by UA Libraries | Quota system                         | Free                                                                                               | Not for restricted data      | Login and fill out fields, then upload               | Longer than 10 years                                      | No       |
| <p>Soteria<br>HIPAA</p> | Secure data enclave                                                                                                                 | Individual requests                  | Free upon qualification                                                                            | Restricted data; HIPAA, ePHI | HIPAA training required, followed by request process | Long term                                                 | No       |
| Box                     | General data                                                                                                                        | 50GB                                 | Free                                                                                               | Not for restricted data      | Browser                                              | Long term                                                 | No       |
| Google Drive            | General data                                                                                                                        | 15GB                                 | Free. Google rates for amounts > 15GB                                                              | Not for restricted data      | Browser                                              | Unlimited usage expires March 1, 2023                     | No       |

## **NIH Data Management and Sharing Policy** <a href="#storage-nihdatamanagementandsharingpolicy" id="storage-nihdatamanagementandsharingpolicy"></a>

The NIH has issued a new [data management and sharing policy](https://sharing.nih.gov/data-management-and-sharing-policy), effective January 25, 2023. The [university libraries now offers a comprehensive guide](https://data.library.arizona.edu/data-management/nih-data-management-sharing-policy-2023) for how to navigate these policies and what they mean for you.

> **What's new about the 2023 NIH Data Management and Sharing Policy?**
>
> Previously, the NIH only required grants with $500,000 per year or more in direct costs to provide a brief explanation of how and when data resulting from the grant would be shared.
>
> The 2023 policy is entirely new. Beginning in 2023, ALL grant applications or renewals that generate Scientific Data must now include a robust and detailed plan for how you will manage and share data during the entire funded period. This includes information on data storage, access policies/procedures, preservation, metadata standards, distribution approaches, and more. You must provide this information in a data management and sharing plan (DMSP). The DMSP is similar to what other funders call a data management plan (DMP).
>
> The DMSP will be assessed by NIH Program Staff (though peer reviewers will be able to comment on the proposed data management budget). The Institute, Center, or Office (ICO)-approved plan becomes a Term and Condition of the Notice of Award.
