\# PC Café Network Access Control Implementation



\## Purpose



The purpose of this change is to restrict the Guest network from accessing internal PC Café networks while allowing required internal business communication.



\## Network Segments



\- Guest: `192.168.0.0/27`

\- Reception: `192.168.0.32/27`

\- Sales: `192.168.0.64/27`

\- Back Office: `192.168.0.96/27`



The Back Office router interface was corrected to:



`192.168.0.126 /27`



PC6 uses:



\- IP: `192.168.0.97`

\- Gateway: `192.168.0.126`



The Back Office printer uses:



\- IP: `192.168.0.98`

\- Gateway: `192.168.0.126`



\## ACL Configuration



An extended ACL named `GUEST\_RESTRICT` was created.



```text

10 deny ip 192.168.0.0 0.0.0.31 192.168.0.32 0.0.0.31

20 deny ip 192.168.0.0 0.0.0.31 192.168.0.64 0.0.0.31

30 deny ip 192.168.0.0 0.0.0.31 192.168.0.96 0.0.0.31

40 permit ip any any

```



The ACL was applied inbound on `GigabitEthernet0/0`, the Guest network interface.



\## Before ACL



Before the ACL was applied, Guest PC1 successfully reached Back Office PC6 at `192.168.0.97`.



Result: 4 replies, 0% packet loss.



This demonstrated that Guest devices could communicate with protected internal systems.



\## After ACL



After applying `GUEST\_RESTRICT`:



| Test | Result |

|---|---|

| Guest → Reception `192.168.0.34` | Blocked |

| Guest → Sales `192.168.0.66` | Blocked |

| Guest → Back Office `192.168.0.97` | Blocked |

| Guest → Guest Gateway `192.168.0.1` | Allowed |

| Reception → Sales `192.168.0.66` | Allowed |

| Reception → Back Office `192.168.0.97` | Allowed |

| Sales → Back Office `192.168.0.97` | Allowed |



\## ACL Verification



The router displayed these match counters:



```text

10 deny ip 192.168.0.0 0.0.0.31 192.168.0.32 0.0.0.31 (4 matches)

20 deny ip 192.168.0.0 0.0.0.31 192.168.0.64 0.0.0.31 (4 matches)

30 deny ip 192.168.0.0 0.0.0.31 192.168.0.96 0.0.0.31 (4 matches)

40 permit ip any any (4 matches)

```



These counters confirm that the router actively blocked Guest traffic to the three protected internal networks while still permitting other traffic.



\## Conclusion



The ACL successfully isolates the Guest network from Reception, Sales, and Back Office resources without disrupting required communication between the internal business networks.



The configuration was saved using:



```text

copy running-config startup-config

```

