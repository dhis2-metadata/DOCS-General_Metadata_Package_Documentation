# Real-time Monitoring of Vaccination Campaigns - Implement  { #imm-camp-implement }

This chapter focuses on aspects of **DHIS2 implementation strategies** and decisions that typically must be made on a per-country/per-campaign basis to accommodate local context. The guide is intended for DHIS2 **implementers** to be aware of deployment strategies and approaches for implementing a robust and fit-for-purpose campaign with DHIS2.

## Selecting Modes of Data Collection

DHIS2 allows **multiple modes of data entry**, including a native DHIS2 Android client, and can support hybrid implementations that rely on a combination of paper-based and electronic reporting suitable for offline settings.

The following considerations should inform the implementation plan:

- Real-time data entry vs secondary/retrospective data entry
- Level of primary data collection: which users collect the primary data, using what tools?
- Level of electronic reporting: in the case of paper-based or hybrid primary data collection, implementers should define at what level the data should be entered into the system based on feasibility, context, and data analysis requirements.
- Connectivity at vaccination site and sub-district operational units
- Modes of electronic reporting
  - Web-based
  - DHIS2 Android [mobile](https://docs.dhis2.org/en/implement/android-implementation/about-this-guide.html) data entry systems
  - SMS, USSD & other modes of data transmission

The key benefit of such flexibility is that **no interoperability solution is required** - once the data is entered into the system, **DHIS2 becomes a repository of the campaign’s data**. Moreover the possibility of entering the data offline (possibly in a mobile device) and synchronising the data in a second moment allows for the chance of entering data directly in the field without having to first tally on paper.

### Tracker

The use of DHIS2 Tracker for real-time monitoring **should be carefully considered** depending on the availability of infrastructure (i.e. robust, extendable hosting), network connectivity at end user levels, and feasibility of training data entry staff to collect data in Tracker in real-time. Many countries faced substantial challenges with large back-logs of tracker data entry during COVID-19 vaccine delivery due to limited resources for data entry, limited network connectivity and other foundational issues. If real-time data entry is not feasible, **DHIS2 Tracker can also be implemented in parallel to an aggregate real-time monitoring solution** provided that there are sufficient resources for secondary data entry.

It is strongly recommended to review the Tracker Implementation Guide and conduct a rapid Tracker-readiness assessment to ensure that key foundational components and facilitators are in place for a successful Tracker deployment.

### Submitting data via SMS & USSD

The [SMS Module](https://docs.dhis2.org/en/develop/developing-with-the-android-sdk/sms-module.html) can be used as a fallback method to upload data when there is **no internet connection**. DHIS2 supports accepting data via SMS, however, the SMS needs to be structured in a certain syntax to be interpreted and fed into DHIS2.The DHIS2 Android App acts as a transparent layer to send the information via SMS where the user does not have to worry about writing the SMS. To send SMSs with the Android App the SMS gateway needs to be properly configured.

For more information on [SMS data entry and the configuration](https://docs.dhis2.org/en/manage/performing-system-administration/dhis-core-version-master/using-gateways-for-sms-reporting.html) please refer to the embedded links.

### Other mobile data entry tools

Data collection with non-DHIS2 mobile apps and tools such as **ODK and KoboToolbox** is possible, but the solution requires the presence of a **strong technical team** in the country in order to facilitate the [interoperability](https://docs.dhis2.org/en/implement/implementing-dhis2/integration-concepts.html) and supervise the establishment of a strong metadata governance in both systems to ensure the compatibility of the collected data.

## Infrastructure & Performance Testing

### Planning for Scale

For large-scale, high volume campaigns, it is typically recommended that a **dedicated DHIS2 instance** be used during the campaign and key campaign data such as coverage rates integrated into the HMIS after for triangulation and use. This is to **preserve the stability of the routine HMIS** and prevent any disruptions of routine reporting, acknowledging that many national aggregate HMIS instances are hosted on-site or in local servers – often with only a single server available.

Hosting infrastructure should be planned at the **earliest stages**.  Where possible under national policies, it is strongly recommended to host using **cloud-based resources**. Hosting in the cloud typically can allow for improved performance and scalability as a network of physical or virtual servers can be used. Server monitoring tools should be deployed to ensure that server admins have timely, accurate information about performance throughout the campaign and can make adjustments in response to bottlenecks that may occur. See additional [technical guidance on server hosting, admin & monitoring](https://docs.dhis2.org/en/implement/tracker-implementation/tracker-performance-at-scale.html#server-hosting-administration-and-monitoring).

Guiding questions for planning infrastructure:

- Mode of data entry: aggregate or tracker data entry?
  - If Tracker is used:
    - How many Tracked Entities are you expecting?
    - How many Tracked Entity Attributes does each Tracked Entity have?
    - How many enrollments?
    - How many events?
- Number of organizational units?
  - How are they distributed in the hierarchy (well-balanced or large numbers of sub-units in some parts?)
  - How many levels?
  - Are data entered at different OU levels, or just at the lowest level?
  - Are some OUs more active than others, or is activity distributed evenly across all of them?
- Number of concurrent users?
  - Distribution of users based on function/role: e.g. how many users configured with roles to enter aggregate data vs tracker data, how many users configured with roles that only allow access to dashboards/analytics apps?
  - Do all users have access to all OUs, or are there some limitations? If yes, which?
- How many data values are expected?
  - Tracker vs aggregate?

> **Example**
>
> **DHIS2 IN USE:**
>
> The **Bangladesh measles mass campaign** needed to support and maintain a total of **403,765 microplan-related OU**s, daily vaccination data, and a total of **16,000 user IDs**.
With such a scale, the campaign provided DHIS2 core developers a real use case [challenging scenario where to test performance and stress testing](https://community.dhis2.org/t/bangladesh-is-the-first-country-to-use-dhis2-in-planning-implementing-and-monitoring-mr-campaign-in-largest-scale/42408) against large databases. The result of such assessments translated into significant improvement in the memory usage of API and performance fixes on tracker (in combination with OUs and user access) as a secondary cascade impact of the primary tests on aggregate.

## User Management

Planning how the staff involved in the SIA will be able to access the information is also a key consideration to evaluate in the planning pre-campaign stage as this will also reflect the roles and responsibilities during and after the activities.

All the global packages are published with some core users - administrators, data collectors, and data monitoring. These [users and their roles](https://docs.dhis2.org/en/implement/maintenance-and-use/users-and-user-roles.html) can be kept and tweaked for the local context, or can be completely changed depending on the type of implementation and distribution of workload.

Decentralised access control and user management are key for the functioning of an information system. Already with routine HMIS data district users can have their accounts managed and their access limited to their district. It is therefore core to underline that, especially during vaccination campaigns when the temptation to take shortcuts and share users among different people and positions or to have just one user per higher hierarchy level with a range of roles, the **main recommendation would be to assign one single role per position/person, or a fixed set of roles per position**. This means no user sharing and very specific roles depending on the type of work within the data and workflow of the campaign. This approach is very important to align the configuration of the SIA in the system to the national laws/regulations related to data storage, protection and security in the country. Moreover, this could also be a valuable tool to **maintain a good supervision of health workers and data entry clerks** and monitor the quality of performance and data through time.

While the proper institution of user and user roles is core for the proper functioning and supervision of the workflow of the campaign, there may be **data privacy concerns** as multiple stakeholders may have access to digitised data that can therefore be easily shareable. This concern is of particular importance whenever a tracker is implemented, though local regulations and laws should be implemented both for aggregate and individual data.

The [DHIS2 guidelines on security considerations](https://docs.dhis2.org/en/implement/implementing-dhis2/security-considerations.html) provide a range of contextual advice and pragmatic measures that can be implemented and monitored for the management of security.

## User Acceptance Testing

Conducting User Acceptance Test (UAT) with a small but representative sample of end users is recommended prior to user **training** to optimise the configuration for usability. Implementers/testers/designers should map each end user **workflow** and test the configuration internally before the UAT. The UAT may include:

- Observation as users walk through workflow step to step
- Recording the time to complete the workflow, as well as noting any unnecessary steps, delays, or errors noticed during the data entry process
- Documenting the process and repeating with a sampling of users from each user group (i.e. test each end user workflow)
- Re-testing workflows after optimising the configuration
