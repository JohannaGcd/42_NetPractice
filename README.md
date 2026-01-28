# 42_NetPractice
NetPractice taught me how to configure small-scale networks.

Level 1:
- We have two separate subnets, 
 	host A needs to communicate with host B in the same subnet
 	And host C needs to communicate with host D
- We are given one modifiable tag for each subnet. 
	To complete the exercise, each tag should be modified to enable communication
	between the two hosts, as specified in the subject.
- To complete the exercise, the IP address should be modified such as:
	the router has the same number (first 3 digits based on the subnet mask)
	the device number is close enough to that of the receiving host (the number should be between 1 and 254 inclusive, as .0 and.255 are reserved for the network and broadcast address respectively, ie. default gateway)

Level 2:
- We have a similar configuration with Level 1, with two separate subnets, only:
	1. communication should happen back and forth
	2. 4 tags should be modified (both IP and Mask)
- To complete the exercice between Hosts A and B:
	Given are: Host B-IP (192.168.137.222) and Host A-Mask (255.255.255.224)
	Given A and B are part of the same subnet, I changed B's subnet to the same as A's.
	A subnet mask ending in .224 is equivalent to /27, meaning there are 30 total usable IPs
	So, to allow back and forth communication between Host A and B, I changed A's
	IP to 192.168.137.193 (could be any number between 193 and 221).
- Between Hosts C and D:
	Given are: Host C-Mask (255.255.255.252) and Host D-Mask (/30)
	255.255.255.252 and /30 are equivalent. Question is what is the range of potential IPs within the range allowed by this subnet mask?
	/30 allows only 2 usable Host IPs, so I can use either .1 or .2 (first .0 and last .4 being reserved, as we've seen above). From there, I could pick any IP within allowed ranges:
	[picked arbitrarily: 192.168.1, outside of the "reserved ranges"] and then for each host a different ending, within scope: .1 and .2.

Level 3:
- Configuration: 
	3 host computers, connected via a network switch, which connects devices
	within the same network. 
	Given are: Host A-IP (104.198.77.125), and Host C-Mask (255.255.255.128)
- To complete, I:
	Given that the hosts are connected via a switch, they are on the same subnet. 
	Host A's IP is 104.198.77.125. With a /25 mask (255.255.255.128), this places it in the following subnet range: 104.108.77.0->127.
	Therefore, I gave the other hosts (B and C) IPs in the same range (excluding .0 and .127, reserved for the network and default gateway respectively).
	I gave the other hosts the same /25 mask so they would compute the same network address and communicate successfully. 

Level 4:
- Configuration:
	2 hosts (A and B) are connected to a switch, which is connected to a router. 
	We are given A's IP: 82.15.114.132 and 2 out of 3 router interfaces: R2: IP - 82.15.114.1 Mask - 255.255.255.128 and R3: IP - 82.15.114.244 Mask - 255.255.255.192
- To complete:
	First, we have to figure out the range of valid IPs for A's subet. A's IP is 82.15.114.132. Looking at R2's Mask (255.255.255.128) this is a /25, so a block size of 128. A's IP (ending with 132) doesn't fit. R3's Mask (255.255.255.192) corresponds to a /26 decimal. Block size should be 64, so the range corresponding to it's IP is 192-255, which excludes A's 132. Therefore, A belongs to a /26 subnet, which must be contained in R1. 
	Since Host A is a /26 mask, the range of IPs is 128-191. So R1 should have a usable IP is that range (ex: 82.15.114.129).
	Moving on to B, since A & B are on the same switch, B must be in the same subnet as A. So mask is /26 and IP should be in the same usable range (128-191).