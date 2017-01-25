# PDU Shell Standard

#### Version 2.0.0


## Introduction
The PDU Shell Standard is a project used to define a standard for all PDU Shells that integrate with CloudShell. The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in the PDU Shells development and customization.



## Revision History

Version | Date | Notes
--- | --- | ---
2.0.0 | 2017-01-23 | Changed the type of the following attributes to "Password": "SNMP Read Community", "SNMP Write Community" and "SNMP V3 Password". This change is NOT backwards compatible
1.1.0 | 2016-08-25 | 1. Removed the Power Managed Device family from the standard. For a generic resource with a power port please refer to the Resource standard (generic Shell). 2. Attributes which aren't user-input changed from being read-only to having the rule "Admin only" enabled. 3. Behavior of setting the resource live status on poewr on/off/cycle was clarified in the commands notes section.
1.0.0 | 2016-07-04 | First release of the PDU Shell Standard


## Definitions
### Granularity
A PDU Shell should support all PDU devices of the same Vendor. For example, a correct shell granularity will be “Raritan PDU” and not “Raritan PDU PX2”.

### Specific Models Certification
Each release Shell should have a list of certified models. Model certification can be done only by Quali’s engineering, and validates that all the Shell’s capabilities are working for a specific model.
The Shell should also work for non-certified models, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the model certified.

### Generic Data Model
All PDU Shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all networking Shells and their values are populated by the driver. It is allowed to add custom attributes only to the root level model, and it isn’t allowed to remove attributes from any level.

### Versioning
The shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.

### Dependencies
In case the  shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-pdu-raritan 2.1.X”.
The dependency to cloudshell-automation-api will be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).



## Data Model Structure
### Families & Models
The PDU Shell Standard supports PDUs with power sockets.


#### PDU Data Model
- PDU
  - Power Socket

##### Example:

- Family: PDU, Model: Raritan PDU
  - Family: Power Socket, Model: Generic Power Socket


In order for the PDU shell to be used correctly within CloudShell both the PDU and devices connected to the PDU should be modeled in CloudShell, and the PDU sockets should be defined as “physically connected” to the devices power ports. Once this configuration is in place the devices connected to the PDU will get the “Power On”, “Power Off” and “Power Cycle” commands and those commands will be applicable on the power ports. The power ports can be defined on any type of device (for example, a networking device). The PDU shell comes with an OOB power managed device model that can be used to model in CloudShell a device connected to the PDU via a power port.



#### Family Rules
The following CloudShell family rules are enabled per family in the data model:

Family | Rules
--- | ---
PDU | Searchable, IsPowerSwitch
Power Socket | Searchable, Connectable, Locked By Default

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
PDU | [Vendor] PDU | (user defined) | Searchable
Power Socket | Generic Power Socket | (name in device) | (name in device)


## Attributes
#### Guidelines
- Attributes which aren’t relevant to a device won’t be populated by the driver.
- All attributes which aren't user-input should have the rule "Admin only" enabled.
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### [Vendor] PDU

Attribute Name | Details | User input?
--- | --- | ---
User | User with administrative privileges | Yes
Password | Attribute of type Password | Yes
Firmware Version | | No
Vendor | | No
Model | | No
SNMP Read Community | Attribute of type Password | Yes
SNMP Write Community | Attribute of type Password | Yes
SNMP V3 User | | Yes
SNMP V3 Password | Attribute of type Password | Yes
SNMP V3 Private Key | | Yes
SNMP Version | Possible values – v1, v2c, v3 | Yes
Console Server IP Address | | Yes
Console User | | Yes
Console Port | Attributes of type Numeric | Yes
Console Password | Attribute of type Password | Yes
CLI Connection Type | Attribute of type Lookup. Possible values – Auto, Console, SSH, Telnet, TCP | Yes
Sessions Concurrency Limit | Numeric, default is 1 (no concurrency) | Yes


#####  Generic Power Socket

No Attributes


## Commands
The following chapter describes the list of commands that needs to be supported by the shell. It includes command name, parameters and description of the functionality.

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





## Power Commands
  In CloudShell users can trigger a power commands directly from the power managed resource, doing that implicitly triggers the command execution on the PDU.

  To enable this feature, power commands must include the 'power' tag.

  ```xml
  <Driver Name="SamplePowerDriver" Version="1.0.0" MainClass="SamplePowerDriver.SamplePowerDriver" Description="">
    <Layout>
      <Category Name="Power">
        <Command Name="PowerOn" Description="" Tags="power"></Command>
        <Command Name="PowerOff" Description="" Tags="power"></Command>
        <Command Name="PowerCycle" Description="" Tags="power"></Command>
      </Category>
    </Layout>
  </Driver>
  ```  


### Power On
```python
def PowerOn(context, ports):     
```  
###### Description
Starts the power for the selected socket.

###### Notes
This command sets the live status of the resource connected to the PDU to "Online" with description "Resource powered on".

###### Display Name
Power On  

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | context | object | system parameter  | object of type ResourceRemoteCommandContext the details of the resource that triggered the power command.
Input | ports | list[string] | system parameter | This parameter includes the power socket ports that the resource is connected to.




### Power Off
```python
def PowerOff(context, ports):     
```    
###### Description
Stops the power for the selected socket.

###### Notes
This command sets the live status of the resource connected to the PDU to "Offline" with description "Resource powered off".

###### Display Name
Power Off  

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | context | object | system parameter  | object of type ResourceRemoteCommandContext the details of the resource that triggered the power command.
Input | ports | list[string] | system parameter | This parameter includes the power socket ports that the resource is connected to.




### Power Cycle
```python
def PowerCycle(context, ports, delay):     
```  
###### Description
Stops and then starts the power for the selected socket.   - CLI based

###### Notes
This command sets the live status of the resource connected to the PDU to "Online" with description "Resource powered on".

###### Display Name
Power Cycle

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | context | object | system parameter  | object of type ResourceRemoteCommandContext the details of the resource that triggered the power command.
Input | ports | list[string] | system parameter | This parameter includes the power socket ports that the resource is connected to.
Input | delay | string | No |  Optional. If kept empty the default from the The value here should be a positive integer and defines the wait time between the power off and power on. If left empty the default from the device will be used.
