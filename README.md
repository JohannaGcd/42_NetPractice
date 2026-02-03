Alright — let’s turn your notes into a clean, compliant `README.md`.

Before you read it, quick self-check (Socratic style 🙂):
• Does each section clearly answer *what*, *how to run*, and *what concepts*?
• Does the Resources section explicitly mention networking concepts + AI usage?

Now here’s a complete redraft that follows the requirements.

---

# 42_NetPractice

*This project has been created as part of the 42 curriculum by jguacide.*

---

## Description

NetPractice is a networking training project focused on understanding and configuring small-scale network topologies.

Through a series of progressively complex levels, the goal is to correctly assign:

* IP addresses
* Subnet masks
* Routing tables
* Default gateways

in order to allow communication between hosts, switches, routers, and the Internet.

The project emphasizes practical comprehension of core networking concepts such as subnetting, routing, and packet forwarding by simulating real network flows and analyzing logs.

Each level introduces new constraints and configurations, requiring careful reasoning about network ranges and paths.

---

## Instructions

### Running the training interface

1. Open the NetPractice interface (usually by opening `index.html` in a browser).
2. For each level:

   * Modify the IP addresses, subnet masks, and routing fields as required.
   * Use the “Check” or validation button to test connectivity.
   * Analyze the logs to understand packet flow and errors.

### Exporting configurations

* After completing each level successfully, export the configuration file.
* Each exported file represents the solved state of one level.

### Submission requirements

➡️ You must place **10 exported configuration files (one per level)** at the **root of the repository**.

---

## Level Overview & Notes

### Level 1

* Two separate subnets:

  * Host A ↔ Host B
  * Host C ↔ Host D
* One modifiable tag per subnet.

Key idea:

* Devices in the same subnet must share compatible IP ranges based on the subnet mask.
* Network address (.0) and broadcast (.255) are reserved.

---

### Level 2

* Similar to Level 1, but:

  * Communication must be bidirectional
  * Both IPs and masks are modified

Key ideas:

* `/27` (255.255.255.224) → 30 usable IPs per subnet
* `/30` (255.255.255.252) → only 2 usable host IPs

Hosts must fall inside the same valid subnet range to communicate.

---

### Level 3

* Three hosts connected via a switch (same subnet).

Given:

* Host A IP: `104.198.77.125`
* Mask: `/25` (255.255.255.128)

Key idea:

* `/25` splits the range into blocks of 128:

  * `0–127`
  * `128–255`

All hosts were assigned IPs within the same subnet block.

---

### Level 4

* Two hosts connected to a switch, which connects to a router.

Given:

* Host A IP: `82.15.114.132`
* Router interfaces with different masks (`/25` and `/26`)

Key ideas:

* Determine which subnet Host A belongs to by checking block sizes.
* `/26` has a block size of 64 → valid ranges like `128–191`.

Host A, Host B, and the router interface were assigned IPs within the same `/26` subnet.

---

### Level 5

* Hosts communicate with a router.

Key ideas:

* Each host uses the router interface as its default gateway.
* Hosts share the same subnet mask as the router interface they connect to.
* IPs are chosen within the correct network range.

---

### Level 6

* Host A → Switch → Router → Internet.

Given:

* Host A IP: `78.109.226.227`
* R1 mask: `/25`
* R2 mask: `/28`
* R2 IP: `163.172.250.12`

Key ideas:

* `/25` subnet containing Host A is `78.109.226.128–255`
* Host A and R1 share this subnet
* Internet must have a route back to the LAN subnet via R2

A route was added on the Internet node to reach `78.109.226.128/25` through gateway `163.172.250.12`.

---

### Level 7

* Multiple routers with minimal subnet sizes.

Key ideas:

* `/30` is used for point-to-point links (2 usable hosts).
* Each router-to-router or router-to-host connection gets its own small subnet.
* Avoid overlap by assigning different subnet blocks.

---

### Level 8

Key ideas:

* `/28` (255.255.255.240) → 16 total addresses, 14 usable hosts
* Same mask used across segments
* Different subnet ranges assigned per link
* Routes indicate reachable networks via next-hop routers

---

Nice — before I rewrite, quick check: do you see that each level mainly revolves around **avoiding overlap, picking minimal masks, and fixing routing scope** rather than just filling IPs?

Keep that in mind as you read the summaries.

---

### Level 8 (advanced subnetting & routing scope)

Key ideas:

* Use very small subnets (`/30`) for router-to-router links to avoid wasting IP ranges
* Carefully choose non-overlapping IP blocks for each network segment
* Larger subnet (`/28`) used where more hosts are needed
* Internet routing must point back to a summarized network range instead of using multiple default routes

Important concept:

Instead of multiple conflicting default routes on R1, a single route was created pointing to a broader destination range (`141.195.172.0/27`) that covers all internal subnets behind R2.

---

### Level 9 (private IP limitation & reverse routing)

Key ideas:

* Small `/30` subnet used between router and host to minimize address usage
* Initially used private IP range (`10.0.0.x`) for a network that connects to the Internet
* Forward traffic reached the Internet, but reverse traffic failed

Important concept:

Since no NAT exists in NetPractice, **private IPs cannot communicate with the Internet**.

Fix:

* Replace private IPs with public IP ranges
* Update routing tables on routers and Internet accordingly

Additional goals:

* Build a public A–B–R11 network
* Add correct subnet destination in Internet routing (example: `/25`)
* Determine correct network address for D’s subnet using `/18` block calculations and add it to R1’s routing table

---

### Level 10 (complex overlap management & multi-network routing)

Key ideas:

* Hosts H1 and H2 placed in same subnet using router-defined mask
* Correct IP range chosen within allowed block

For Internet-connected network:

* Follow fixed masks and fixed router IPs along the path
* Adjust Internet routing CIDR to `/24` to reach entire host subnet

Hardest part:

* Create a new `/30` subnet for R22–H31 without overlapping any existing networks
* Analyze all previously used IP ranges
* Pick the next free block (`150.152.40.192–195` in example)

Final step:

* Add this subnet’s **network address + mask** as destination in R1’s routing table

---

## Resources

### Learning references

* [https://42-cursus.gitbook.io/guide/4-rank-04/netpractice/theory](https://42-cursus.gitbook.io/guide/4-rank-04/netpractice/theory)
* [https://github.com/caroldaniel/42sp-cursus-netpractice](https://github.com/caroldaniel/42sp-cursus-netpractice)

### Networking concepts studied

* TCP/IP addressing
* Subnet masks and CIDR notation
* Network and broadcast addresses
* Default gateways
* Routers and switches
* Routing tables and packet forwarding
* OSI model layers (especially Network and Data Link layers)

### AI usage

AI (ChatGPT) was used to:

* Clarify subnetting logic and CIDR block calculations
* Understand routing behavior and reverse path issues
* Help structure explanations and improve README documentation

