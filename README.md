# Cloushell Standards

This repository contains the official documentation for all CloudShell Shell Standards. A Shell standard defines the shell's data model, commands, and a set of guidelines that you should follow when developing and customizing shells.

The following standards are available in CloudShell:

Standard | Latest version | Details
--- | --- | ---
[Networking](Documentation/networking_standard.md) | 5.0.4 | Used for modeling Routers, Switches and Wireless Controllers. Relevant both for infrastructure devices and DUTs.
[Resource](Documentation/shell_resource_standard.md) | 2.0.3 | Generic resource standard. Includes an optional port and power port levels.
[Resource with Connected Commands](Documentation/Generic%20Resource%20with%20Connected%20Commands.md) | 1.0.0 | Similar to the generic resource standard. The root resource family supports connected commands (resources that are physically connected to this resource's ports will get commands that are tagged as remote commands).
[Connectable Resource](Documentation/Generic%20Connectable%20Resource.md) | 1.0.0 | Generic resource standard for root only connectable resources (no sub resources). Can be used to model simple devices such as mobile phones.
[Broadband Media Appliance](Documentation/Broadband%20Media%20Appliance%20Shell%20Standard.md) | 1.0.3 | 
[Firewall](Documentation/firewall_standard.md) | 3.0.2 |
[Traffic Generator Chassis](Documentation/Traffic%20Generator%20Chassis%20Standard.md) | 1.0.3 |
[Traffic Generator Controller](Documentation/Traffic%20Generator%20Controller%20Shell%20Standard.md) | 2.0.0 | 
Virtual Traffic Generator | 1.0.0 |
[Load Balancer](Documentation/Load%20Balancer%20Shell%20Standard.md) | 1.0.0 |
[PDU](Documentation/pdu_standard.md) | 2.0.1 | 
[SDN Controller](Documentation/SDN_controller_standard.md) | 1.0.1 |
[Software Asset](Documentation/Software%20Asset%20Shell%20Standard.md) | 1.0.0 | 
[Deployed App](Documentation/deployed_app_standard.md) | 1.0.3 | Generic deployed app standard. Used to model appliactions deployed by CloudShell.
[Cloud Provider](Documentation/cloud_provider_standard.md) | 1.0.0 | The standard for modeling the integration of private or public Cloud Providers with CloudShell
[Custom Service](Documentation/Custom%20Service%20Shell%20Standard.md) | 1.0.0 | Generic service standard
Admin Only Custom Service | 1.0.0 | Generic service standard for admin-only services
[Cloud Service](Cloud%20Service%20Shell%20Standard.md) | 1.0.0 |
Cisco ACI | 1.0.0 |
