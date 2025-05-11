# Lab - Use Wireshark to View Network Traffic

## Topology

## Objectives

- Part 1: Capture and Analyze Local ICMP Data in Wireshark
- Part 2: Capture and Analyze Remote ICMP Data in Wireshark

## Background / Scenario

Wireshark is a software protocol analyzer, or "packet sniffer" application, used for network troubleshooting, analysis, software and protocol development, and education. As data streams travel back and forth over the network, the sniffer "captures" each protocol data unit (PDU) and can decode and analyze its content according to the appropriate RFC or other specifications.

Wireshark is a useful tool for anyone working with networks and can be used with most labs in the CCNA courses for data analysis and troubleshooting. In this lab, you will use Wireshark to capture ICMP data packet IP addresses and Ethernet frame MAC addresses.

## Required Resources

- 1 PC (Windows with internet access)
- Additional PCs on a local-area network (LAN) will be used to reply to ping requests.

Using a packet sniffer such as Wireshark may be considered a breach of the security policy of the school. It is recommended that permission be obtained before running Wireshark for this lab. If using a packet sniffer such as Wireshark is an issue, the instructor may wish to assign the lab as homework or perform a walk-through demonstration.

## Instructions

### Part 1: Capture and Analyze Local ICMP Data in Wireshark

In Part 1 of this lab, you will ping another PC on the LAN and capture ICMP requests and replies in Wireshark. You will also look inside the frames captured for specific information. This analysis should help to clarify how packet headers are used to transport data to their destination.

#### Step 1: Retrieve your PC interface addresses

For this lab, you will need to retrieve your PC IP address and its network interface card (NIC) physical address, also called the MAC address.

Open a Windows command prompt.

a. In a command prompt window, enter `ipconfig /all`, to the IP address of your PC interface, its description, and its MAC (physical) address.

```text
C:\Users\Student> ipconfig /all
Windows IP Configuration
Host Name . . . . . . . . . . . . : DESKTOP-NB48BTC
Primary Dns Suffix . . . . . . . :
Node Type . . . . . . . . . . . . : Hybrid
IP Routing Enabled. . . . . . . . : No
WINS Proxy Enabled. . . . . . . . : No
Ethernet adapter Ethernet:
Connection-specific DNS Suffix . :
Description . . . . . . . . . . . : Intel(R) 82577LM Gigabit Network Connection
Physical Address. . . . . . . . . :00-26-B9-DD-00-91
DHCP Enabled. . . . . . . . . . . : No
Autoconfiguration Enabled . . . . : Yes
Link-local IPv6 Address . . . . . : fe80::d809:d939:110f:1b7f%20(Preferred)
IPv4 Address. . . . . . . . . . . : 192.168.1.147(Preferred)
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.1.1
<output omitted>
```

b. Ask a team member or team members for their PC IP address and provide your PC IP address to them. Do not provide them with your MAC address at this time.

Close a Windows Command Prompt.

#### Step 2: Start Wireshark and begin capturing data

a. Navigate to Wireshark. Double-click the desired interface to start the packet capture. Make sure the desired interface has traffic.

b. Information will start scrolling down the top section in Wireshark. The data lines will appear in different colors based on protocol.

This information can scroll by very quickly depending on what communication is taking place between your PC and the LAN. We can apply a filter to make it easier to view and work with the data that is being captured by Wireshark.

For this lab, we are only interested in displaying ICMP (ping) PDUs. Type `icmp` in the Filter box at the top of Wireshark and press Enter, or click the Apply button (arrow sign) to view only ICMP (ping) PDUs.

c. This filter causes all data in the top window to disappear, but you are still capturing the traffic on the interface. Navigate to a command prompt window and ping the IP address that you received from your team member.

```powershell
C:\> ping 192.168.1.114
Pinging 192.168.1.114 with 32 bytes of data:
Reply from 192.168.1.114: bytes=32 time<1ms TTL=128
Reply from 192.168.1.114: bytes=32 time<1ms TTL=128
Reply from 192.168.1.114: bytes=32 time<1ms TTL=128
Reply from 192.168.1.114: bytes=32 time<1ms TTL=128
Ping statistics for 192.168.1.114:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

Notice that you start seeing data appear in the top window of Wireshark again.

Note: If the PC of your team member does not reply to your pings, this may be because the PC firewall of the team member is blocking these requests. Please see Appendix A: Allowing ICMP Traffic Through a Firewall for information on how to allow ICMP traffic through the firewall using Windows.

d. Stop capturing data by clicking the Stop Capture icon.

#### Step 3: Examine the captured data

In Step 3, examine the data that was generated by the ping requests of your team member PC. Wireshark data is displayed in three sections:

1) The top section displays the list of PDU frames captured with a summary of the IP packet information listed
2) The middle section lists PDU information for the frame selected in the top part of the screen and separates a captured PDU frame by its protocol layers
3) The bottom section displays the raw data of each layer. The raw data is displayed in both hexadecimal and decimal form.

a. Click the first ICMP request PDU frames in the top section of Wireshark. Notice that the Source column has your PC IP address, and the Destination column contains the IP address of the teammate PC that you pinged.

b. With this PDU frame still selected in the top section, navigate to the middle section. Click the plus sign to the left of the Ethernet II row to view the destination and source MAC addresses.

**Questions:**

- Does the source MAC address match your PC interface?

ipconfig /all

```txt
Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Realtek PCIe GbE Family Controller
   Physical Address. . . . . . . . . : 00-D8-61-19-63-EE
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::72ea:3100:c2e1:6b46%18(Preferred)
   IPv4 Address. . . . . . . . . . . : 192.168.31.189(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Lease Obtained. . . . . . . . . . : 10 травня 2025 р. 11:51:37
   Lease Expires . . . . . . . . . . : 11 травня 2025 р. 5:51:36
   Default Gateway . . . . . . . . . : 192.168.31.1
   DHCP Server . . . . . . . . . . . : 192.168.31.1
   DHCPv6 IAID . . . . . . . . . . . : 100718689
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-2D-AD-32-C3-00-D8-61-19-63-EE
   DNS Servers . . . . . . . . . . . : 8.8.8.8
                                       8.8.4.4
   NetBIOS over Tcpip. . . . . . . . : Enabled
```

Wireshark

```txt
Ethernet II, Src: MicroStarINT_19:63:ee (00:d8:61:19:63:ee), Dst: Apple_d3:bd:6d (38:f9:d3:d3:bd:6d)
```

- Does the destination MAC address in Wireshark match your team member MAC address?

Teammember's ifconfig

```txt
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
options=6460<TSO4,TSO6,CHANNEL_IO,PARTIAL_CSUM,ZEROINVERT_CSUM>
ether 38:f9:d3:d3:bd:6d
inet6 fe80::27:bf62:2076:bbe1%en0 prefixlen 64 secured scopeid 0x7 
inet 192.168.31.34 netmask 0xffffff00 broadcast 192.168.31.255
nd6 options=201<PERFORMNUD,DAD>
media: autoselect
status: active
```

Wireshark

```txt
Ethernet II, Src: MicroStarINT_19:63:ee (00:d8:61:19:63:ee), Dst: Apple_d3:bd:6d (38:f9:d3:d3:bd:6d)
```

- How is the MAC address of the pinged PC obtained by your PC?

Note: In the preceding example of a captured ICMP request, ICMP data is encapsulated inside an IPv4 packet PDU (IPv4 header) which is then encapsulated in an Ethernet II frame PDU (Ethernet II header) for transmission on the LAN.

### Part 2: Capture and Analyze Remote ICMP Data in Wireshark

In Part 2, you will ping remote hosts (hosts not on the LAN) and examine the generated data from those pings. You will then determine what is different about this data from the data examined in Part 1.

#### Step 1: Start capturing data on the interface

a. Start the data capture again.

b. A window prompts you to save the previously captured data before starting another capture. It is not necessary to save this data. Click Continue without Saving.

c. With the capture active, ping the following three website URLs from a Windows command prompt:

Open a Windows command prompt

1) <www.yahoo.com>
2) <www.cisco.com>
3) <www.google.com>

Note: When you ping the URLs listed, notice that the Domain Name Server (DNS) translates the URL to an IP address. Note the IP address received for each URL.

d. You can stop capturing data by clicking the Stop Capture icon.

#### Step 2: Examining and analyzing the data from the remote hosts

Review the captured data in Wireshark and examine the IP and MAC addresses of the three locations that you pinged. List the destination IP and MAC addresses for all three locations in the space provided.

**Questions:**

- IP address for <www.yahoo.com>: 87.248.119.252
- MAC address for <www.yahoo.com>: 88:c3:97:e0:35:ae
- IP address for <www.cisco.com>: 104.91.49.38:
- MAC address for <www.cisco.com>: 88:c3:97:e0:35:ae
- IP address for <www.google.com>: 142.250.203.196
- MAC address for <www.google.com>: 88:c3:97:e0:35:ae
- What is significant about this information? - The MAC addresses are the same
- How does this information differ from the local ping information you received in Part 1? - We don't see the actul MAC address of the destination hosts

Close the Windows command prompt

## Reflection Question

Wireshark shows the actual MAC addresses of local hosts but not remote hosts because MAC addresses only function at Layer 2 (Data Link layer) and are only relevant within a single network segment. When a computer communicates with a remote host on the internet, packets are addressed at Layer 2 to the default gateway (router), not to the final destination. As packets travel across the internet, they are stripped of their original Layer 2 information and re-encapsulated with new MAC addresses at each router hop. Therefore, what Wireshark captures is the MAC address of the local router (for outgoing packets to remote hosts), not the actual MAC address of the remote destination, which exists many network segments away and is never directly visible to the local network interface.

## Appendix A: Allowing ICMP Traffic Through a Firewall

If the members of your team are unable to ping your PC, the firewall may be blocking those requests. This appendix describes how to create a rule in the firewall to allow ping requests. It also describes how to disable the new ICMP rule after you have completed the lab.

### Part 1: Create a new inbound rule allowing ICMP traffic through the firewall

a. Navigate to the Control Panel and click the System and Security option in the Category view.

b. In the System and Security window, click Windows Defender Firewall or Windows Firewall.

c. In the left pane of the Windows Defender Firewall or Windows Firewall window, click Advanced settings.

d. On the Advanced Security window, click the Inbound Rules option on the left sidebar and then click New Rule… on the right sidebar.

e. This launches the New Inbound Rule wizard. On the Rule Type screen, click the Custom radio button and click Next.

f. In the left pane, click the Protocol and Ports option and using the Protocol Type drop-down menu, select ICMPv4, and then click Next.

g. Verify that Any IP address for both the local and remote IP addresses are selected. Click Next to continue.

h. Select Allow the connection. Click Next to continue.

i. By default, this rule applies to all the profiles. Click Next to continue.

j. Name the rule with Allow ICMP Requests. Click Finish to continue. This new rule should allow your team members to receive ping replies from your PC.

### Part 2: Disabling or deleting the new ICMP rule

After the lab is complete, you may want to disable or even delete the new rule you created in Step 1. Using the Disable Rule option allows you to enable the rule again at a later date. Deleting the rule permanently deletes it from the list of inbound rules.

a. On the Advanced Security window, click Inbound Rules in the left pane and then locate the rule you created previously.

b. Right-click the ICMP rule and select Disable Rule if so desired. You may also select Delete if you want to permanently delete it. If you choose this option, you must re-create the rule again to allow ICMP replies.
