---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Cybersecurity 101
parent: kv - Solutions
grand_parent: Knowledge Vaults
permalink: /knowledge-vaults/solutions/cybersecurity
nav_order: 105
---

# Cybersecurity 101
Solutions
{: .badge .badge-pill .badge-primary }

* Do not remove this line (it will not be displayed)
{:toc}

# The Twelve Domains of Cybersecurity
ISO/IEC 27000 is a series of information security standards or best practices to help organizations improve their information security. Published by the International Organization for Standardization (ISO) and the International Electrotechnical Commission (ICO), the ISO 27000 standards set out comprehensive information security management system (ISMS) requirements. An ISMS consists of all of the administrative, technical and operational controls that address information security within an organization.

The ISO 27000 standard is represented by twelve independent domains. These twelve domains provide the basis for developing security standards and effective security management practices within organizations, as well as helping to facilitate communication between organizations.

| Domains                 | Details              |
| ----------------------- | -------------------- |
| Risk Assesment          | This is the first step in the risk management process, which determines the quantitative and qualitative value of risk related to a specific situation or threat. |
| Security policy          | This document addresses the constraints and behaviors of individuals within an organization and often specifies how data can be accessed, and what data is accessible by whom.  |
| Organization of information security          | This is the governance model set out by an organization for information security.      |
| Asset management          | This is an inventory of and classification scheme for information assets within an organization.      |
| Human resoruces security          | This refers to the security procedures in place that relate to employees joining, moving within and leaving an organization.    |
| Physical and environmental security          | This refers to the physical protection of an organization’s facilities and information.    |
| Communications and operations management          | This refers to the management of technical security controls of an organization’s systems and networks.    |
| Information systems acquisition, development and maintenance          | This refers to security as an integral part of an organization’s information systems.   |
| Access control          | This describes how an organization restricts access rights to networks, systems, applications functions and data in order to prevent unauthorized user access.    |
| Information security incident management          | This describes an organization’s approach to the anticipation of and response to information security breaches.    |
| Bussiness continuity management          | This describes the ability of an organization to protect, maintain and recover business-critical activities following a disruption to information systems.    |
| Compliance          | This describes the process of ensuring conformance with information security policies, standards and regulations. |


# The Cybersecurity Cube
The cube reminds us of what the task of protecting data entails, including the three dimensons of information security.

## Security Principles
The first dimension of the cybersecurity cube identifies the goals to protect cyberspace. The foundational principles of confidentiality, integrity and availability of data provide a focus which enables the cybersecurity expert to prioritize actions when protecting any networked system.

<img src="/assets/images/knowledge/solution/cybersecurity/cs_01.webp" alt="drawing"/>

**Data confidentiality** prevents the disclosure of information to unauthorized people, resources, or processes.

**Data integrity** refers to the accuracy, consistency, and trustworthiness of data.

**Data availability** ensures that information is accessible by authorized users when needed.

## Data States
The cyberspace domain contains a considerable amount of critically important data. But in what state? The second dimension of the cybersecurity cube represents the three possible data states:

- **Data in transit**.
- **Data at rest or in storage**.
- **Data in process.**.

<img src="/assets/images/knowledge/solution/cybersecurity/cs_02.webp" alt="drawing"/>

Effective cybersecurity requires the safeguarding of data in all three states. We can’t focus only on protecting data that is being processed, nor just on data in storage.

### Data at Rest
‘Data at rest’ refers to data that is in storage. Simply put, it is the state data is in when no user or process is accessing, requesting or amending it. Data at rest can be stored on local devices such as a hard disk in a user’s computer, or centralized on a network, such as an organization’s server.

Data that is not in transit or in-process is considered data at rest. If you have data that you need to store and will want to access later, a number of storage options exist.

- **Direct-attacted storage (DAS)**: This type of storage is connected to a computer. A hard drive or USB flash drive is an example of direct-attached storage. By default, systems are not set up to share direct-attached storage with other computers on their network.
- **Redundant array of independent disks (RAID)**: These professional storage solutions use multiple hard drives in an array, which is a method of combining multiple disks so that the operating system sees them as a single disk. RAID provides improved performance and fault tolerance.
- **Network attached storage (NAS) device**: This is a storage device connected to a network that allows storage and retrieval of data from a centralized location by authorized network users. NAS devices are flexible and scalable, meaning administrators can increase their capacity as needed.
- **Storage area network (SAN)**: SAN architecture is a network-based storage system. SAN systems connect to the network using high-speed interfaces, which allows for improved performance and the ability to connect multiple servers to a centralized disk storage repository.
- **Cloud storage**: This is a remote storage option that uses space on a data center provider and is accessible from any computer with Internet access, usually upon subscription. Google Drive, iCloud, and Dropbox are all examples of cloud storage providers.

### Data in transit
Data in transit is the second state of data we are going to look at, referring simply to data which is being transmitted — it is not at rest nor in use.

Data transmission involves sending information from one device to another, and protecting data in transit poses challenges. There are numerous ways to transmit data between devices.

- A **sneaker net** uses removable media to physically move data from one computer to another. Organizations will never be able to fully eliminate the use of a sneaker net as a way to transmit data between devices.
- **Wired networks** include copper and fiber optic media and can serve a local area network (LAN) or span great distances in wide area networks (WAN).
- **Wireless networks** use radio waves to transmit data. Wireless networks are replacing wired networks as they become faster and able to handle more traffic. Wireless networks increase the number of guest users with mobile devices on small office home office (SOHO) and enterprise networks. This also increases the attack surface of the network.

The protection of data in transit is one of the most challenging jobs of a cybersecurity professional. With the growth in mobile and wireless devices, and the increasing amounts of data collected and stored by organizations, cybersecurity professionals are responsible for protecting massive amounts of data crossing their network daily.

- **Protecting confidentiality**: Cybercriminals can capture, save, or steal data in transit. Cybersecurity professionals must take steps to safeguard data in transit, such as implementing VPNs, using SSL and IPsec, and various other methods of encrypting data for transmission.
- **Protecting integrity**: Cybercriminals can intercept and alter data in transit. Cybersecurity professionals deploy data integrity systems that test the integrity and authenticity of transmitted data to counter these actions. These systems include, for example, hashing and data redundancy.
- **Protecting availability**: Cybercriminals can use rogue or unauthorized devices to interrupt data availability, capturing it in transit. A simple mobile device can pose as a local wireless access point and trick unsuspecting users into associating with it. The cybercriminal can then hijack an authorized connection to a protected service or device. As data is being transmitted to and from the victim’s device, the cybercriminal can intercept and even delete it, affecting its availability.
Network security professionals can implement mutual authentication systems to counter these actions. Mutual authentication systems require the user to authenticate to the server and requests the server to authenticate to the user. This way, a user’s device can tell when it is being contacted or it is receiving data requests from unauthenticated, rogue systems, such as the attacker’s in the example above.

### Data in Process
Data in process refers to data during initial input, modification, computation or output. It is the state that data is in when it is neither in transit nor at rest — in simple terms, it is data that is being processed.

- **Input**: Protection of data integrity starts with the initial input of data. Organizations use several methods to collect data, each posing a potential threat to data integrity: data entry, scanning forms, file uploads and data collected from sensors. Corruption during the input process may include mislabeling and incorrect or mismatched data formats, data entry errors or disconnected and/or malfunctioning or inoperable system sensors.
- **Modification**: Data modification is any change made to original data, such as users manually modifying data, and programs processing and changing data. These changes are intentional. Processes like encoding/decoding, compression/decompression and encryption/decryption are all examples of data modification too. But changes to data can be unintentional or malicious. When data is modified in a way that stops it from being readable or usable, this is often referred to as data corruption. For instance, equipment failing can result in data corruption. Malicious code can also cause data corruption.
- **Output**: Data output refers to outputting data to output devices, such as printers, electronic displays and speakers. The accuracy of output data is critical because output provides information and influences decision-making. Examples of output data corruption include the incorrect use of data delimiters, incorrect communication configurations and improperly configured printers.

## Safeguards
The third dimension of the cybersecurity cube defines the pillars on which we need to base our cybersecurity defenses in order to protect data and infrastructure in the digital realm.

<img src="/assets/images/knowledge/solution/cybersecurity/cs_03.webp" alt="drawing"/>

These are **technology**, **policy** and **practices**, and improving education, training and awareness in people.

Cybersecurity professionals must use a range of different skills and disciplines available to them when protecting data and infrastructure in cyberspace.



# ISO 27000 and the CIA Triad

ISO 27000 is a universal framework that is applicable to every type of organization. In order to use it effectively, an organization must identify which domains, control objectives and controls apply to its environment and operations.

Most organizations do this by producing a statement of applicability (SOA) which allows it to tailor the available control objectives and controls to best meet its priorities around confidentiality, integrity and availability. 

# ISO 27000 and the States of Data

The ISO controls specifically address security objectives for data in each of the three states: in process, at rest (in storage) and in transit.  

The responsibility for identifying and implementing the relevant controls may lie with different groups across an organization. For example, a network security team may be responsible for controls that ensure the confidentiality, integrity and availability of all data being transmitted (data in transit), programmers and data entry analysts for data being processed (in process) and hardware support specialists for stored data (at rest/in storage).

# ISO 27000 and Safeguards

The ISO controls also provide technical direction for control objectives that relate to the cybersecurity policies, procedures and guidelines set out by senior management within an organization.

For example, let’s imagine that a senior management team establishes a policy to protect all data coming into or going out of an organization. The responsibility for implementing and configuring the networks, systems and equipment to be able to fulfill the policy directives will fall to the appropriate IT professionals within the organization, not the senior management team.









