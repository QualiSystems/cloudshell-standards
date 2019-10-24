# Traffic Generator Controller Shell Standard

#### Version 2.0.0

## Introduction
The Traffic Generator Controller Shell Standard is a project used to define a standard for all Traffic Generator Controlleres that integrate with CloudShell. CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) inside the sandbox.

In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator chassis and ports, and a traffic controller service that runs the commands, such as Load Configuration, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells corresponding to different standards, allowing you to accurately model your real-life architecture.

The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in traffic generator controller Shells development and customization.


## Revision History

Version | Date | Notes
--- | --- | ---
2.0.0 | 2019-02-13 | Updated the attributes and commands of the standard, adding new attributes and commands and changing the interface of some of the existing commands. This standard is not backwards compatible.
1.0.0 | 2018-02-19 | First release of the Traffic Generator Controller Shell Standard

## Definitions
### Granularity
 The Traffic Generator Controller Shell supports traffic controller of a specific vendor and application, for example "Ixia BreakingPoint Traffic Controller Shell" or "Spirent Test Center Controller Shell".

### Specific Versions Certification
Each released Shell should have a list of certified versions. Version certification can be done only by Quali’s engineering, and it includes validatation that all the Shell’s capabilities are working for a specific version.
The Shell should also work for non-certified versions unless specified differently in the Shell's release notes, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the version certified.

### Generic Data Model
All traffic generator controller shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all traffic generator controller shells and their values are populated by the driver. It is allowed to add custom attributes to any resource level, and it isn’t allowed to remove attributes from any level.

### Versioning
The traffic generator controller shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Patch version is promoted when making backward-compatibile bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making any backwards incompatible change. The standard itself follows the same guidelines.

### Dependencies
In case the traffic generator controller shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-traffic-ixia 2.1.X”.
The dependency to cloudshell-automation-api should be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).


## Data Model
### Families & Models
The traffic generator controller shell standard supports traffic generator controllers, working with either physical or virtual traffic chassis.

The traffic generator chassis and controllers shells are modeled per vendor; for example a traffic generator chassis will be modeled as "Ixia Traffic Generator" or "Spirent Traffic Generator". A specific traffic generator chassis is associated with a traffic controller; for example an "Ixia Traffic Generator" can be associated with an "IxNetwork" traffic generator controller. The association between traffic generators and traffic controllers is per sandbox.

### User flows and Shell configuration
The expected user flow is adding traffic ports to a blueprint (via the inventory or abstract template), adding the relevant controller service, and reserving. Launch commands such as load configuration, run/stop traffic etc. using the Traffic Controller shell.

The expected administrator flow is to load both the traffic generators and controllers into CloudShell inventory. The traffic client used by the Controller is expected to be installed on the Execution Server(s) as a pre-requisite for the controller shell and the path to its installation should be defined in the attribute "Client Install Path" on the Traffic Generator Controller and Traffic Generator Chassis resource. In case there is an external server (such as Spirent Test Center Lab Server or IxNetwork API Server) the address of the Traffic Generator Controller should point to this server and the server's TCP Port (if not default) should be defined in the "Server TCP Port" attribute of the Traffic Controller. Else the address of the Traffic Controller should be defined as "NA".
Only one controller service should be defined per application per server. For example, if for STC there is no lab server in use, only one controller service should be defined. If there is a lab server, 2 controllers should be defined: one with the server and the other without.

#### Traffic Generator Controller Data Model
- Traffic Generator Controller
 - (no sub resources)


##### Example:

- Family: Traffic Generator Controller, Model: Ixia IxNetwork Traffic Generator Controller

#### Family Rules

Family | Rules | Default Category
--- | --- | ---
Traffic Generator Controller | Regular Service | Traffic Generator Controllers

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Traffic Generator Controller | [Vendor/Application] Traffic Generator Controller | (not relevant) | (user defined - IP or "NA")

Note:
The address of a physical Traffic Generator Controller should be the IP of the server in case an external server is configured (can be relevant for Ixia IxNetwork, Spirent Test Center Lab Server and Ixia IxN2X). In case there is no external server the address should be "NA" which means there is no external server but only a client application installed on the Execution Servers.

### Attributes
#### Guidelines
- Attributes which aren’t relevant to a device/application won’t be populated by the driver.
- All attributes which aren't user-input should have the rule "Admin only" enabled.
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.
- Attributes shouldn’t be removed.
- Custom attributes can be added to any resource level.
- All attributes are of type String unless mentioned otherwise
- Some traffic controller shells will be released with additional attributes which are specific to them, for more information see the shell's documentation.

##### [Vendor/Application] Traffic Generator Controller

Attribute Name | Data Type | User input? | Description | Family Attribute?
--- | --- | --- | --- | ---
Client Install Path | String | Yes | The path in which the traffic client is installed on the Execution Server. For example "C:\Program Files (x86)\Ixia\IxLoad\5.10-GA". | No
Address | String | Yes | | No
Controller TCP Port | String | Yes | The TCP port of the traffic server. Relevant only in case an external server is configured. Default TCP port should be used if kept empty. | No
User | String | Yes | | No
Password | Password | Yes | | No
Test Files Location | String | Yes | Location for test related files | No

## Commands
Below is a list of all the commands that are part of a standard traffic generator controller Shell, their names and interfaces. Each traffic generator controller Shell that will be released by Quali’s engineering will include implementation for all those commands as long they are relevant to the specific vendor or application.

Some traffic controller shells will be released with additional commands which are specific to them, for more information see the shell's documentation.

When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output. The “Autoload” command has a special output on success that CloudShell reads when building the resource hierarchy.

### Traffic Generator Controller Commands
Below is a list of all the commands associated with the Traffic Generator Controller service (Family = Traffic Generator Controller).

#### Load Configuration
```python
def load_config(self, context, config_file_location)
```

###### Description
Reserve ports and load configuration

###### Display Name
Load Configuration

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | config_file_location | Configuration File Location | String | yes | Full path to the configuration file

#### Start Traffic
```python
def start_traffic(self, context, blocking)
```

###### Description
Start traffic on all ports

###### Display Name
Start Traffic

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description | Allowed Values | Default Value
--- | --- | --- | --- | --- | --- | --- | ---
Input | blocking | Block | Lookup | no | True - return after traffic finish to run, False - return immediately | True, False | False

#### Stop Traffic
```python
def stop_traffic(self, context)
```

###### Description
Stop traffic on all ports

###### Display Name
Stop Traffic

###### Parameters
No parameters.

#### Get Statistics
```python
def get_statistics(self, context, view_name, output_type)
```
###### Description
Get real time statistics as sandbox attachment

###### Display Name
Get Statistics

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | view_name | View Name | String | yes | The requested view name, see shell's documentation for details
Input | output_type | Output Type | String | yes | CSV or JSON

#### Send ARP
```python
def send_arp(self, context)
```
###### Description
Send ARP/ND for all protocols

###### Display Name
Start ARP/ND

###### Parameters
No parameters.

#### Start Protocols
```python
def start_protocols(self, context)
```
###### Description
Start all protocols

###### Display Name
Start Protocols

###### Parameters
No parameters.

#### Stop Protocols
```python
def stop_protocols(self, context)
```
###### Description
Stop all protocols

###### Display Name
Stop Protocols

###### Parameters
No parameters.

#### Run Quick Test
```python
def run_quick_test(self, context)
```
###### Description
Run quick test

###### Display Name
Run Quick Test

###### Parameters
No parameters. For parameters in specific shells see the shell's documentation.

#### Get Session Id
```python
def get_session_id(self, context)
```
###### Description
API only command to get REST session ID.

###### Display Name
get_session_id

###### Parameters
No parameters.

#### Get Children
```python
def get_children(self, context, obj_ref, child_type)
```
###### Description
API only command to get list of children

###### Display Name
get_children

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | obj_ref | obj_ref | String | Yes | Valid object reference
Input | child_type | obj_ref | String | Yes | Requested children type. If None returns all children.

#### Get Attributes
```python
def get_attributes(self, context, obj_ref)
```
###### Description
API only command to get object attributes

###### Display Name
get_attributes

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | obj_ref | obj_ref | String | Yes | Valid object reference

#### Set Attribute
```python
def set_attribute(self, context, obj_ref, attr_name, attr_value)
```
###### Description
API only command to set traffic generator object attribute

###### Display Name
set_attribute

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | obj_ref | obj_ref | String | Yes | Valid object reference
Input | attr_name | attr_name | String | Yes | Attribute name
Input | attr_value | attr_value | String | Yes | Attribute value

#### Cleanup Reservation
```python
def cleanup_reservation(self, context)
```
###### Description
No description.
This is a hidden command to release the traffic ports, should be called by the sandbox teardown script. Implemented only in traffic controllers that don't release the port automatically when the session ends.

###### Display Name
Cleanup Reservation

###### Parameters
No parameters.

#### Cleanup
```python
def cleanup(self)
```
###### Description
No description.
This is a hidden command.

###### Display Name
No display name.

###### Parameters
No parameters.

#### Keep Alive
```python
def keep_alive(self, context, cancellation_context)
```
###### Description
No description.
This is a hidden command.

###### Display Name
Keep Alive

###### Parameters
No parameters.
