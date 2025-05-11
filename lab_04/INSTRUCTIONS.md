# Step-by-Step Guide: MAC Address Table Lab in Packet Tracer

## Part 1: Building the Network in Packet Tracer

### Step 1: Create the topology

1. Open Cisco Packet Tracer
2. Add two 2960 switches to the workspace (found in the "Switches" category)
3. Add two PCs to the workspace (found in the "End Devices" category)
4. Connect the devices with appropriate cables:
   - Connect PC-A to S1 using a straight-through copper cable
   - Connect PC-B to S2 using a straight-through copper cable
   - Connect S1 to S2 using a straight-through copper cable (F0/1 to F0/1)

### Step 2: Configure PC IP addresses

1. Click on PC-A → Desktop tab → IP Configuration
   - Set IP address: 192.168.1.1
   - Set Subnet Mask: 255.255.255.0
   - Leave Default Gateway blank (not needed for this lab)

2. Click on PC-B → Desktop tab → IP Configuration
   - Set IP address: 192.168.1.2
   - Set Subnet Mask: 255.255.255.0
   - Leave Default Gateway blank

### Step 3: Configure the switches

1. Configure S1:
   - Click on S1 → CLI tab
   - Enter the following commands:

   ```cli
   # Enter privileged EXEC mode
   enable
   
   # Enter global configuration mode
   configure terminal
   
   # Set the switch name to S1
   hostname S1
   
   # Enter VLAN 1 interface configuration mode
   interface vlan 1
   
   # Assign IP address and subnet mask to VLAN 1
   ip address 192.168.1.11 255.255.255.0
   
   # Enable the VLAN 1 interface
   no shutdown
   
   # Return to global configuration mode
   exit
   
   # Enter console line configuration mode
   line console 0
   
   # Set console password to "cisco"
   password cisco
   
   # Enable password checking at login
   login
   
   # Return to global configuration mode
   exit
   
   # Enter vty (Telnet/SSH) line configuration mode
   line vty 0 15
   
   # Set vty password to "cisco"
   password cisco
   
   # Enable password checking at login
   login
   
   # Return to global configuration mode
   exit
   
   # Set privileged EXEC password to "class"
   enable password class
   
   # Return to privileged EXEC mode
   exit
   ```

2. Configure S2:
   - Click on S2 → CLI tab
   - Enter the following commands:

   ```cli
   # Enter privileged EXEC mode
   enable
   
   # Enter global configuration mode
   configure terminal
   
   # Set the switch name to S2
   hostname S2
   
   # Enter VLAN 1 interface configuration mode
   interface vlan 1
   
   # Assign IP address and subnet mask to VLAN 1
   ip address 192.168.1.12 255.255.255.0
   
   # Enable the VLAN 1 interface
   no shutdown
   
   # Return to global configuration mode
   exit
   
   # Enter console line configuration mode
   line console 0
   
   # Set console password to "cisco"
   password cisco
   
   # Enable password checking at login
   login
   
   # Return to global configuration mode
   exit
   
   # Enter vty (Telnet/SSH) line configuration mode
   line vty 0 15
   
   # Set vty password to "cisco"
   password cisco
   
   # Enable password checking at login
   login
   
   # Return to global configuration mode
   exit
   
   # Set privileged EXEC password to "class"
   enable password class
   
   # Return to privileged EXEC mode
   exit
   ```

## Part 2: Examining the MAC Address Table

### Step 1: Record device MAC addresses

1. Record PC-A's MAC address:
   - Click on PC-A → Desktop tab → Command Prompt
   - Type `ipconfig /all` and press Enter
   - Note the Physical Address (MAC) of the Ethernet adapter

2. Record PC-B's MAC address:
   - Click on PC-B → Desktop tab → Command Prompt
   - Type `ipconfig /all` and press Enter
   - Note the Physical Address (MAC) of the Ethernet adapter

3. Record S1's interface MAC address:
   - Click on S1 → CLI tab
   - Type `enable` and press Enter
   - Type `show interface f0/1` and press Enter
   - Note the hardware address (MAC) from the output

4. Record S2's interface MAC address:
   - Click on S2 → CLI tab
   - Type `enable` and press Enter
   - Type `show interface f0/1` and press Enter
   - Note the hardware address (MAC) from the output

### Step 2: Display the MAC address table

1. On S2's CLI:
   - Type `show mac address-table` and press Enter
   - Observe if any MAC addresses are already in the table
   - Note which ports they are associated with

### Step 3: Clear the MAC address table

1. On S2's CLI:
   - Type `clear mac address-table dynamic` and press Enter
   - Immediately type `show mac address-table` and press Enter
   - Note which MAC addresses remain (if any)
   - Wait 10 seconds, then type `show mac address-table` again
   - Note if any new MAC addresses have appeared

### Step 4: Generate traffic and observe MAC learning

1. Check PC-B's ARP cache:
   - On PC-B's Command Prompt
   - Type `arp -a` and press Enter
   - Note how many IP-to-MAC address pairs are listed

2. Ping from PC-B to other devices:
   - On PC-B's Command Prompt
   - Type `ping 192.168.1.1` and press Enter (to ping PC-A)
   - Type `ping 192.168.1.11` and press Enter (to ping S1)
   - Type `ping 192.168.1.12` and press Enter (to ping S2)
   - Verify all pings are successful

3. Check S2's MAC address table after pinging:
   - On S2's CLI
   - Type `show mac address-table` and press Enter
   - Note which new MAC addresses have been learned
   - Compare with the MAC addresses you recorded earlier to identify which device each belongs to

4. Check PC-B's updated ARP cache:
   - On PC-B's Command Prompt
   - Type `arp -a` and press Enter again
   - Note if there are new entries for the devices you pinged

## Tips for Successful Completion

1. **Timing is important**: MAC address tables update dynamically, so perform the commands quickly after clearing the table.

2. **MAC address format**: In Packet Tracer, MAC addresses may be displayed in different formats (with dashes, colons, or periods). Focus on the actual hex values.

3. **Simulation mode**: You can use Packet Tracer's Simulation mode (click the stopwatch icon) to observe frame movement and MAC learning in slow motion.

4. **Screenshots**: Take screenshots of important command outputs to help answer the lab questions.

5. **Troubleshooting**: If pings fail, verify your IP configurations and connections.

This step-by-step guide should allow you to complete the entire lab in Packet Tracer and observe how switches build and maintain their MAC address tables.
