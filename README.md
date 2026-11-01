# Two-office standard ACL | Project 8
This Cisco Packet Tracer lab uses a standard IPv4 access control list (ACL) on the Dublin router to filter traffic from the Cork LAN. OSPF continues to connect the two routers.

![Dublin and Cork topology](images/topology.png)

| Network | Addresses |
|---|---|
| Dublin LAN | PC 192.168.10.11/24; gateway 192.168.10.1 |
| Router link | Dublin 10.0.0.1/30; Cork 10.0.0.2/30 |
| Cork LAN | PC 192.168.20.11/24; gateway 192.168.20.1 |

## What the ACL does
R1-dublin checks ACL 10 on packets leaving G0/0 towards the Dublin LAN. The first rule denies sources in 192.168.20.0/24. The second permits other sources. Rules are checked in order; without an explicit permit, unmatched packets are dropped.

This is a source-based filter. A ping started in Dublin also fails because the reply from Cork is blocked. OSPF stays FULL on G0/1, the link between the routers.

## Results
| Test from Cork to Dublin | Result |
|---|---|
| ACL applied | 0/4 replies; deny counter showed 4 matches |
| ACL detached from G0/0 | 4/4 replies |
| ACL reapplied | 0/4 replies |

## Reproduce
1. Open [the project](lab/Project-8-Office-ACL.pkt) in Packet Tracer.
2. From CORK-PC, ping 192.168.10.11. On R1-dublin, run `show access-lists` and `show ip ospf neighbor`.
3. Use the [ACL commands](configs/ACL-commands.txt) to detach the filter, repeat the ping, then reapply the filter and test again.

[Router configurations](configs/) · [Test results](tests/verification.txt) · [Combined evidence image](images/Project-8-Network-Evidence.jpg)

The results above come from the recorded lab session. The uploaded Packet Tracer file is included unchanged under its Project 8 filename.
