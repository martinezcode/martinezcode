<!-- Header (Start) -->

# Threat Modeling Framework

## Engagement Report (2 of 2) - Recommendations & Action Plan

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

The general threat modeling process applied consists of creating a diagram, identifying threats, mitigating the threats, and validating each mitigation as illustrated in Figure 1. The STRIDE identification method supports this SDL approach by providing a consistent and predictable set of threat categories that can be applied to many different types of systems. Table 1 outlines the types of threats that can be identified using the STRIDE mnemonic. The first two steps of the process, *Diagram* and *Identify*, were detailed in a preceding report. The *Mitigate* step is documented in the following Recommendations section of this document.

![Figure 1. Threat modeling process flow based on `SDL` (Microsoft, 2017)](./threat-modeling-framework-3-recommendations-report/media/image1.tmp)

###### *Figure 1. Threat modeling process flow based on `SDL` (Microsoft, 2017).*

![Table 1. `STRIDE` model for threat identification (Shevchenko, 2018).](./threat-modeling-framework-3-recommendations-report/media/image2.tmp)

###### *Table 1. `STRIDE` model for threat identification (Shevchenko, 2018).*

**Recommendations**

Previously documented steps in the threat modeling process outlined the processes, external interactors, data stores, data flows, and trust boundaries for the new developments being considered by H&M. Automatic STRIDE identification was performed with Microsoft Threat Modeling Tool using its Analysis View feature to auto-generate a threat list for the system. The list was analyzed and revised to include 51 High priority threats and 7 Medium priority threats.

The automated STRIDE identification also included recommended mitigations. These mitigations were reviewed and mapped to NIST SP 800-53, *Security and Privacy Controls for Federal Information Systems and Organizations*, in the following subject areas:

- Access Control (AC)

- Audit and Accountability (AU)

- Identification and Authentication (IA)

- System and Services Acquisition (SA)

- System and Communications Protection (SC)

- System and Information Integrity (SI)

Mapping of the recommendations to NIST federal standards ensures that mitigations are based on best-practices and provides a reference for guidance as controls are implemented. The full list of recommendations with NIST mappings is provided in Appendix A.

**Action Plan**

The list of recommendations in Appendix A is long, due to the inclusion of at least one mitigation for each identified threat. However, many mitigations are repeated, and can be carried out simultaneously for multiple areas of the system. The following action plan was organized into groups of recommendations according to NIST SP 800-53 control areas, so similar controls may be implemented in a coordinated effort by representatives from organization groups, such as Information Technology (IT), Information Security (IS), and Development teams along with other stakeholders as needed. Recommendation groups were ordered by priority based on assessment of likelihood and/or severity of potential impact. The majority of threats are considered high priority, but in many cases mitigation of high priority threats may automatically reduce or eliminate one or more medium priority threats. Items listed as \"Threats Mitigated\" are high priority unless otherwise denoted as medium.

**System and Services Acquisition - Development Process, Standards, & Tools (SA-15)**

Recommendations:

- Do not use dynamic queries in stored procedures

- Implement Certificate Pinning

- Mitigate against Cross-Site Request Forgery (CSRF) attacks

- Implement proper authorization mechanism in Web API

- Ensure that standard authentication techniques are used to secure Web APIs

- Use standard libraries to manage token requests

Threats Mitigated:

- Spoofing

  - An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests

  - An adversary may spoof Customer Mobile Clients and gain access to Web API

  - An adversary may spoof Customer Web Clients and gain access to Web API

  - An adversary may spoof Database and gain access to Web API

  - An adversary may spoof F&G Web Clients and gain access to Web API

  - An adversary may spoof H&M Web Clients and gain access to Web API

  - An adversary obtains refresh or access tokens from Customer Mobile Clients and uses them to obtain access to the Portal & Delivery Front Ends API

- Information Disclosure

  - An adversary can gain access to sensitive data by performing SQL injection

  - An adversary can gain access to sensitive data by sniffing traffic from Mobile client

- Elevation of Privileges

  - An adversary may gain unauthorized access to Web API due to poor access control checks

Potential Impacts of Mitigations:

- Security program management overhead may be introduced into business processes and development practices

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams:

  - Require developers of information systems, system components, or information system services to follow a documented development process that:

    - Explicitly addresses security requirements

    - Identifies the standards and tools used in the development process

    - Documents the specific tool options and tool configurations used in the development process

    - Documents, manages, and ensures the integrity of changes to the process and/or tools used in development

    - Review the development process, standards, tools, and tool options/configurations regularly to determine if the process, standards, tools, and tool options/configurations selected and employed can satisfy organization-defined security requirements

**System and Communications Protection - Protection of Information at Rest (SC-28)**

Recommendations:

- Use strong encryption algorithms to encrypt data in the database

- Ensure that sensitive data in database columns is encrypted

Threats Mitigated:

- Information Disclosure

  - An adversary can gain access to sensitive PII or HBI data in database

Potential Impacts of Mitigations:

- Database performance may be reduced, or hardware system requirements may be increased

- Cryptographic key management overhead may be introduced into business processes

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams:

  - Ensure systems protect the confidentiality and integrity of sensitive information at rest by implementing cryptographic mechanisms to prevent unauthorized disclosure and modification

**Access Control - Account Management (AC-2)**

Recommendations:

- Sysadmin role should only have valid necessary users

Threats Mitigated:

- Elevation of Privileges

  - An adversary can gain unauthorized access to database due to loose authorization rules

Potential Impacts of Mitigations:

- User account management overhead may be introduced into business processes

- Some users may experience reduction/loss of privileges

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT & IS Teams:

  - Identify information system accounts to support missions/business functions

  - Assign account managers for accounts

  - Establish conditions for group/role membership

  - Specify authorized users, group/role membership, access authorizations/privileges, and other attributes for each account

  - Require approvals by organization-defined personnel for requests to create accounts

  - Create, enable, modify, disable, and remove accounts in accordance with organization-defined procedures or conditions

  - Monitor the use of accounts

**Access Control - Least Privilege (AC-6)**

Recommendations:

- Ensure that least-privileged accounts are used to connect to Database server

Threats Mitigated:

- Information Disclosure

  - An adversary can gain access to sensitive data by performing SQL injection

- Elevation of Privileges

  - An adversary can gain unauthorized access to database due to loose authorization rules

Potential Impacts of Mitigations:

- User account management overhead may be introduced into business processes

- Some users may experience reduction/loss of privileges

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS & Development Teams:

  - Employ the principle of least privilege, allowing only authorized accesses for users (or processes acting on behalf of users) which are necessary to accomplish assigned tasks in accordance with organizational missions and business functions

  - Consider the creation of additional processes, roles, and information system accounts as necessary, to achieve least privilege

**System and Information Integrity - Information Input Validation (SI-10)**

Recommendations:

- Ensure that type-safe parameters are used in Web API for data access

- Implement input validation on all string type parameters accepted by Web API methods

Threats Mitigated:

- Tampering

  - An adversary can gain access to sensitive data by performing SQL injection through Web API

  - An adversary may inject malicious inputs into an API and affect downstream processes

Potential Impacts of Mitigations:

- Security program management overhead may be introduced into business processes and development practices

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams:

  - Ensure systems check the validity of information inputs by:

    - Checking the valid syntax and semantics of information system inputs (e.g., character set, length, numerical range, and acceptable values)

    - Verifying that inputs match specified definitions for format and content

**Access Control - Audit Events (AU-2)**

Recommendations:

- Ensure that login auditing is enabled on Database server

- Ensure that auditing and logging is enforced on Web API

Threats Mitigated:

- Repudiation

  - Attacker can deny a malicious act on an API leading to repudiation issues

  - An adversary can deny actions on database due to lack of auditing (Medium)

Potential Impacts of Mitigations:

- Log management overhead may be introduced into business processes

- Some users may react negatively to loss of anonymity

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS & Development Teams:

  - Determine that the information system is capable of auditing specific events

  - Coordinate the security audit function with other organizational entities requiring audit-related information to enhance mutual support and help guide the selection of auditable events

  - Provide a rationale for why the auditable events are deemed to be adequate to support after-the-fact investigations of security incidents

  - Determine that specific events are to be audited along with the frequency of (or situation requiring) auditing for each identified event

**System and Communications Protection - Transmission Confidentiality & Integrity (SC-8)**

Recommendations:

- Force all traffic to Web APIs over HTTPS connection

Threats Mitigated:

- Information Disclosure

  - An adversary can gain access to sensitive data by sniffing traffic to Web API

Potential Impacts of Mitigations:

- Some users may need to update web browser to access Web API over HTTPS

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS & Development Teams:

  - Ensure systems protect the confidentiality and integrity of transmitted information by employing encryption techniques

**System and Communications Protection - Boundary Protection (SC-7)**

Recommendations:

- Configure a firewall for Database access

Threats Mitigated:

- Elevation of Privileges

  - An adversary can gain unauthorized access to database due to lack of network access protection

Potential Impacts of Mitigations:

- System performance may be reduced, or hardware system requirements may be increased

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT & IS Teams:

  - Monitor and control communications at the external boundary of the system and at key internal boundaries within the system

  - Implement subnetworks for publicly accessible system components that are separated from internal organizational networks

  - Enable connection to systems only through managed interfaces consisting of boundary protection devices arranged in accordance with an organizational security architecture

**System and Information Integrity - Information System Monitoring (SI-4)**

Recommendations:

- Enable threat detection on Database server

Threats Mitigated:

- Tampering

  - An adversary may leverage the lack of monitoring systems and trigger anomalous traffic to database

Potential Impacts of Mitigations:

- Database performance may be reduced, or hardware system requirements may be increased

- User account management overhead may be introduced into business processes

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT & IS Teams:

  - Monitor the information system to detect:

    - Attacks and indicators of potential attacks

    - Unauthorized local, network, and remote connections

    - Unauthorized use of the information system

  - Implement measures to protect information obtained from intrusion-monitoring tools from unauthorized access, modification, and deletion

**System and Information Integrity - Software, Firmware, and Information Integrity (SI-7)**

Recommendations:

- Add digital signature to critical database securables

- Obfuscate generated binaries before distributing to end users

Threats Mitigated:

- Tampering

  - An adversary can tamper critical database securables and deny the action

  - An adversary can reverse engineer and tamper binaries (Medium)

Potential Impacts of Mitigations:

- Database performance may be reduced, or hardware system requirements may be increased

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams:

  - Employ integrity verification tools to detect unauthorized changes to database securables and binary executable application files

  - Ensure software systems perform an integrity check of database securables and binary executable application files at startup, transitional states, security-relevant events, and/or organization-defined frequency

**System and Communications Protection - Information in Shared Resources (SC-4)**

Recommendations:

- Encrypt sensitive or PII data written to phones local storage

- Ensure that sensitive data relevant to Web API is not stored in browser\'s storage

- Encrypt sections of Web API\'s configuration files that contain sensitive data

Threats Mitigated:

- Information Disclosure

  - An adversary can gain sensitive data from mobile device

  - An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage

  - An adversary can gain access to sensitive data stored in Web API\'s config files (Medium)

Potential Impacts of Mitigations:

- System performance may be reduced, or hardware system requirements may be increased

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams:

  - Ensure the information system prevents unauthorized and unintended information transfer via shared system resources

**System and Information Integrity - Error Handling (SI-11)**

Recommendations:

- Ensure that proper exception handling is done in Web API

Threats Mitigated:

- Information Disclosure

  - An adversary can gain access to sensitive information from an API through error messages

Potential Impacts of Mitigations:

- Security program management overhead may be introduced into business processes and development practices

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT, IS, & Development Teams

  - Ensure systems generate error messages that:

    - Provide information necessary for corrective actions without revealing information that could be exploited by adversaries

    - Reveal sensitive error messages only to authorized personnel

**Access Control - Access Enforcement (AC-3)**

Recommendations:

- Implement Row Level Security (RLS) to prevent tenants from accessing each other\'s data

Threats Mitigated:

- Elevation of Privileges

  - An adversary can gain unauthorized access to database due to loose authorization rules

Potential Impacts of Mitigations:

- Database performance may be reduced, or hardware system requirements may be increased

- User account management overhead may be introduced into business processes

- Some users may experience reduction/loss of access to database records

Timeframe:

- Implement within 6 Months

- Review & update annually

Actions (NIST, 2013):

- IT & IS Teams:

  - Configure systems to enforce authorizations for access to information resources in accordance with access control policies

**Conclusion**

The organization may follow the recommendations in the proposed order or revise and reorder items according to priorities determined by the IT, IS, Development teams and other stakeholders. The potential impacts should be considered, and the organization may choose to avoid, transfer, or accept the documented risks instead of implementing recommended mitigations. A formal process for authorizing, approving, and documenting risk decisions is recommended. In most cases, the potential threats should be mitigated, but the organization should weigh all options and determine an optimal balance of trade-offs between potential impact and risk levels according to its own unique priorities and risk tolerance.

# References

Microsoft. (2017, August 17). Getting started with the Threat Modeling Tool. *Azure Security Documentation*. Retrieved from
https://docs.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-getting-started

NIST. (2013, April). Security and Privacy Controls for Federal Information Systems and Organizations. *NIST SP 800-53 Revision 4*. Retrieved from
https://csrc.nist.gov/publications/detail/sp/800-53/rev-4/final

Shevchenko, N. (2018, December 3). Threat Modeling: 12 Available Methods. *Carnegie Mellon University*. Retrieved from
https://insights.sei.cmu.edu/sei_blog/2018/12/threat-modeling-12-available-methods.html

Shostack, A. (2014). *Threat Modeling, Designing for Security.* Wiley Publishing.

# Appendix A: Recommendations List

```
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| Interaction                                                  | Category                | Title                                                                                                                                             | Priority | Mitigation                                                                            | NIST Control Area | NIST                                          |
|                                                              |                         |                                                                                                                                                   |          |                                                                                       |                   |                                               |
|                                                              |                         |                                                                                                                                                   |          |                                                                                       |                   | Control                                       |
|                                                              |                         |                                                                                                                                                   |          |                                                                                       |                   |                                               |
|                                                              |                         |                                                                                                                                                   |          |                                                                                       |                   | Name                                          |
+==============================================================+=========================+===================================================================================================================================================+==========+=======================================================================================+===================+===============================================+
| From Customer Mobile Clients to Portal & Delivery Front Ends | Spoofing                | An adversary may spoof Customer Mobile Clients and gain access to Web API                                                                         | High     | Ensure that standard authentication techniques are used to secure Web APIs            | SA-15             | Development Process, Standards, and Tools     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary obtains refresh or access tokens from Customer Mobile Clients and uses them to obtain access to the Portal & Delivery Front Ends API | High     | Use standard libraries to manage token requests                                       | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     | Ensure that type-safe parameters are used in Web API for data access                  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     | Implement input validation on all string type parameters accepted by Web API methods  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can reverse engineer and tamper binaries                                                                                             | Medium   | Obfuscate generated binaries before distributing to end users                         | SI-7              | Software, Firmware, and Information Integrity |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     | Ensure that auditing and logging is enforced on Web API                               | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain sensitive data from mobile device                                                                                           | High     | Encrypt sensitive or PII data written to phones local storage                         | SC-4              | Information in Shared Resources               |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     | Force all traffic to Web APIs over HTTPS connection                                   | SC-8              | Transmission Confidentiality and Integrity    |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic from Mobile client                                                             | High     | Implement Certificate Pinning                                                         | IA-5              | Authenticator Management                      |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     | Ensure that proper exception handling is done in Web API                              | SI-11             | Error Handling                                |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   | Encrypt sections of Web API\'s configuration files that contain sensitive data        | SC-4              | Information in Shared Resources               |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     | Implement proper authorization mechanism in Web API                                   | SA-15             | Development Process, Standards, and Tools     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| From Customer Web Clients to Portal & Delivery Front Ends    | Spoofing                | An adversary may spoof Customer Web Clients and gain access to Web API                                                                            | High     | Ensure that standard authentication techniques are used to secure Web APIs            | SA-15             | Development Process, Standards, and Tools     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     | Mitigate against Cross-Site Request Forgery (CSRF) attacks                            | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     | Ensure that type-safe parameters are used in Web API for data access                  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     | Implement input validation on all string type parameters accepted by Web API methods  | SI-10             | Information Input Validation                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     | Ensure that auditing and logging is enforced on Web API                               | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     | Force all traffic to Web APIs over HTTPS connection                                   | SC-8              | Transmission Confidentiality and Integrity    |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     | Ensure that sensitive data relevant to Web API is not stored in browser\'s storage    | SC-4              | Information in Shared Resources               |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     | Ensure that proper exception handling is done in Web API                              | SI-11             | Error Handling                                |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   | Encrypt sections of Web API\'s configuration files that contain sensitive data        | SC-4              | Information in Shared Resources               |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     | Implement proper authorization mechanism in Web API                                   | SA-15             | Development Process, Standards, and Tools     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| From Database to Data                                        | Tampering               | An adversary can tamper critical database securables and deny the action                                                                          | High     | Add digital signature to critical database securables                                 | SI-7              | Software, Firmware, and Information Integrity |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may leverage the lack of monitoring systems and trigger anomalous traffic to database                                                | High     | Enable threat detection on Database server                                            | SI-4              | Information System Monitoring                 |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | An adversary can deny actions on database due to lack of auditing                                                                                 | Medium   | Ensure that login auditing is enabled on Database server                              | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive PII or HBI data in database                                                                             | High     | Use strong encryption algorithms to encrypt data in the database                      | SC-28             | Protection of Information at Rest             |
|                                                              |                         |                                                                                                                                                   |          +---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         |                                                                                                                                                   |          | Ensure that sensitive data in database columns is encrypted                           | SC-28             | Protection of Information at Rest             |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection                                                                        | High     | Ensure that least-privileged accounts are used to connect to Database server          | AC-6              | Least Privilege                               |
|                                                              |                         |                                                                                                                                                   |          +---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         |                                                                                                                                                   |          | Do not use dynamic queries in stored procedures                                       | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary can gain unauthorized access to database due to lack of network access protection                                                    | High     | Configure a firewall for Database access                                              | SC-7              | Boundary Protection                           |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain unauthorized access to database due to loose authorization rules                                                            | High     | Ensure that least-privileged accounts are used to connect to Database server          | AC-6              | Least Privilege                               |
|                                                              |                         |                                                                                                                                                   |          +---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         |                                                                                                                                                   |          | Sysadmin role should only have valid necessary users                                  | AC-2              | Account Management                            |
|                                                              |                         |                                                                                                                                                   |          +---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         |                                                                                                                                                   |          | Implement Row Level Security RLS to prevent tenants from accessing each other\'s data | AC-3              | Access Enforcement                            |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| From Database to Portal & Delivery Front Ends                | Spoofing                | An adversary may spoof Database and gain access to Web API                                                                                        | High     | Ensure that standard authentication techniques are used to secure Web APIs            | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Tampering               | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     | Implement input validation on all string type parameters accepted by Web API methods  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     | Ensure that type-safe parameters are used in Web API for data access                  | SI-10             | Information Input Validation                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     | Ensure that auditing and logging is enforced on Web API                               | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive information from an API through error messages                                                          | High     | Ensure that proper exception handling is done in Web API                              | SI-11             | Error Handling                                |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     | Force all traffic to Web APIs over HTTPS connection                                   | SC-8              | Transmission Confidentiality and Integrity    |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   | Encrypt sections of Web API\'s configuration files that contain sensitive data        | SC-4              | Information in Shared Resources               |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     | Implement proper authorization mechanism in Web API                                   | SA-15             | Development Process, Standards, and Tools     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| From F&G Web Clients to Portal & Delivery Front Ends         | Spoofing                | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     | Mitigate against Cross-Site Request Forgery (CSRF) attacks                            | SA-15             | Development Process, Standards, and Tools     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may spoof F&G Web Clients and gain access to Web API                                                                                 | High     | Ensure that standard authentication techniques are used to secure Web APIs            | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Tampering               | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     | Implement input validation on all string type parameters accepted by Web API methods  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     | Ensure that type-safe parameters are used in Web API for data access                  | SI-10             | Information Input Validation                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     | Ensure that auditing and logging is enforced on Web API                               | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive information from an API through error messages                                                          | High     | Ensure that proper exception handling is done in Web API                              | SI-11             | Error Handling                                |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     | Ensure that sensitive data relevant to Web API is not stored in browser\'s storage    | SC-4              | Information in Shared Resources               |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     | Force all traffic to Web APIs over HTTPS connection                                   | SC-8              | Transmission Confidentiality and Integrity    |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   | Encrypt sections of Web API\'s configuration files that contain sensitive data        | SC-4              | Information in Shared Resources               |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     | Implement proper authorization mechanism in Web API                                   | SA-15             | Development Process, Standards, and Tools     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
| From H&M Web Clients to Portal & Delivery Front Ends         | Spoofing                | An adversary may spoof H&M Web Clients and gain access to Web API                                                                                 | High     | Ensure that standard authentication techniques are used to secure Web APIs            | SA-15             | Development Process, Standards, and Tools     |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain unauthorized access to API end points due to unrestricted cross domain requests                                             | High     | Mitigate against Cross-Site Request Forgery (CSRF) attacks                            | SA-15             | Development Process, Standards, and Tools     |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Tampering               | An adversary can gain access to sensitive data by performing SQL injection through Web API                                                        | High     | Ensure that type-safe parameters are used in Web API for data access                  | SI-10             | Information Input Validation                  |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may inject malicious inputs into an API and affect downstream processes                                                              | High     | Implement input validation on all string type parameters accepted by Web API methods  | SI-10             | Information Input Validation                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Repudiation             | Attacker can deny a malicious act on an API leading to repudiation issues                                                                         | High     | Ensure that auditing and logging is enforced on Web API                               | AU-2              | Audit Events                                  |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Information Disclosure  | An adversary can gain access to sensitive data by sniffing traffic to Web API                                                                     | High     | Force all traffic to Web APIs over HTTPS connection                                   | SC-8              | Transmission Confidentiality and Integrity    |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary may retrieve sensitive data (e.g., auth tokens) persisted in browser storage                                                         | High     | Ensure that sensitive data relevant to Web API is not stored in browser\'s storage    | SC-4              | Information in Shared Resources               |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive information from an API through error messages                                                          | High     | Ensure that proper exception handling is done in Web API                              | SI-11             | Error Handling                                |
|                                                              |                         +---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              |                         | An adversary can gain access to sensitive data stored in Web API\'s config files                                                                  | Medium   | Encrypt sections of Web API\'s configuration files that contain sensitive data        | SC-4              | Information in Shared Resources               |
|                                                              +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
|                                                              | Elevation of Privileges | An adversary may gain unauthorized access to Web API due to poor access control checks                                                            | High     | Implement proper authorization mechanism in Web API                                   | SA-15             | Development Process, Standards, and Tools     |
+--------------------------------------------------------------+-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+----------+---------------------------------------------------------------------------------------+-------------------+-----------------------------------------------+
```

###### *Table A. Recommended mitigations with mapping to NIST SP 800-53 Revision 4 security controls.*

<!-- Footer (Start) -->

# Author

### Aaron Martinez

- GitHub: <https://github.com/martinezcode/>
- LinkedIn: <https://www.linkedin.com/in/martinezcode/>

<!-- Footer (End) -->