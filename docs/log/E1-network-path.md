# E1: Can the internet reach the host?

**Goal:** confirm an inbound UDP port reaches the host before building
WireGuard on it. This is the riskiest unknown, since an ISP router might
block or fail to forward inbound UDP.

## What I did
1. Collected the host's LAN address and gateway, and my public IP.
2. Checked the public IP matched the router's WAN IP, which rules out CGNAT.
3. Created a UDP port forward (51820) on the ISP router to the host's static address.
4. Ran `tcpdump -ni any udp port 51820` on the host.
5. From a PC on a phone hotspot (a genuinely outside network), sent one UDP packet to my public IP.

## Result
Packet arrived at the host; the source address was a public carrier address,
not a LAN one. **Passed.**

## Notes
- The public IP is dynamic, so dynamic DNS is needed later (E5).
- A website port checker would not have proven this; seeing the packet arrive
  at the host did.
