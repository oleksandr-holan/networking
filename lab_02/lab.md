# Packet Tracer - Investigate the TCP/IP and OSI Models in Action

## Objectives

- Part 1: Examine HTTP Web Traffic
- Part 2: Display Elements of the TCP/IP Protocol Suite

## Background

This simulation activity provides a foundation for understanding the TCP/IP protocol suite and its relationship to the OSI model. Simulation mode allows you to view the data contents being sent across the network at each layer.

As data moves through the network, it's broken down into smaller pieces and identified so they can be reassembled at the destination. Each piece is assigned a specific name (protocol data unit [PDU]) and associated with a specific layer of the TCP/IP and OSI models. Packet Tracer simulation mode enables you to view each layer and the associated PDU.

## Instructions

### Part 1: Examine HTTP Web Traffic

#### Step 1: Switch from Realtime to Simulation mode

a. Click the Simulation mode icon to switch from Realtime mode to Simulation mode.
b. Select HTTP from the Event List Filters.

   1) HTTP may already be the only visible event. If necessary, click the Edit Filters button to display available events.
   2) Click the Show All/None check box until all boxes are cleared and then select HTTP from the Misc tab. Close the Edit Filters window.

#### Step 2: Generate web (HTTP) traffic

a. Click Web Client in the far left pane.
b. Click the Desktop tab and click the Web Browser icon to open it.
c. In the URL field, enter <www.osi.local> and click Go.
d. Click Capture/Forward four times. There should be four events in the Event List.

**Question:**

Look at the Web Client web browser page. Did anything change?

> Yes, the web page loaded and displayed content from the OSI Model website

#### Step 3: Explore the contents of the HTTP packet

a. Click the first colored square box under the Event List > Type column.
b. Ensure that the OSI Model tab is selected. Under the Out Layers column, click Layer 7.

**Questions:**

What information is listed in the numbered steps directly below the In Layers and Out Layers boxes for Layer 7?

> The HTTP client sends a HTTP request to the server.

What is the Dst Port value for Layer 4 under the Out Layers column?

> 80

What is the Dest. IP value for Layer 3 under the Out Layers column?

> 192.168.1.254

What information is displayed at Layer 2 under the Out Layers column?

> 1. The next-hop IP address is a unicast. The ARP process looks it up in the ARP table.
> 2. The next-hop IP address is in the ARP table. The ARP process sets the frame's destination MAC address to the one found in the table.
> 3. The device encapsulates the PDU into an Ethernet frame.

c. Click the Outbound PDU Details tab.

**Questions:**

What is the common information listed under the IP section of PDU Details as compared to the information listed under the OSI Model tab? With which layer is it associated?

> The source and destination IP addresses (192.168.1.1 and 192.168.1.254) are common between both views. This information is associated with Layer 3 (Network Layer).

What is the common information listed under the TCP section of PDU Details, as compared to the information listed under the OSI Model tab, and with which layer is it associated?

> The source and destination port numbers are common between both views. This information is associated with Layer 4 (Transport Layer).

What is the Host listed under the HTTP section of the PDU Details? What layer would this information be associated with under the OSI Model tab?

> The Host is "www.osi.local". This information is associated with Layer 7 (Application Layer).

d. Click the next colored square box under the Event List > Type column.

e. Advance to the next HTTP Type box within the Event List and click the colored square box.

**Question:**

Comparing the information displayed in the In Layers column with that of the Out Layers column, what are the major differences?

> The major differences are that the source and destination information is reversed. In the In Layers, the source is the web server (192.168.1.254) and the destination is the client (192.168.1.1), while in the Out Layers, the source is the client and the destination is the server. The port numbers are also reversed, with the server using port 80 and the client using a dynamic port (like 1025). Also, in the In Layers the information in decapsulated and in the Out Layers encapsulated

f. Click the Inbound and Outbound PDU Details tab. Review the PDU details.

g. Click the last colored square box under the Info column.

**Question:**

How many tabs are displayed with this event? Explain.

> Two tabs are displayed: OSI Model tab and Inbound PDU Details tab. This is because this event represents the final packet in the communication stream (the last HTTP response from the server to the client). Since this is the end of the transmission, there is no "Outbound PDU Details" tab because the device is only receiving data at this point, not sending any.

### Part 2: Display Elements of the TCP/IP Protocol Suite

#### Step 1: View Additional Events

a. Close any open PDU information windows.

b. In the Event List Filters > Visible Events section, click Show All/None.

**Question:**
What additional Event Types are displayed?

> Additional Event Types displayed include DNS, ARP, and TCP events. These protocols play various roles in the TCP/IP suite: ARP resolves IP addresses to MAC addresses, DNS resolves domain names to IP addresses, and TCP manages connection establishment, data transfer, and connection termination.

c. Click the first DNS event in the Type column. Explore the OSI Model and PDU Detail tabs.
d. Click the Outbound PDU Details tab.

**Question:**
What information is listed in the NAME field: in the DNS QUERY section?

> NAME (VARIABLE LENGTH): <www.osi.local>

e. Click the last DNS Info colored square box in the event list.

**Questions:**
At which device was the PDU captured?

> Web Client

What is the value listed next to ADDRESS: in the DNS ANSWER section of the Inbound PDU Details?

> IP: 192.168.1.254

f. Find the first HTTP event in the list and click the colored square box of the TCP event immediately following this event. Highlight Layer 4 in the OSI Model tab.

**Question:**
In the numbered list directly below the In Layers and Out Layers, what is the information displayed under items 4 and 5?

> The TCP connection is successful.
> The device sets the connection state to ESTABLISHED.

g. Click the last TCP event. Highlight Layer 4 in the OSI Model tab.

**Question:**
What is the purpose of this event, based on the information provided in the last item in the list (should be item 4)?

> The purpose of this event is to terminate the TCP connection.

## Challenge Questions

This simulation provided an example of a web session between a client and a server on a local area network (LAN). The client makes requests to specific services running on the server. The server must be set up to listen on specific ports for a client request. (Hint: Look at Layer 4 in the OSI Model tab for port information.)

Based on the information that was inspected during the Packet Tracer capture, what port number is the Web Server listening on for the web request?

> Port 80 (the standard HTTP port)

What port is the Web Server listening on for a DNS request?

> Port 53 (the standard DNS port)
