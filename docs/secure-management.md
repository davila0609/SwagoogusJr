\# Secure Router and Switch Management



\## Issue

Issue #3 — Secure Router and Switch Management



\## Objective

Improve administrative access to the PC Café network devices by using secure local administrator accounts and SSH instead of insecure remote management methods.



\## Devices Secured

\- PC\_Cafe router

\- Ops\_Switch

\- Guest\_Switch

\- BackOffice\_Switch



\## Router Configuration

The PC\_Cafe router was configured with:

\- Local administrator accounts

\- Enable secret

\- Domain name `pc-cafe.local`

\- 1024-bit RSA keys

\- SSH version 2

\- Local authentication on VTY lines

\- SSH-only remote access



VTY configuration:



```text

line vty 0 4

&#x20;login local

&#x20;transport input ssh

```



SSH was successfully verified from a client PC.



\## Operations Switch

The Operations switch was configured for secure management.



Management settings:

\- Hostname: `Ops\_Switch`

\- Management VLAN: VLAN 10

\- Management IP: `192.168.0.36/27`

\- Default gateway: `192.168.0.33`

\- SSH version 2

\- Local administrator authentication

\- SSH-only VTY access



Remote SSH login from the Reception PC was successfully tested.



\## Guest Switch

The Guest switch was configured with:

\- Hostname: `Guest\_Switch`

\- Management interface: VLAN 1

\- Management IP: `192.168.0.30/27`

\- Default gateway: `192.168.0.1`

\- SSH version 2

\- Local administrator authentication

\- SSH-only VTY access



The management interface was verified as `up/up`.



\## Back Office Switch

The Back Office switch was configured with:

\- Hostname: `BackOffice\_Switch`

\- Management interface: VLAN 1

\- Management IP: `192.168.0.125/27`

\- Default gateway: `192.168.0.126`

\- SSH version 2

\- Local administrator authentication

\- SSH-only VTY access



Remote SSH access was successfully tested from the Back Office network.



\## Security Improvement

Before this change, the switches did not have secure remote management configured. Their VTY lines used basic login settings and did not require SSH.



After the change:

\- SSH version 2 is enabled.

\- RSA encryption keys are installed.

\- Local administrator authentication is required.

\- Telnet is disabled by allowing only SSH on VTY lines.

\- Management interfaces were configured where required.

\- Secure remote login was successfully tested.



\## Verification

The following commands were used to verify the implementation:



```text

show ip ssh

show ip interface brief

show running-config | section line vty

show running-config | include username

```



SSH login tests successfully reached the network devices and provided privileged access using the configured enable secret.



\## Result

Secure administrative management was successfully implemented across the PC Café router and switches.

