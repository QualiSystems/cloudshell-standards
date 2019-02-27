# Generic Resource With Connected Commands

#### Version 1.0.0


## Introduction
This Shell Standard is a project used to define a standard for generic Shells that integrate with CloudShell, shells that don't match other CloudShell standards, and should support connected commands. The specifications of this shell include the most common elements that shells usually have such as: vendor, location, ports etc.




## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2019-2-26 | First release of the Generic Resource With Connected Commands standard


## Definitions
### Versioning
The Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.


## Data Model Structure
### Families & Models

- Generic Resource
 - Port
 - Power Port


##### Example:

- Family: CS_GenericResourceConnectedCommands, Model: DUT
  - Family: Port, Model: Resource Port
  - Family: Power Port, Model: Generic Power Port



#### Family Rules

Family | Rules
--- | ---
CS_GenericResourceConnectedCommands | Searchable, Shared By Default, Is Power Switch
CS_Port | Searchable, Connectable, Locked By Default
CS_PowerPort | Searchable, Connectable, Locked By Default


#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
CS_GenericResourceConnectedCommands | [The shell Model] | The IP address of the resource
CS_Port | Resource Port | The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed.] | [ID]
CS_PowerPort | Generic Power Port | PP[ContainerID][ID] | PP[ContainerID][ID]

Note: The [ID] for each sub-resource is taken from the device itself (corresponds to the names defined in the device).


## Attributes
#### Guidelines
- Attributes which aren’t relevant to a devices won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise
- Attributes associated with the family level can't be changed in the shelldefinition.yaml of the shell and are commonly used in abstract resources.

##### Generic Resource Connected Commands

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
User | User with administrative privileges | Yes | No
Password | Attribute of type Password | Yes | No
Enable Password | Attribute of type Password, The Enable password is required by some CLI protocols such as Telnet | Yes | No
Power Management | Attribute of type Boolean. Possible values – True, False, Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status | Yes | No
System Name | A unique identifier for the device, if exists in the device terminal/os | No | Yes
Vendor | | No | Yes
Location | The device physical location identifier. For example: Lab1/Floor2/Row5/Slot4 | No | Yes
Backup Location | Used by the save/restore orchestration to determine where backups should be saved | Yes | No
Model | The device model. This information is typically used for abstract resource filtering. | No | Yes
SNMP Read Community | | Yes | No
SNMP Write Community | | Yes | No
SNMP V3 User | | Yes | No
SNMP V3 Password | | Yes | No
SNMP V3 Private Key | | Yes | No
SNMP V3 Authentication Protocol | Relevant only in case SNMP V3 is in use. Possible values are "No Authentication Protocol" (default), "MD5", "SHA". | Yes | No
SNMP V3 Privacy Protocol | Relevant only in case SNMP V3 is in use. Possible values are "No Privacy Protocol" (default), "DES", "3DES-EDE", "AES-128", "AES-192", "AES-256" | Yes | No
SNMP Version | Possible values – v1, v2c, v3 | Yes | No
Sessions Concurrency Limit | Attributes of type Numeric. Default is 1 (no concurrency) | Yes | No
Console Server IP Address | | Yes | No
Console User | | Yes | No
Console Port | Attributes of type Numeric | Yes | No
Console Password | Attribute of type Password | Yes | No
CLI Connection Type | Attribute of type Lookup. Possible values – Auto, Console, SSH, Telnet, TCP | Yes | No
Model Name | Attribute of type String. Automatically populated model name that will be presented in the Sandbox diagram | No | Yes


##### Generic Port

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
MAC Address | | No | No
IPv4 Address | | No | No
IPv6 Address | | No | No
Port Speed | The port speed (e.g 10Gb/s, 40Gb/s, 100Mb/s) | No | No
Model Name | Attribute of type String. Automatically populated model name that will be presented in the Sandbox diagram | No | Yes


#####  Generic Power Port

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
Model | | No | No
Serial Number | | No| No | No
Version | | No | No
Port Description | | No | No
Model Name | Attribute of type String. Automatically populated model name that will be presented in the Sandbox diagram | No | Yes


## Commands
The following chapter describes the list of commands that needs to be supported by the shell. it includes command name, parameters and description of the functionality.

Note that this standard supports **connected commands**. This means that if a command in this shell's driver is tagged with Tags="remote_connectivity", it will be available for all resources that are physically connected to sub-resources of this shell. For example, if you have some controller that has multiple end-devices connected to its ports, you can tag commands that should be launched directly on the end-devices as connected commands.

**Interface Implementation** - When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

**Error Handling**: Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output.



### Get Inventory (Shell Autoload)
```python
def get_inventory(self, context)
```  
###### Description
This function queries the device, discovers it's specification and autoloads it into CloudShell. When a new resource is created, CloudShell asks the user to specify some user inputs (i.e user name & password) and then it calls the get_inventory function.

The standard recommended way of communicating and discovering the device should be via SNMP protocol.


###### Display Name
System command, it has no display name.



###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | context | object | system parameter | object of type AutoLoadCommandContext which includes API connectivity details and the details of the resource including attributes that the user entered during the resource creation.
Output | AutoLoadDetails | object | Yes | object of type AutoLoadDetails which the discovered resource structure and attributes.



### Save & Restore in sandbox orchestration  
The shell must implement the save and restore commands and is responsible on saving and restoring its own state. The standard specifies the interface and functionality that shells expose to the sandbox orchestration. These two commands are hidden from the end user, their interface uses .json protocol and they should only be used by the sandbox orchestration via API.


```python
def orchestration_save (mode="shallow", custom_params = null)
```

```python
def orchestration_restore (saved_details)
```

**For more details:** [Orchestration Standard - Save & Restore ](http://goo.gl/L8pUjP)
