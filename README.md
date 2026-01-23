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
	Modified all the masks to match the given one (Host C - 255.255.255.128)
	With this mask, there are exactly 126 usable host IPs.
	Host A's IP is given: 104.198.77.125.
	
