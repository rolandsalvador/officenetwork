<h1>Small Office Network (Part 1) - Created From Scratch</h1>

<h2>Description</h2>
This repository is the first part of two in my small office network project. Part one is creating the network from scratch, and <a href="https://github.com/rolandsalvador/officenetwork2">part two</a> is configuring the network to use the many protocols and services required in an office. 
<br />
<br />
The network is a two-tier, or collapsed core, design with a PC, laptop, phone, server, wireless LAN controller, and lightweight access point. The full topology can be seen below.
<br />
<br />
<img src="https://i.imgur.com/RuzVqm3.png"/>
I wanted to put my networking knowledge to the test after obtaining my Cisco Certified Network Associate (CCNA) certification. Though the CCNA exam had practical questions that required me to apply what I learned, I wanted to take it one step further by designing a network from the ground up and configure it as if it were a real small office network. Thank you for taking a look, and please make sure to check out <a href="https://github.com/rolandsalvador/officenetwork2">part 2</a> after!

<h2>Skills Used</h2>

- <b>Network Fundamentals</b> 
- <b>Routing and Switching</b>
- <b>Subnetting</b>

<h2>Environments Used</h2>

- <b>Cisco Packet Tracer</b>

<h2>Contents</h2>

[1. Starting out](#1-starting-out)<br />
[2. Connecting interfaces](#2-connecting-interfaces)<br />
[3. Configuring IP addresses](#3-configuring-ip-addresses)<br />
[4. Ping test](#4-ping-test)<br />
[5. Add wireless router](#5-add-wireless-router)<br />
[6. Add Server1](#6-add-server1)<br />
[7. Configure default gateway and DNS addresses](#7-configure-default-gateway-and-dns-addresses)<br />
[8. Add cloud](#8-add-cloud)<br />
[9. Change the index.html file on Server1](#9-change-the-indexhtml-file-on-server1)<br />
[10. Configure DNS](#10-configure-dns)<br />
[11. Add router and internet](#11-add-router-and-internet)<br />
[12. Add distribution switches 1 and 2](#12-add-distribution-switches-1-and-2)<br />
[13. Add WLC and LWAP to access switch 1](#13-add-wlc-and-lwap-to-access-switch-1)<br />
[14. Add access switch 2 and IP phone](#14-add-access-switch-2-and-ip-phone)<br />
[15. Add access switch 3](#15-add-access-switch-3)<br />
[16. Add redundancy and clean up](#16-add-redundancy-and-clean-up)<br />
[17. Test connectivity](#17-test-connectivity)<br />
[Onto Part 2](#onto-part-2)<br />

<h2>Walkthrough</h2>

<h3>1. Starting out</h3>
To keep things simple, I started off with a switch, a PC, and a laptop. The network address will be 192.168.1.0 with a subnet mask of 255.255.255.0.
<br />
<br />
<img src="https://i.imgur.com/nBu8aXz.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>2. Connecting interfaces</h3>
For now, I connected PC1’s FastEthernet0 (FE0) interface to Switch1’s FastEthernet0/10 (F0/10) interface and Laptop1’s FE0 interface to Switch1’s F0/11 interface. This will change later as the network topology becomes more complex.
<br />
<br />
<img src="https://i.imgur.com/B945CSv.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>3. Configuring IP addresses</h3>
I set PC1’s IP address as 192.168.1.10 and Laptop1’s IP address as 192.168.1.11. I wanted to reserve the first 9 addresses for other devices.
<br />
<br />
<img src="https://i.imgur.com/n1FlG5V.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>4. Ping test</h3>
To test if this basic setup was working correctly, I pinged Laptop1 from PC1.
<br />
<br />
<img src="https://i.imgur.com/TtEbpfe.png"/>
The pings were successful, and we can see the packets traveling in simulation mode.
<br />
<br />
<img src="https://i.imgur.com/l4a02N8.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>5. Add wireless router</h3>
I added a wireless router to the network, Wireless Router1. I set its GigabitEthernet (GE1) interface IP address to 192.168.1.1, the first available host address on its subnet. For now, it will also act as the default gateway of the network.
<br />
<br />
I pinged Wireless Router1 from PC1 to check connectivity again, and it worked.
<br />
<br />
<img src="https://i.imgur.com/XQMDeee.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>6. Add Server1</h3>
Next, I added a server to the network, Server1. I set its FE0 interface IP address to 192.168.1.254, the last available host address on its subnet. It will act as the DNS server of the network.
<br />
<br />
<img src="https://i.imgur.com/NYsWwai.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>7. Configure default gateway and DNS addresses</h3>
On PC1 and Laptop1, I configured the default gateway as Wireless Router1’s address and the DNS server as Server1’s address.
<br />
<br />
<img src="https://i.imgur.com/RGrouRU.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>8. Add cloud</h3>
Next, I added a Cloud node. Wireless Router1 connects to the Cloud and acts as the barrier between the inside and outside network. The topology is starting to take shape.
<br />
<br />
<img src="https://i.imgur.com/VZ1489I.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>9. Change the index.html file on Server1</h3>
In the HTTP tab of Server1’s Services page, there is an index.html file that contains information to display when a client connects to Server1’s IP address. By default, generic Cisco information is displayed on the webpage. 
<br />
<br />
<img src="https://i.imgur.com/KmC4j9M.png"/>
I edited the code so that different information gets displayed. Note that Server1’s IP address, 192.168.1.254, is entered in the URL page on the web browser.
<br />
<br />
<img src="https://i.imgur.com/MvVe77C.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>10. Configure DNS</h3>
In the DNS tab of Server1’s Services page, I added an IPv4 A record to translate a test website to Server1’s IP address, 192.168.1.254.
<br />
<br />
<img src="https://i.imgur.com/oeZCwoi.png"/>
This time, I entered the test website to access Server1’s webpage, indicating that DNS is working properly.
<br />
<br />
<img src="https://i.imgur.com/CH8Q6Fi.png"/>
For good measure, I also sent a ping to the test website, which was successful.
<br />
<br />
<img src="https://i.imgur.com/oMdwBIo.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>11. Add router and internet</h3>
I replaced Wireless Router1 and Cloud with Router1 and an Internet node. Though Router1’s G0/2 address is set to 192.168.2.1/30 in the picture below, I changed it to 10.0.0.1/30 later on to avoid potential confusion while setting up the network.
<br />
<br />
<img src="https://i.imgur.com/bPX2K2F.png"/>
In the Internet node, I set up two more routers named ISP1 and ISP2. However, these routers are currently just for show. The focus of part 1 is on network creation, not connectivity, so this will suffice for now.
<br />
<br />
<img src="https://i.imgur.com/VLe8Rj5.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>12. Add distribution switches 1 and 2</h3>
Now that I’ve set up a basic network with endpoints, a switch, and a router, it’s time to implement the two-tier, collapsed core design. 
<br />
<br />
I added two multilayer switches, DSW1 and DSW2, to act as the distribution layer switches. There are two connections between them for redundancy, and both switches are connected to Router1 for further redundancy.
<br />
<br />
The original layer 2 switch has been renamed to ASW1, an access layer switch, for clarity. In addition, I kept track of all the different interface connections by putting labels on each one. If applicable, I included the IP address of the connection. 
<br />
<br />
<img src="https://i.imgur.com/XuJtZ3I.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>13. Add WLC and LWAP to access switch 1</h3>
Next, I connected a wireless LAN controller (WLC1) and a lightweight access point (LWAP1) to serve as our wireless portion of the office network. Laptop1 has been placed off to the side without it’s ethernet connection. These will be used when I configure wireless networks in the next part of the project.
<br />
<br />
<img src="https://i.imgur.com/xKvOX7k.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>14. Add access switch 2 and IP phone</h3>
Phone1 is placed between ASW2 and PC1 so that traffic between the two has to go through the phone first. This will be used when I configure IP phones and VLANs in the next part of the project.
<br />
<br />
<img src="https://i.imgur.com/eba564c.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>15. Add access switch 3</h3>
Finally, I added ASW3 and connected Server1 to it. The access layer is complete, and each of the endpoints are physically separated. In the next part of the project, I’ll be configuring all the VLANs so that they are also logically separated.
<br />
<br />
<img src="https://i.imgur.com/iVW1hEo.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)
  
<h3>16. Add redundancy and clean up</h3>
To add redundancy between the distribution and access layer, each access switch is connected to each distribution switch. I cleaned up the topology a bit so that it is a little clearer to see which interface is for which connection. 
<br />
<br />
<img src="https://i.imgur.com/eFmb1JO.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>17. Test connectivity</h3>
To finish off part 1 of the project, I double-checked whether connectivity still works in the network. From PC1, I pinged Router1, Server1, and the test website. All were successful, which completes the setup of the small office network!
<br />
<br />
<img src="https://i.imgur.com/bYc2dMY.png"/>

[Back to top](#small-office-network-part-1---created-from-scratch)

<h3>Onto Part 2</h3>
This portion of the project was already getting lengthy, so I decided to split the configuration into a part 2, which can be found 
<a href="https://github.com/rolandsalvador/officenetwork2">here</a>. 
Please make sure to check it out, because that’s where the fun really starts. I’ll be configuring VLANs, DHCP, NAT, STP, OSPF, SSH, and much more!
<br />
<br />

[Back to top](#small-office-network-part-1---created-from-scratch)
