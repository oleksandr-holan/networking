# OSI

## IP Packet Fields

1. **Version**: Indicates whether the packet is IPv4 (value 4) or IPv6 (value 6). This determines how the rest of the header is interpreted.

2. **Header Length**: Specifies the length of the IP header in 32-bit words. Typical value is 5 (for a 20-byte header with no options).

3. **Type of Service/DSCP (Differentiated Services Code Point)**: Used to specify how the packet should be handled in terms of priority, delay, throughput, and reliability. Modern networks use this field for QoS (Quality of Service).

4. **Total Length**: The entire size of the IP packet in bytes, including both header and data.

5. **Identification**: A unique identifier assigned to packet fragments belonging to the same original IP datagram, used in reassembly.

6. **Flags**: Control and identify fragments:
   - Bit 0: Reserved (always 0)
   - Bit 1: Don't Fragment (DF)
   - Bit 2: More Fragments (MF)

7. **Fragment Offset**: Indicates where in the original datagram this fragment belongs, measured in 8-byte units.

8. **Time to Live (TTL)**: Prevents packets from circulating indefinitely. Each router decrements this value by at least 1; when it reaches 0, the packet is discarded.

9. **Protocol**: Identifies the next level protocol used in the data portion (e.g., 6 for TCP, 17 for UDP).

10. **Header Checksum**: Error-detection mechanism for the header only. Recalculated at each hop as TTL changes.

11. **Source IP Address**: The 32-bit IP address of the sender.

12. **Destination IP Address**: The 32-bit IP address of the intended recipient.

13. **IP Options**: Optional field that can contain various control information. Not commonly used in regular traffic.

## TCP Packet Fields

1. **Source Port**:
   - **Description**: 16-bit number identifying the sending application/process on the source host.
   - **Purpose**: Identifies the sending application/process.
   - **Usage**: Allows the receiving host to direct responses back to the correct application. When the destination host replies, it uses this as the destination port.

2. **Destination Port**:
   - **Description**: 16-bit number identifying the receiving application/process on the destination host.
   - **Purpose**: Identifies the intended receiving application/process.
   - **Usage**: Directs incoming packets to the correct service/application (e.g., port 80 for HTTP, 443 for HTTPS). Essential for multiplexing multiple connections on a single host.

3. **Sequence Number**:
   - **Description**: 32-bit value that identifies the byte in the stream of data from the sending TCP to the receiving TCP that the first byte of data in this segment represents.
   - **Purpose**: Tracks the ordering of data bytes in a TCP stream.
   - **Usage**: Enables the receiver to reassemble data in the correct order and detect missing segments. During connection establishment (SYN), it contains the initial sequence number (ISN).

4. **Acknowledgment Number**:
   - **Description**: 32-bit value that contains the next sequence number that the sender of the acknowledgment expects to receive.
   - **Purpose**: Confirms receipt of data.
   - **Usage**: Tells the sender which byte the receiver expects next, implicitly acknowledging all previous bytes. Critical for TCP's reliability mechanism.

5. **Data Offset/Header Length**:
   - **Description**: 4-bit value that specifies the size of the TCP header in 32-bit words.
   - **Purpose**: Indicates where the header ends and data begins.
   - **Usage**: Necessary because the TCP header can vary in length due to optional fields.

6. **Reserved**:
   - **Description**: 6 bits reserved for future use; should be set to zero.
   - **Purpose**: Reserved for future protocol extensions.
   - **Usage**: Must be set to zero; ensures backward compatibility if new features are added.

7. **Control Flags**:
   - **Description**: 6 individual bits that control the connection:
     - URG: Urgent Pointer field is significant
     - ACK: Acknowledgment field is significant
     - PSH: Push function (deliver data to the application immediately)
     - RST: Reset the connection
     - SYN: Synchronize sequence numbers (used during connection establishment)
     - FIN: No more data from sender (used during connection termination)
   - **Purpose**: Control connection state and data handling.
   - **Usage**:
     - **URG**: Marks data as urgent, needing immediate attention.
     - **ACK**: Indicates the acknowledgment number is valid.
     - **PSH**: Tells the receiver to deliver data to the application immediately without buffering.
     - **RST**: Abruptly terminates a connection when an error occurs.
     - **SYN**: Establishes connections by synchronizing sequence numbers.
     - **FIN**: Gracefully closes connections when transmission is complete.

8. **Window Size**:
   - **Description**: 16-bit value that specifies the number of bytes the sender is willing to accept.
   - **Purpose**: Implements flow control.
   - **Usage**: Indicates how many bytes the receiver can accept, preventing sender from overwhelming receiver's buffer.

9. **Checksum**:
   - **Description**: 16-bit error-detection mechanism covering the header and data.
   - **Purpose**: Detects corruption in the TCP segment.
   - **Usage**: Receiver calculates its own checksum and compares it to this value; if they differ, the segment is discarded.

10. **Urgent Pointer**:
    - **Description**: 16-bit value that points to the sequence number of the byte following the urgent data (only valid if URG flag is set).
    - **Purpose**: Points to urgent data in the segment.
    - **Usage**: When URG flag is set, indicates the position of urgent data that should be processed immediately.

11. **Options**:
    - **Description**: Variable length field that can include:
      - Maximum Segment Size (MSS)
      - Window Scale
      - Selective Acknowledgment (SACK)
      - Timestamps
      - And others
    - **Purpose**: Extends TCP functionality.
    - **Usage**:
      - **MSS**: Negotiates maximum segment size to avoid fragmentation.
      - **Window Scale**: Allows larger receive windows than 65,535 bytes.
      - **SACK**: Permits selective acknowledgment of non-contiguous blocks.
      - **Timestamps**: Measures round-trip time and protects against wrapped sequence numbers.

12. **Padding**:
    - **Description**: Extra zero bits added to ensure the TCP header ends on a 32-bit boundary.
    - **Purpose**: Ensures proper alignment.
    - **Usage**: Makes the header end on a 32-bit boundary for efficient processing by hardware and software.

## HTTP

The Host listed under the HTTP section of the PDU Details would be "www.osi.local". This information is part of the HTTP header, which is associated with Layer 7 (Application Layer) of the OSI Model.

The Host field in an HTTP request header specifies the domain name of the server being requested, which in this case is the web server the client is trying to access. This information is crucial for the web server to determine which website to serve, especially when multiple websites are hosted on the same server (virtual hosting).

## Questions and Answers

For the last colored square box under the Info column, there would be two tabs displayed:

1. OSI Model tab
2. Inbound PDU Details tab

This is because this event represents the final packet in the communication stream (the last HTTP response from the server to the client). Since this is the end of the transmission, there is no "Outbound PDU Details" tab because the device is only receiving data at this point, not sending any. The simulation shows only the inbound information as the web page data is delivered to the client, completing the HTTP transaction.

**What information is listed in the NAME field: in the DNS QUERY section?**

NAME (VARIABLE LENGTH):www.osi.local

### 1e. Click the last DNS Info colored square box in the event list

**At which device was the PDU captured?**

Web Client

**What is the value listed next to ADDRESS: in the DNS ANSWER section of the Inbound PDU Details?**

IP:192.168.1.254

### 1f. Find the first HTTP event in the list and click the colored square box of the TCP event immediately following this event. Highlight Layer 4 in the OSI Model tab

**In the numbered list directly below the In Layers and Out Layers, what is the information displayed
under items 4 and 5?**

> The TCP connection is successful.
> The device sets the connection state to ESTABLISHED.

### 1g. Click the last TCP event. Highlight Layer 4 in the OSI Model tab. Examine the steps listed directly below In Layers and Out Layers

**What is the purpose of this event, based on the information provided in the last item in the list (should be
item 4)?**

> Sent segment information: the sequence number 103, the ACK number 273, and the data length 20.

### Challenge Questions

This simulation provided an example of a web session between a client and a server on a local area network
(LAN). The client makes requests to specific services running on the server. The server must be set up to
listen on specific ports for a client request. (Hint: Look at Layer 4 in the OSI Model tab for port information.)

Based on the information that was inspected during the Packet Tracer capture, what port number is the Web
Server listening on for the web request?
Type your answers here.
What port is the Web Server listening on for a DNS request?
