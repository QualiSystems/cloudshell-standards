# Compute Server Shell Standard

#### Version 2.0.1


## Introduction
The Compute Server Shell Standard defines a standard for all compute server shells that integrate with CloudShell. The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in compute server shell development and customization.




## Revision History

Version | Date | Notes
--- | --- | ---
2.0.1 | 2017-07-03 | Added a "Model Name" attribute on the root resource
2.0.0 | 2017-01-31 | Changed the type of the following attributes to "Password": "SNMP Read Community", "SNMP Write Community" and "SNMP V3 Password". Those changes are NOT backwards compatible
1.0.0 | 2016-07-14 | First release of the Compute server Shell Standard


## Definitions

### Versioning
The compute Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.


## Data Model Structure
### Families & Models

**Compute Server Data Model**
- Compute Server
 - Port
 - Power Port


**Example**
- Family: Compute Server, Model: Dell Power-Edge Server
- Family: Port, Model: Resource Port
- Family: Power Port, Model: Generic Power Port


#### Family Rules

Family | Rules
--- | ---
Compute Server | Searchable
Port | Searchable, Connectable, Locked By Default
Power Port | Searchable, Connectable, Locked By Default



#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Compute | [Vendor] [Series] Server | (user defined) | (user defined - IP)
Power Port | Generic Power Port | PP[ContainerID][ID] | PP[ContainerID][ID]

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

##### [Vendor] [Series] Server

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
User | User with administrative privileges | Yes | No
Password | Attribute of type Password | Yes | No
Enable Password | Attribute of type Password, The Enable password is required by some CLI protocols such as Telnet | Yes | No
Power Management | Attribute of type Boolean. Possible values – True, False, Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status | Yes | No
System Name | A unique identifier for the device, if exists in the device terminal/os | No | No
Vendor | | No | Yes
Location | The device physical location identifier. For example: Lab1/Floor2/Row5/Slot4 | No | Yes
Backup Location | Used by the save/restore orchestration to determine where backups should be saved | Yes | No
Model | The device model. This information is typically used for abstract resource filtering. | No | Yes
SNMP Read Community | | Yes | No
SNMP Write Community | | Yes | No
SNMP V3 User | | Yes | No
SNMP V3 Password | | Yes | No
SNMP V3 Private Key | | Yes | No
SNMP Version | Possible values – v1, v2c, v3 | Yes | No
Sessions Concurrency Limit | Attributes of type Numeric. Default is 1 (no concurrency) | Yes | No
Console Server IP Address | | Yes | No
Console User | | Yes | No
Console Port | Attributes of type Numeric | Yes | No
Console Password | Attribute of type Password | Yes | No
CLI Connection Type | Attribute of type Lookup. Possible values – Auto, Console, SSH, Telnet, TCP | Yes | No
OS Architecture | The Operating System (OS) architecture - i.e: x86_32, x86_64, etc. | No | No
OS Type | The Operating System (OS) type - i.e: linux, aix, mac, windows, etc.  | No | No
OS Distribution | The Operating System (OS) distribution. i.e: linux distributions: debian, fedora, rhel and ubuntu | No | No
OS Version | The Operating System version | No | No
Storage Capacity | The storage size in MB.  | No | No
Model Name | Attribute of type String. Automatically populated model name that will be presented in the Sandbox diagram | No | Yes


#####  Generic Power Port

Attribute Name | Details | User input? | Family Attribute?
--- | --- | --- | ---
Model | | No | No
Serial Number | | No | No
Version | | No | No
Port Description | | No | No
Model Name | Attribute of type String. Automatically populated model name that will be presented in the Sandbox diagram | No | Yes



## Commands
The following chapter describes the list of commands that needs to be supported by the shell. it includes command name, parameters and description of the functionality.

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



### Save
```python
def save (folder_path)  
```  
###### Description
Save a snapshot of the Compute server

###### Display Name
Save  

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | folder_path | string | no | the path in which the configuration file will be saved. Won’t include the name of the file but only the folder. This input is optional and in case this input is empty the value will be taken from the “Backup Location” attribute on the root resource. The path should include the protocol type (for example “tftp://asdf”)
Output | | string | yes | The configuration file name should be “[ResourceName]-[ConfigurationType]-[DDMMYY]-[HHMMSS]”




### Restore
```python
def restore (path)
```  
###### Description
Restore a snapshot of the Compute server

###### Display Name
Restore  


###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | path | string | no | the path to the configuration file, including the configuration file name. The path should include the protocol type (for example “tftp://asdf”). This input is mandatory



### Restart
```python
def restart()
```  
###### Description
Sends a restart request to the compute server

###### Display Name
Restart  

###### Parameters
None.




### Save & Restore in sandbox orchestration  
The shell must implement the save and restore commands and is responsible on saving and restoring its own state. The standard specifies the interface and functionality that shells expose to the sandbox orchestration. These two commands are hidden from the end user, their interface uses .json protocol and they should only be used by the sandbox orchestration via API.


```python
def orchestration_save (mode="shallow", custom_params = null)
```

```python
def orchestration_restore (saved_details)
```

**For more details:** [Orchestration Standard - Save & Restore ](http://goo.gl/L8pUjP)
