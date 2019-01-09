# Deployed App Shell Standard

#### Version 1.0.3


## Introduction
The deployed App Shell Standard defines a standard for all deployed App shells that integrate with CloudShell. The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in compute server shell development and customization.


## Revision History

Version | Date | Notes
--- | --- | ---
1.0.3 | 2018-05-08 | Added the attribute Bandwidth to the vPort level sub-level
1.0.2 | 2018-02-20 | Added a vPort optional sub-level
1.0.0 | 2016-07-14 | First release of the Compute server Shell Standard


## Definitions

### Versioning
The compute Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.

## Data Model
### Families & Models

** Deployed App Data Model **

- Family: CS_GenericAppFamily, Model: Generic Deployed App
   - Family: CS_Port, Model: Generic vPort

#### Family Rules

Family | Rules
--- | ---
Generic App Family | Searchable, Locked By Default
CS_Port | Searchable, Locked By Default, Connectable

### Attributes
#### Guidelines
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings", "Read only" and "Available For Abstract Resources" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.
- All attributes are of type String unless mentioned otherwise
- Attributes associated with the family level can't be changed in the shelldefinition.yaml of the shell and are commonly used in abstract resources.

#### Generic App

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
User | | Yes | No
Password | | Yes | No
Public IP | | No | No

####  Generic VPort
Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
Bandwidth | The current interface bandwidth, in MB. Integer. | No | No
Request vNIC Name | VNic to be associated with the vPort. | Yes | No
Model Name | | Yes | Yes
IP Address | | Yes | No
MAC Address | | Yes | No
