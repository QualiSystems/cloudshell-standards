# SDN Contorller Shell Standard

#### Version 1.0.0


## Introduction
The SDN Controller Shell Standard is a project used to define a standard for all SDN Controller Shells that integrate with CloudShell.
The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in SDN Controller Shells development and customization.


## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2017-11-01 | First release of the Traffic Shell Standard


## Definitions
### Granularity
The SDN Controller Shelll will be implemented for each type of controller. example "SDN ODL Shell". 

### Specific Versions Certification
Each released Shell should have a list of certified versions. Version certification can be done only by Quali’s engineering, and it includes validatation that all the Shell’s capabilities are working for a specific version.
The Shell should also work for non-certified versions unless specified differently in the Shell's release notes, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the version certified.

### Generic Data Model
All SDN Controller Shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all SDN Controller Shells and their values are populated by the driver. It is allowed to add custom attributes only to the root level model, and it isn’t allowed to remove attributes from any level.

### Versioning
The SDN Controller Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Patch version is promoted when making backward-compatibile bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making any backwards incompatible change. The standard itself follows the same guidelines.

### Dependencies
In case the SDN Controller Shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-traffic-ixia 2.1.X”.
The dependency to cloudshell-automation-api should be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).



## Data Model
### Families & Models

The SDN Controller is modeled per type; for example a open daylight server will be modeled as "SDN ODL Controller".

### User flows and Shell configuration

The SDN controller will act as a "Giant" switch providing l2 connectivity.
The main use case is to have the SDN act as the infra structure (not as DUT).
Once autuoload is done, the admin will add the relevenat physical connections and thus have capabilities to do logical connections.

#### SDN Controller Data Model
- SDN Controller
 - Switch
    - Port
   
##### Example:
- Family: SDN Controller, Model: SDN ODL controller
- Family: SDN Switch, Model: Generic SDN switch
- Family: Port, Model: Generic SDN Port

#### Family Rules

Family | Rules
--- | ---
SDN Controller | Searchable
Switch | Searchable
Port | Searchable, Connectable, Locked By Default

##### Controller Rules
Rule | Value
--- | ---
SupportsConcurrentCommands | True
isPowerSwitch | False

##### Swicth Rules
Rule | Value
--- | ---
SupportsConcurrentCommands | True
isPowerSwitch | False

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Controller | SDN [Vendor] Controller | (user defined) | (user defined - IP)
Switch | Generic SDN Switch | openflow:[ID] | [ID]
Port | Generic SDN Port | The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed.] | [ID]

Note: The [ID] for each sub-resource is taken from the controller itself.


### Attributes
#### Guidelines
- Attributes which aren’t relevant to a device won’t be populated by the driver.
- All attributes which aren't user-input should have the rule "Admin only" enabled.
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

#### SDN [Vendor] Controller
Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
User | String | Yes |
Password | Password | Yes |
Model Name | String | No | The Controller model/vendor in a readable format (used by the GUI for display). This information is typically used for abstract resource filtering.
Controller TCP Port | Integer | Yes |  default is 8181.
Scheme | String | Yes | two options: HTTP, HTTPS
Enable Full Trunk Ports | String | Yes | Optional. in case need to configure a full trunk port to be accessible for all flows (example: ports that private cloud provider are connected to), the ports should be listed in format: openflow:1::eth1;openflow:1:eth2
Disable Full Trunk Ports | String | Yes | Optional. in case need to remove a full trunk port , the ports should be listed in format: openflow:1::eth1;openflow:1:eth2

##### Generic SDN Switch
Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model Name | String | No | The switch model/Vendor. This information is typically used for abstract resource filtering.

##### Generic SDN Port
Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
MAC Address | String | No |
IPv4 Address | String | No |
IPv6 Address | String | No |
Port Description | String | No | The description of the port as configured in the device.
Adjacent | String | No | The adjacent device (system name) and port, based on LLDP or CDP protocol.


## Commands
Below is a list of all the commands that will be part of the standard Shell, their names and interfaces. Each SDN Controller Shell that will be released by Quali’s engineering will include implementation for all those commands.

When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output. The “Autoload” command has a special output on success that CloudShell reads when building the resource hierarchy.

### SDN Controller Commands
Below is a list of all the commands associated with the Traffic Generator root resource (Family = Server).

#### Autoload
```python
def get_inventory (self, context)
```

###### Description
This function queries the controller, discovers it's specification and structure and autoload it into CloudShell. When new resource is created Cloudshell asks the user to specify some user input (i.e address and credentials if needed) and then it calls the get_inventory function.
The autoload should retrive only the leaf ports, and not ports that are part of the spine or facing it (core).
During autoload, if there is an input in the Enable Full Trunk Ports or Disable Full Trunk Ports attribute, the autload command will also configure those ports accordingly.

###### Display Name
System command, it has no display name

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | object | system parameter | object of type AutoLoadCommandContext which includes API connectivity details and the details of the resource including attributes that the user entered during the resource creation. | - | -
Output | AutoLoadDetails | - | object | Yes | object of type AutoLoadDetails with the discovered resource structure and attributes. | - | -

#### ### ApplyConnectivityChanges
```python
def ApplyConnectivityChanges(self, context, request)
```

###### Description
Configures flows with VLANs as match cretiria.

###### Notes
The standard doesn’t support different VLAN request to the same Switch/Router/Wireless-Controller port at the same time. For example, connecting the same port to multiple VLAN services each with a different VLAN ID/range. When configuring VLAN ID/range on a port the assumption is that there is no other VLAN configured on it. 
This command should be hidden from the UI.
The controller will get 2 requests. each request will contain a port and a vlan id. a flow will be created between those 2 ports with the vlan ID as match criteria
If valn service will be used in order to connect more port - those ports will be added to the flow with the same vlan ID as match criteria.
The controller will be able to handle getting only one request. This port will be added to a flow with the same vlan ID (if exist) and/or to trunk port pre configured (see vcenter section below). In case none of them exist it will get configured with out any dest flow until a new request will arrive with the same vlan id or a trunk port.
In case of QinQ connectivity, those flows will not include the fully trunked port as we need a matching configuration in all ends of the flow.

  
Private cloudsa:
The Admin should specifying the port/ports that the private cloud is connect to in the "Enable Full Trunk Ports" before the autload. Those ports will be configured as fully trunked port during autoload (same as required regardless of SDN).
Any flow that will be defined by cloud shell will automatically include those trunk port thus getting the same behavior as we have in a regular l2 fabric.
In case of app to app connectivity nothing will be executed on the controller.

###### Display Name
ApplyConnectivityChanges

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | request | request | string | Yes | a JSON with bulk “add_vlan” or “remove_vlan” request. The request includes the list of ports and VLANs that should be configured or cleared on those ports. See separate article with the JSON schema and an example.
Output | | | string | Yes | a JSON with the command’s response, should include success/fail per each connection request.
