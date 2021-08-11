# Traffic Generator Chassis Shell Standard

#### Version 1.0.5


## Introduction
The Traffic Generator Chassis shell Standard defines the standard for all Traffic Generator Chassis shells that are integrated with CloudShell. CloudShell's traffic generator shells enable you to run traffic tests on Devices Under Test (DUT) or Systems Under Test (SUT) inside a sandbox.

In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator chassis and ports, and a traffic controller service that runs the commands, such as Load Configuration, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells corresponding to different standards, allowing you to accurately model your real-life architecture.

The standard defines the shell’s data model, commands, and a set of guidelines that you should follow when developing and customizing Traffic Generator Chassis shells.


## Revision History

Version | Date | Notes
--- | --- | ---
1.0.5 | 2021-08-09 | Added Generic Traffic Generator EndPoint Entity.
1.0.3 | 2018-07-24 | 1) Separated the controller and chassis standards into two separate standards. 2) Revised the chassis stanadrd.
1.0.2 | 2018-03-19 | Added port level directly under the chassis level.
1.0.1 | 2017-01-03 | 1) The controller shell is now a service. 2) Added load configuration command to the controller. 3) Added ARP command to the controller (when applicable, for up to layer 3). 4) Added start emulation command to the controller. 5) added start/stop traffic commands to the controller. 6) added get stats command to the controller. 7) The family name  of the chassis shell is changed to "Traffic Generator Chassis" and the model changed to "<Vendor> Chassis" like "Ixia Chassis". 8) The model name for virtual chassis is changed to "Virtual Ixia". 9) The model of the port was changed to "Generic Traffic Generator Port". 10) Added "Client Install Path" attribute also to the chassis. 11) The driver name changed to "<vendor> Chassis Driver". 12) Model attribute was removed from the port. 13) Removed the "Controller Group" attribute from both the chassis and controller.
1.0.0 | 2016-09-01 | First release of the Traffic Shell Standard


## Definitions
### Granularity
The Traffic Generator Chassis shell supports all traffic generator devices of the same Vendor. For example "Ixia Traffic Generator Chassis Shell" supports all Ixia Traffic Generator chassis devices.

### Specific Version Certification
Each released shell includes a list of versions certified by Quali. This process validates that the shell's capabilities are working as designed for that particular version.
Quali releases a new shell version from time to time to resolve gaps and/or fix issues.
Note: The shell is designed to work for non-certified versions as well, unless noted in the shell's release notes.

### Generic Data Model
All Traffic Generator Chassis shells share the same generic data model, except the root level model which differs from shell to shell. Do not modify the data model. The attributes associated with the generic models are also shared by all Traffic Generator Chassis shells, and their values are populated by the driver.
Important: You cannot remove attributes from any level, but you can add custom attribute to any model level.

### Versioning
The Traffic Generator Chassis דhell version follows Semantic Versioning Guidelines (see http://semver.org). In other words, the version numbering scheme is defined as Major.Minor.Patch. For example “1.0.2”.
- A Major version is released when implementing backwards-incompatible changes. 
- A Minor version is released when adding functionality in a backwards-compatible manner.
- A Patch version is released when implementing backward-compatibile bug fixes.
The standard itself follows the same guidelines.

### Dependencies
If the Traffic Generator Chassis shell is written in Python and has Python package dependencies (that follow Semantic Versioning guidelines), we recommend setting the dependency to a range of patch versions. For example, "cloudshell-traffic-ixia 2.1.X”.
Make sure to set the cloudshell-automation-api dependency to the latest patch version. cloudshell-automation-api package version follows the format "CloudShell_Version.X". For example 7.0.X".


## Data Model
### Families & Models
The Traffic Generator Chassis דhell standard supports physical traffic generator chassis only. There are separate standards which support traffic generator controllers and virtual traffic generator chassis.

Traffic generator chassis and controllers shells are modeled per vendor. For example, a traffic generator chassis will be modeled as "Ixia Traffic Generator" or "Spirent Traffic Generator". A specific traffic generator chassis is associated with a traffic generator controller. For example, an "Ixia Traffic Generator" can be associated with an "IxNetwork" traffic generator controller. The association between traffic generators chassis and traffic generator controllers is per sandbox.

### Workflows and Shell Configuration

The expected user workflow is as follows:
1. Create a blueprint.
2. Add traffic port resources. You can add them directly from the Add Resource catalog or via an Abstract Resource Template.
3. Add the controller service of the application to be used.
4. Reserve the blueprint
5. Launch commands such as Load Configuration, Run/Stop Test etc. using the Traffic Controller Shell. For details, see the Traffic Generators Overview article in the online help (help.quali.com).

The expected administrator workflow is as follows:
1. Load both the traffic generator chassis and controller shells into CloudShell.
2. Create resources for your traffic generator chassis devices.
Notes:
- Make sure that the traffic client used by the controller is installed on the Execution Server(s) as a pre-requisited for the controller shell. In addition, define its installation path in the "Client Install Path" attribute on the Traffic Generator Controller and the Traffic Generator Chassis resource.
- If there is an external server (such as Spirent Test Center Lab Server or IxNetwork API Server), the Traffic Generator Controller address must point to this server. Define the server's TCP Port (if not default) in the "Controller TCP Port" attribute of the Traffic Generator Controller. Otherwise, define the Traffic Generator Controller address as "NA".
- Make sure to define only one controller service per application per server. For example, if for STC there is no Lab Server in use, define only one controller service. If there is a Lab Server, define two controllers: one with the server and one without.

#### Traffic Generator Chassis Data Model
- Traffic Generator Chassis
  - Generic Traffic Generator Module
     - Generic Traffic Generator EndPoint
     - Generic Traffic Generator Port
     - Generic Traffic Generator Port Group
       - Generic Traffic Generator Port
  - Generic Power Port
   

##### Example:
- Family: CS_TrafficGeneratorChassis, Model: Ixia Traffic Generator Chassis
 - Family: CS_TrafficGeneratorModule, Model: Generic Traffic Generator Module
    - Family: CS_TrafficGeneratorPort, Model: Generic Traffic Generator Port
    - Family: CS_TrafficGeneratorEndPoint, Model: Generic Traffic Generator EndPoint
    - Family: CS_PortGeneratorPortGroup, Model: Generic Port Group
      - Family: CS_TrafficGeneratorPort, Model: Generic Traffic Generator Port
 - Family: CS_PowerPort, Model: Generic Power Port

#### Family Rules
Family | Rules
--- | ---
Traffic Generator Chassis | Searchable, Shared By Default, Allow Remote Connection
Traffic Generator Module | Searchable
Traffic Generator Port | Searchable, Connectable, Locked By Default
Traffic Generator EndPoint | Searchable, Connectable, Locked By Default
Power Port | Searchable, Connectable, Locked By Default
Traffic Generator Port Group | Searchable

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Traffic Generator Chassis | [Vendor/OS] Traffic Geneartor Chassis | (user defined) | (user defined - IP)
Traffic Geneartor Module | Generic Traffic Generator Module | Module[ID] | M[ID]
Traffic Generator EndPoint | Generic Traffic Generator EndPoint | The name of the port as appears in the device. Any “/” character is replaced with “-“, spaces trimmed. | E[ID]
Traffic Generator Port | Generic Traffic Generator Port | The name of the port as appears in the device. Any “/” character is replaced with “-“, spaces trimmed. | P[ID]
Power Port | Generic Power Port | PP[ContainerID][ID] | PP[ContainerID][ID]
Port Group | Generic Traffic Generator Port Group | PG[ID] | PG[ID]

Notes:
 - The [ID] for each sub-resource is taken from the device itself, and corresponds to the names defined in the device.
 - The get_inventory command, which returns the structure to CloudShell, automatically generates the Port Group [ID].
 - Grouped ports are modeled under a "Port Group".

### Attributes
#### Guidelines
- The shell's driver does not populate attributes that are not relevant to device.
- The shell's attribute rules are as follows:
    - The "Configuration" rule is enabled for all user-input attributes.
    - The "Settings" and "Available For Abstract Resoruces" rules are enabled for all non user-input attributes.
- You can change rules on attribues in the shelldefinition yaml (only on attributes that are not associated with the family). For details, see "Customizing Shells" in the Dev Guide.
- Do not remove attributes.
- You can add custom attributes in the shelldefinition yaml, both to root and sub levels.
- All shell attributes are of type String unless noted.

##### [Vendor/OS] Traffic Generator Chassis

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
User | String | Yes | User with administrative privileges
Password | Password | Yes | 
Model Name | String | No | The catalog name of the device model. This attribute will be displayed in CloudShell instead of the CloudShell model.
Controller TCP Port | String | Yes | The TCP port of the traffic server. Relevant only in case an external server is configured. Default TCP port should be used if kept empty.
Controller Address | String | Yes | The IP address of the traffic server. Relevant only in case an external server is configured.
Client Install Path | String | Yes | The path in which the traffic client is installed on the Execution Server. For example "C:/Program Files (x86)/Ixia/IxLoad/5.10-GA".
Power Management | Boolean | Yes | Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status. Enabled by default.
Serial Number | String | No | The serial number of the resource.
Server Description | String | No | The full description of the server. Usually includes the OS, exact firmware version and additional characteritics of the device.
Vendor | String | No | The name of the device manufacture.
Version | String | No | The firmware version of the resource.

#####  Generic Traffic Generator Module

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model Name | String | No | The catalog name of the device model. This attribute will be displayed in CloudShell instead of the CloudShell model.
Version | String | No | The firmware version of the resource.
Serial Number | String | No | The serial number of the resource.

##### Generic Traffic Generator Port

Attribute Name | Data Type | User input? | Description | Possible Values
--- | --- | --- | --- | ---
Max Speed | String | Yes | Max speed supported by the interface (default units - MB) | 
Media Type | String | No | Interface media type. Possible values are Fiber and/or Copper (comma-separated). | 
Logical Name | String | Yes | The port's logical name in the test configuration. If kept emtpy - allocation will applied in the blueprint. |
Configured Controllers | String | No | specifies what controller can be used with the ports (IxLoad controller, BP controller etc...) | IxLoad, BreakingPoint, Ixload and IxNetwork, STC, TRex, TeraVM, Avalanche, Xena

##### Generic Traffic Generator EndPoint

Attribute Name | Data Type | User input? | Description | Possible Values
--- | --- | --- | --- | ---
Max Speed | String | Yes | Max speed supported by the interface (default units - MB) | 
Media Type | String | No | Interface media type. Possible values are Fiber and/or Copper (comma-separated). | 
Logical Name | String | Yes | The port's logical name in the test configuration. If kept emtpy - allocation will applied in the blueprint. |
Configured Controllers | String | No | specifies what controller can be used with the ports (IxLoad controller, BP controller etc...) | IxLoad, BreakingPoint, Ixload and IxNetwork, STC, TRex, TeraVM, Avalanche, Xena

#####  Generic Power Port

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Model Name | String | No | The catalog name of the device model. This attribute will be displayed in CloudShell instead of the CloudShell model.
Serial Number | String | No |
Version | String | No | The firmware version of the resource.
Port Description | String | No | The description of the port as configured in the device.

#####  Generic Traffic Generator Port Group
No attributes.

## Commands
Below is a list of commands that are included in the standard shell, their names and interfaces. Each Traffic Generator Chassis shell released by Quali  includes implementation for all those commands.

When developing a new shell according to the standard, you can choose which commands to implement and also add additional ones. However, a command whose functionality fits one of the predefined command is implemented according to the standard.

Command outputs:
- If a command fails, an exception containing the error is thorwn. A failure occurs when a command does not complete as expected, regardless of the error's source, from the command's input, device or the command infrastructure itself.
- If a command runs successfully, the command returns as passed with no output.

Note: When successful, the “Autoload” command produces a special output that CloudShell reads when building the resource hierarchy.

### Traffic Generator Chassis Commands
Below is a list of all commands associated with the Traffic Generator root resource.

#### Autoload
```python
def get_inventory (self, context)
```

###### Description
This command queries the device, discovers its specifications and structure and autoloads it into CloudShell. When a new resource is created, Cloudshell asks the user to specify some user input, i.e address and credentials if needed, and then calls the get_inventory function.

###### Display Name
This is a system comamnd, which is not exposed in CloudShell Portal (in the "Resource Commands" pane), and therefore, has no display name.

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | object | system parameter | Object of type AutoLoadCommandContext which includes API connectivity details and resource details, including attributes the user entered during the resource creation. | - | -
Output | AutoLoadDetails | - | object | Yes | Object of type AutoLoadDetails, containing the discovered resource structure and attributes. | - | -
