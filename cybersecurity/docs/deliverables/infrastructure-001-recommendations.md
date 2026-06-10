<!-- Header (Start) -->

# Network Architecture - Analysis & Recommendations

### By Aaron Martinez, Adam Bessler, Amanda Fasano, Jamario Kelly, Naomi See, & Norbert Youtat Tankeu

<!-- Header (End) -->

<!-- Body (Start) -->

## Abstract

When designing a network, selecting an underlying infrastructure service that meets the all the project requirements will ensure the highest likelihood for success in the final implementation. A thorough analysis of multiple available network services should take place so a fitting infrastructure can be determined. We apply this methodology to three network design scenarios. Scenario A is a network connecting a large number of locations in a metropolitan area, Scenario B is a wide area network (WAN) that interconnects several locations in remote areas across the United States, and Scenario C is a multimedia application network servicing a small number of locations. For each case, we consider four available infrastructure service technologies; frame relay, asynchronous transfer mode (ATM), multiprotocol label switching (MPLS), and Carrier Ethernet. By researching each service and comparing the capabilities with the network project requirements, we identify that MPLS is suitable for Scenario A, and ATM is appropriate for Scenario B and Scenario C. This approach to infrastructure service selection may be generalized to apply to any network design scenario.

## Choosing the Right Network Technology

**Introduction**

As noted by Simon Kemp (2018), more than four billion people are using the Internet as of 2018. Companies utilize the Internet for communication, marketing, improving productivity, providing customer support, and cloud data storage, among other uses. The Internet is essentially a large wide area network (WAN). Smaller WANs that connect geographically separated business locations face issues with growing data volumes resulting from adoption of new technologies such as desktop virtualization, voice over Internet Protocol (VoIP), and video applications. Whether developed for desktop workstations, mobile devices, or other network host stations, these applications produce large volumes of network traffic, which leads to congestion and saturation of network links. The growing number of users who work remotely also contributes to stress on WANs. The need for more bandwidth is becoming paramount.

Furthermore, WAN security is a significant issue when many different people rely on information from remote computers and services. Protection against hackers and viruses means more complications and expense. Businesses or organizations turn towards special types of WAN technology or high-speed WAN alternatives to meet their needs. Among those services we can name faster switched networks schemes like frame relay, asynchronous transfer mode (ATM), multiprotocol label switching (MPLS), and Carrier Ethernet services. Each of these network services has advantages or disadvantages making them suitable for different use cases.

**Network Design Scenario Considerations**

*Scenario A* is a network connecting a large number of locations in a metropolitan area. At each location, real-time data transactions are expected to be sent and processed independently and randomly. To achieve real-time performance, delay must be kept to a minimum. The data volumes are expected to be modest, but transfer rates may reach several megabits per second (Mbps).

*Scenario B* is a WAN that interconnects six or more locations in remote areas across the United States. In this case, transmission facilities are varied but include radio links, satellite links, and phone links using modems.

*Scenario C* is a multimedia application network servicing a small number of locations. The applications include image sharing and real-time audio and video services. Other data services may be interspersed as well. High volumes of traffic are expected to require transfer rates in gigabits per second (Gbps) ranges. Although only a few locations will be connected, a large number of virtual circuits will be needed to accommodate many users and the large sized nature of the multimedia data.

We consider these four notable services as options for three network design scenarios:

*Frame relay* is "a data link layer, digital packet switching network protocol technology designed to connect local area networks (LANs) and transfer data across wide area networks" (Mitchell, 2018, para. 1). As Packet Lab (2010) describes, frame relay sends data in variable-sized units called *frames*, and relies on endpoints to provide error-correction. This speeds transmission but leaves the endpoints responsible for detecting and retransmitting dropped frames. While frame relay is a cost-effective method it is no longer considered one of the top methods to utilize.

*ATM* is "a telecommunication concept, developed for the data link layer, to carry all sorts of different kinds of data such as web traffic, voice, video, etc. while providing QoS (Quality of Service) at the same time," (Shekhar, 2017, para. 1). A network based on ATM achieves the ability to transfer this variety of traffic types through its use of logical connections through virtual paths and virtual channels (Stallings & Case, 2013, p. 467).

*Multiprotocol label switching (MPLS)* is "a way to insure reliable connections for real-time applications" (Weinberg & Johnson, 2018, para. 1). MPLS is much more expensive than many other options and is commonly used with offices, big networks, and any place that needs quality of service with real-time applications. "MPLS is a service that must be purchased from a carrier and is far more expensive than sending traffic over the public internet," (Weinberg & Johnson, 2018, para. 23).

*Carrier Ethernet* is a way to extend Ethernet as we know it. Carrier Ethernet "enables a variety of network services that can be sold to both other carriers (wholesale) and end users (retail). However, it isn't just for carriers -- it's a feature-rich solution perfect for all network operators (carriers, enterprises, and government) who provide networking services to end users, both internally and externally" (Hawkins, 2016, para. 6). Carrier Ethernet services are lower cost solutions but are typically faster than ATM and frame relay.

**Recommendations**

For *Scenario A*, we suggest using MPLS due to its reliability and performance for use with real-time applications. While this can be more of an expensive option than the others, it has the most reliability for real-time performance. Since each location has a large number of these real-time transactions that are to be processed, this component is very important.

For *Scenario B*, we must account for the nature of the remote locations with reliance on various transmission media, including radio, satellite, and telephone links. Given the modest data rates supported by these transmission links, ATM would be a good choice for the underlying communications technology in this WAN scenario. As Stallings and Case (2013) have observed, the relatively small, fixed size cells used in ATM communication offer several advantages, including data prioritization, efficient cell switching, and simple implementation of the switching mechanism in hardware (p. 465). Also, ATM supports both real-time and non-real-time service at constant or variable frame rates, and the recent addition of a guaranteed frame rate (GFR) service category enables the optimization of traffic passing from a LAN router onto a backbone network using ATM (Stallings & Case, 2013). These advantages make ATM an excellent choice for a national WAN. Multiprotocol label switching (MPLS) technology could also be used in this scenario, as it has many of the same advantages as ATM, with similar use of virtual logical connections and an ability to support a wide variety of traffic (Stallings & Case, 2013, p. 470). MPLS also adds the ability to create virtual private networks (VPNs) for enhanced privacy (Stallings & Case, 2013, p. 472-473). However, without additional privacy as a requirement, MPLS is not necessary on our WAN. MPLS is designed to take advantage of modern optical networks with higher data rates of 40 Gbps or more, which are not available in the infrastructure of this WAN.

In *Scenario C*, we must accommodate multimedia applications. In this case, we recommend asynchronous transfer mode (ATM).  ATM is the best fit for any real time data transfer and multimedia data transfer like audio and video. Because when we are seeing video it is very important to receive the next frame of data on time, otherwise the video will break or stop.  The ATM layer multiplexes cells over the physical link. The major function of this layer is to complete the ATM cell structure and set up the cell streams for transmissions of outgoing process, receive the incoming cells, and send them to the corresponding stream. The cells are distinguished by the virtual channel identifier (VCI) and virtual path identifier (VPI) in the cell header. A table in the switch helps the ATM layer place the cell in the appropriate output link. A generic flow control is used for media access by the user network interface to control the amount of traffic entering the network (N.J. Muller, 1996). Interactive multimedia applications, unlike traditional data transfer applications, have stringent simultaneous requirements in terms of loss and delay jitter due to the nature of audiovisual information. In addition, such stream-based applications deliver data at a variable rate, particularly when a constant quality is required. ATM can integrate traffic of different natures within a single network creating interactions of different types that reduce delay jitter and loss. Traditional protocol layers do not have the appropriate mechanisms to provide the required network quality of service (QoS) for such interactive variable bit rate (VBR) multimedia multipoint applications (Adanez, Francisco, & Hubaux, 1998). This lack of functionality calls for the design of protocol layers with the appropriate functions to handle the stringent requirements of multimedia. 

**Conclusion**

For each of the three network design scenarios, we have determined a recommended infrastructure service technology. Careful consideration of the requirements for each individual scenario is a critical aspect of selecting an underlying technology that will meet the needs of the eventual end users. By investigating several available services and weighing their capabilities against those requirements, we can recommend a suitable solution. Using this method of analysis improves the chances of success when the network is fully implemented. Identifying the requirements, researching the available technologies, documenting the results, and providing a detailed recommendation is an approach that can be applied to any network design scenario.

# References

Adda, M., Peart, A., & Wakins, N. (2006). Quality of service in wireless ATM for high demand multimedia applications. Retrieved from https://researchportal.port.ac.uk/portal/en/publications/quality-of-service-in-wireless-atm-for-high-demand-multimedia-applications(c50ae2a2-a003-494e-a77a-9d27c1e280d4).html

Garcia A., Francisco, J., & Hubaux, J. (1998). Designing a new network adaptation and ATM adaptation layers for interactive multimedia applications. Retrieved from https://infoscience.epfl.ch/record/32259?ln=en

Hawkins, J. (2016). Ethernet vs. carrier ethernet: The new network party line. Retrieved from https://www.ciena.com/insights/articles/Ethernet-vs-Carrier-Ethernet-The-New-Network-Party-Line_prx.html

Kemp, S. (2018). Digital in 2018: World's Internet users pass the 4 billion mark. Retrieved from https://wearesocial.com/blog/2018/01/global-digital-report-2018

Mitchell, B. (2018). Frame relay packet switching technology. Retrieved from https://www.lifewire.com/definition-of-frame-relay-817947

Packet Lab. \[packetlab\]. (2010, July 22). Frame Relay - Introduction and Concepts - Part 1 of 4 \[Video File\]. Retrieved from https://www.youtube.com/watch?v=FWZgqUDQc0c

Rajkumar, T. M., & Haldar, A. (1996). Multimedia networking technologies. Retrieved from http://www.ittoday.info/AIMS/Information_Management/504151.pdf

Saha, D. (1998). Supporting distributed multimedia applications on ATM networks. Retrieved from https://drum.lib.umd.edu/handle/1903/756

Shekhar, A. ATM in computer networks: History and basic concepts. (2017). Retrieved from https://fossbytes.com/atm-asynchronous-transfer-mode-history-basic-concepts/

Stallings, W., & Case, T. (2013). In *Business data communications: Infrastructure, networking, and security* (pp. 465-473). Boston: Pearson Education, Inc.

Weinberg, N., & Johnson, J. T. (2018). MPLS explained. Retrieved from https://www.networkworld.com/article/2297171/sd-wan/network-security-mpls-explained.html


<!-- Body (End) -->

<!-- Footer (Start) -->

# Author

### Aaron Martinez

- GitHub: <https://github.com/martinezcode/>
- LinkedIn: <https://www.linkedin.com/in/martinezcode/>

### With Adam Bessler, Amanda Fasano, Jamario Kelly, Naomi See, & Norbert Youtat Tankeu (Bellevue University)

<!-- Footer (End) -->