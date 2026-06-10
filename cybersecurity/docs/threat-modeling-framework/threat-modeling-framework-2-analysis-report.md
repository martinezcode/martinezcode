<!-- Header (Start) -->

# Threat Modeling Framework

## Engagement Report (1 of 2) - Threat Analysis

### Case Study: Harry & Mae's Restaurant Chain

<!-- Header (End) -->

**Introduction**

To conduct threat analysis for Harry & Mae\'s Inc. (H&M) restaurant, franchising, and payment processing business, a flexible threat modeling process was developed following the Microsoft Security Development Lifecycle (SDL) approach consisting of four steps: *Diagram*, *Identify*, *Mitigate*, and *Validate*. The process incorporates the STRIDE model for identifying threats against system entities, events, and boundaries across a generalized set of common threats: *Spoofing*, *Tampering*, *Information Disclosure*, *Repudiation*, *Denial of Service*, and *Elevation of Privileges*.

In addition to seeking improvements in the security of the organization as whole, H&M is considering the following new developments:

1.  H&M\'s is investigating a merger with another restaurant, Fiddles & Griddles (F&G). They are investigating combining information assets and resources for improved efficiencies. 

2.  H&M\'s is investigating expansion into a new area: Online ordering and delivery through web and mobile applications.

The modeling process was applied with a focus on threats associated with these new developments, using the following assumptions:

1.  H&M\'s existing infrastructure has been or will be analyzed separately.

2.  F&G\'s existing infrastructure has been or will be analyzed separately. 

3.  H&M and F&G will operate as separate business entities with each continuing their own existing restaurant services which offer distinct products for different customer bases.

4.  Unrelated H&M operations such as payment processing services will remain exclusive to H&M.

5.  H&M and F&G will share information assets and resources, such as online ordering and delivery data, through a web portal application.

6.  H&M will implement the online ordering and delivery system in house.

7.  H&M will implement the shared information assets and resources web portal application in house.

**Threat Modeling Process**

The general threat modeling process applied consists of creating a diagram, identifying threats, mitigating the threats, and validating each mitigation as illustrated in Figure 1. The STRIDE identification method supports this SDL approach by providing a consistent and predictable set of threat categories that can be applied to many different types of systems. Table 1 outlines the types of threats that can be identified using the STRIDE mnemonic. The first two steps of the process, *Diagram* and *Identify*, are detailed in this report. The following steps will be reported in one or more forthcoming documents.

![Figure 1. Threat modeling process flow based on `SDL` (Microsoft, 2017)](./threat-modeling-framework-2-analysis-report/media/image1.tmp)

###### *Figure 1. Threat modeling process flow based on `SDL` (Microsoft, 2017).*

![Table 1. `STRIDE` model for threat identification (Shevchenko, 2018).](./threat-modeling-framework-2-analysis-report/media/image2.tmp)

###### *Table 1. `STRIDE` model for threat identification (Shevchenko, 2018).*

**Current Trends in Restaurant and Franchise Services Cybersecurity**

Restaurant Group, Fraud Education and Risk Management, and Cybersecurity experts with Bank of America Merrill Lynch (2019) observed that the food service industry faces unique challenges due to current technology trends. In particular, the authors noted:

> *The food service industry has a set of characteristics that make stores vulnerable to theft of all kinds, but especially losses due to cyber crime - including a large volume of transactions, high employee turnover, a wide-ranging network of both local and national vendors, and extensive digital connections to corporate and regional offices as well as IT and POS providers. As more quick-service restaurants and chains have responded to changing customer habits, like allowing customers to pay by credit or debit card via a mobile device, their response has opened up new vulnerabilities.* *(Bank of America Merrill Lynch, 2019)*

According to the authors, restaurants have become a \"prime target\" through vendor connections, point of sale (POS) systems, and general IT support, with credential compromises often used to establish backdoors, deploy malware, and gather customer payment information across franchise locations (Bank of America Merrill Lynch, 2019).

**Diagram**

Microsoft Threat Modeling Tool software was used to create the data flow diagram (DFD) diagram shown in Figure 2, which describes the new developments including proposed information and resource sharing between H&M and F&G, as well as implementation of online ordering and delivery services.

![Figure 2. Data flow diagram representing new development areas being considered by H&M.](./threat-modeling-framework-2-analysis-report/media/image3.tmp)

###### Figure 2. Data flow diagram representing new development areas being considered by H&M.

The DFD was drawn to represent aspects of the system, including:

- Processes (Circles)

  - Portal & Delivery Front End Software

  - Database Interactions

  - Database Administration

- External Interactors (Square Boxes)

  - H&M Web Clients

  - F&G Web Clients

  - Database Administrators

  - Database Users

  - Customer Web Clients

  - Customer Mobile Clients

- Data Stores (Two-Sided Boxes)

  - Data Records

  - Management Records

  - Activity Logs

- Data Flows (Arrows)

  - One-Way Requests

  - Two-Way Requests and Responses

- Trust Boundaries (Dashed Lines)

  - H&M\'s Database Account

  - H&M\'s Database Cluster

  - H&M\'s Infrastructure

  - F&G\'s Infrastructure

  - H&M\'s and F&G\'s Online Ordering and Delivery Services

**Identify**

The STRIDE model simplified the identify step by providing a quick reference for the most common types of credible threats. Automatic STRIDE identification was performed with Microsoft Threat Modeling Tool using its Analysis View feature to auto-generate a threat list for elements of the DFD. The list was analyzed and revised to include the 57 threats documented in Table 2.

```
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| Interaction                                                  | Category                | Title                                                                                                                                             | Priority |
+==============================================================+=========================+===================================================================================================================================================+==========+
| From Customer Mobile Clients to Portal & Delivery Front Ends | Spoofing                | An adversary may spoof Customer Mobile Clients and gain access to Web API                                                                         | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary obtains refresh or access tokens from Customer Mobile Clients and uses them to obtain access to the Portal & Delivery Front Ends API | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can reverse engineer and tamper binaries                                                                                             | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain sensitive data from mobile device                                                                                           | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic from Mobile client                                                             | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| From Customer Web Clients to Portal & Delivery Front Ends    | Spoofing                | An adversary may spoof Customer Web Clients and gain access to Web API                                                                            | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| From Database to Data                                        | Tampering               | An adversary can tamper critical database securables and deny the action                                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may leverage the lack of monitoring systems and trigger anomalous traffic to database                                                | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | An adversary can deny actions on database due to lack of auditing                                                                                 | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive PII or HBI data in database                                                                             | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection                                                                        | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary can gain unauthorized access to database due to lack of network access protection                                                    | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain unauthorized access to database due to loose authorization rules                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| From Database to Portal & Delivery Front Ends                | Spoofing                | An adversary may spoof Database and gain access to Web API                                                                                        | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Tampering               | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive information from an API through error messages                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| From F&G Web Clients to Portal & Delivery Front Ends         | Spoofing                | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may spoof F&G Web Clients and gain access to Web API                                                                                 | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Tampering               | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive information from an API through error messages                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
| From H&M Web Clients to Portal & Delivery Front Ends         | Spoofing                | An adversary may spoof H&M Web Clients and gain access to Web API                                                                                 | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+
```

###### Table 2. List of threats identified new development areas being considered by H&M.

**Conclusion**

As a starting point in the threat modeling process, the DFD shown in Figure 2 outlined the processes, external interactors, data stores, data flows, and trust boundaries for the new developments being considered by H&M. Using STRIDE modeling, 51 High priority threats and 7 Medium priority threats were identified in Table 2. Future analysis will include recommended mitigations and tests for validating the effectiveness of the threat model.

As indicated by the process flow diagram in Figure 1, the threat modeling process is iterative. Each step leads to the next, and the entire process begins again after each step has been completed. Repeating the process allows for refinement of the diagram, threat list, mitigating controls, and validation tests. The DFD and threat list are likely to change as the organization\'s development plans evolve, technology advances, and threats are introduced or removed. Over time, the models will improve, analysis will improve, and system security will improve.

# References

Bank of America Merrill Lynch. (2019). Restaurant Cyber Crime: How to Defend Your Business. Retrieved from
https://www.bofaml.com/content/dam/boamlimages/documents/articles/B2_019/restaurant_group_cybercrime.pdf

Microsoft. (2017, August 17). Getting started with the Threat Modeling Tool. *Azure Security Documentation*. Retrieved from
https://docs.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-getting-started

Shevchenko, N. (2018, December 3). Threat Modeling: 12 Available Methods. *Carnegie Mellon University*. Retrieved from
https://insights.sei.cmu.edu/sei_blog/2018/12/threat-modeling-12-available-methods.html

Shostack, A. (2014). *Threat Modeling, Designing for Security.* Wiley Publishing.

<!-- Footer (Start) -->

# Author

### Aaron Martinez

- GitHub: <https://github.com/martinezcode/>
- LinkedIn: <https://www.linkedin.com/in/martinezcode/>

<!-- Footer (End) -->