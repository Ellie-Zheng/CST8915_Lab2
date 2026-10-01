# CST8915 Lab 2: Refactor the Algonquin Pet Store - Part 1

- **Student Name**: Ellie Zheng
- **Student ID**: 041078727
- **Course**: CST8915 Full-stack Cloud-native Development
- **Semester**: Fall 2026

---

## Notes About Setup Challenges and Lessons Learned

To save Azure credits, I initially chose the cheapest available VM size (2vCPU with 1GB RAM) for the Order Service. It felt slow when I started running it, so I deleted that VM and created a larger one later. I also ran into a three-public-IP quota on my Azure for Students subscription. Deleting the old VM did not immediately remove its public IP resource, and I spent extra time finding and removing that leftover resource before I could continue. During the rebuild, I then overlooked the inbound rule for port 3000. As a result, while the Store Front loaded and displayed products, order placement consistently failed. I checked the services and request path step by step before discovering that the new VM was blocking the browser’s request. This taught me that a running service also needs the correct network rule to be reachable from outside its VM.

Later, I moved from school to home, and my laptop’s public IP changed. My SSH connections to all four VMs timed out because their access rules still allowed my school IP. Updating the inbound rules with my new IP restored access. This highlighted the importance of verifying both source IP authorization and destination port configuration whenever a previously stable connection fails.
