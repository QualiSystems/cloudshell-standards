# Firewall Shell Standard

#### Version 3.0.0


## Introduction
The Firewall Shell Standard is a project used to define a standard for all Firewall Shells that integrate with CloudShell. The standard defines the Shell’s data model, commands and a set of guidelines that should be followed in Firewall Shells development and customization.



## Revision History

Version | Date | Notes
--- | --- | ---
3.0.0 | 2017-01-23 | 1) Added letters to resources address. 2) Changed the type of the following attributes to "Password": "SNMP Read Community", "SNMP Write Community" and "SNMP V3 Password". Those changes are NOT backwards compatible.
2.0.0 | 2016-08-16 | 1) Added a new attribute named “CLI TCP Port” on the root model. That attribute will be filled in by the administrator (optional). 2)  The "Configuration Type" input in the Save and Restore command is now not mandatory, the default value if kept empty is Running. 3) Descriptions were added to the attributes, commands and command inputs (only commands visible in the UI). 4) A “Health check” command was added. This command performs checks on the device that validates that the Shell can work. In a firewall device this checks usually include connectivity check for the protocols used by the Shell. 5) Removed the attribute “Protocol Type” from the standard. 6) Added the attributes “Enable SNMP” and “Disable SNMP” on the root model. Those attribute will allow automatic configuration of SNMP before and after the execution of the Autoload command which requires SNMP. 7) The value of the attribute “Bandwidth” is now in MB instead of Bytes. 8) Added orchestration_save and orchestration_restore commands according to the Save and Restore Orchestration Standard. Those commands wrap the Shell’s Save and Restore commands with a standard interface to be used by the Sandbox orchestration. 9) The command name and command input names are now defined in the standard. Prior to this standard version only the command alias and command input aliases were defined. 10) The inputs of the load_firmware command were changed and alligned with the inputs of the restore command. 11) The expected syntax of the path and folder_path inputs of the restore, load_firmware and save commands in case of FTP protocol was clarified. **The 9th and 10th items aren't backwards compatible and will require modification of any existing automation which calls the Shell’s commands. However, upcoming shells will still have the old commands available as hidden command so the shells themselves will remain backwards compatible until their next major verion.**
1.0.0 | 2016-06-23 | First release of the Firewall Shell Standard


## Definitions
### Granularity
A Firewall Shell should support all Firewall devices with the same Vendor and OS. For example a correct shell granularity will be “Cisco ASA Shell” and not “Cisco ASA 5500 Shell”.

### Specific Models Certification
Each released Shell should have a list of certified models. Model certification can be done only by Quali’s engineering, and validates that all the Shell’s capabilities are working for a specific model.
The Shell should also work for non-certified models, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the model certified.

### Generic Data Model
All Firewall Shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all firewall Shells and their values are populated by the driver. It is allowed to add custom attributes only to the root level model, and it isn’t allowed to remove attributes from any level.

### Versioning
The Firewall Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.

### Dependencies
In case the Firewall shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-firewall-cisco-asa 2.1.X”.
The dependency to cloudshell-automation-api will be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).



## Data Model
### Families & Models
The firewall shell standard supports Firewall devices.

#### Firewall Data Model
- Firewall
 - Chassis
    - Module
       - Port
       - Sub Module
          - Port
    - Port
    - Power Port
 - Port Channel

##### Example:

- Family: Firewall, Model: Cisco ASA Firewall
 - Family: Chassis, Model: Generic Chassis
    - Family: Module, Model: Generic Module
       - Family: Port, Model: Generic Port
       - Family: Sub Module, Model: Generic Sub Module
          - Family: Port, Model: Generic Port
    - Family: Port, Model: Generic Port
    - Family: Power Port, Model: Generic Power Port
 - Family: Port Channel, Model: Generic Port Channel


#### Family Rules

Family | Rules
--- | ---
Firewall | Searchable
Chassis | Searchable
Module | Searchable
Sub Module | Searchable
Port | Searchable, Connectable, Locked By Default
Port Channel | Searchable, Connectable, Locked By Default
Power Port | Searchable, Connectable, Locked By Default


#### Port Channel Usage

The Port Channel is a logical entity that allows grouping of several physical ports to create one logical link.
In CloudShell, all the ports configured to the port channel shouldn’t be “physically connected” and instead the port channel resource will be “physically connected”. The names of all the ports configured to the port channel will appear in the “Associated Ports” attribute on the port channel.
Addition or removal of ports from the port channel will require execution of Autoload to update the resource representation in CloudShell and a manual update of the physical connections in CloudShell by the administrator.

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Firewall | [Vendor] [OS] Firewall | (user defined) | (user defined - IP)
Chassis | Generic Chassis | Chassis[ID] | CH[ID]
Module | Generic Module | Module[ID] | MO[ID]
Sub Module | Generic Sub Module | SubModule[ID] | SM[ID]
Port | Generic Port | The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed.] | PO[ID]
Port Channel | Generic Port Channel | The name of the interface as appears in the device. Any “/” character is replaced with “-“, spaces trimmed. | PC[ID]
Power Port | Generic Power Port | PP[ContainerID][ID] | PP[ContainerID][ID]

Note: The [ID] for each sub-resource is taken from the device itself (corresponds to the names defined in the device).


### Attributes
#### Guidelines
- Attributes which aren’t relevant to a devices won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- The attribute rules are as follows - all attributes which are user input should have the rule "Configuration" enabled, all attributes which aren't user input should have the rules "Settings" and "Available For Abstract Resources" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### [Vendor] [OS] Firewall

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
User | String | Yes |
Password | Password | Yes |
Enable Password | Password | Yes | The enable password is required by some CLI protocols such as Telnet and is required according to the device configuration.
System Name | String | No | A unique identifier for the device, if exists in the device terminal/os.
Contact Name | String | No | The name of a contact registered in the device.
OS Version | String | No | Version of the Operating System.
Vendor | String | No | The name of the device manufacture.
Location | String | No | The device physical location identifier. For example Lab1/Floor2/Row5/Slot4.
Model | String | No | The device model. This information is typically used for abstract resource filtering.
SNMP Read Community | Password | Yes | The SNMP Read-Only Community String is like a password. It is sent along with each SNMP Get-Request and allows (or denies) access to device.
SNMP Write Community | Password | Yes | The SNMP Write Community String is like a password. It is sent along with each SNMP Set-Request and allows (or denies) chaning MIBs values.
SNMP V3 User | String | Yes | Relevant only in case SNMP V3 is in use.
SNMP V3 Password | Password | Yes | Relevant only in case SNMP V3 is in use.
SNMP V3 Private Key | String | Yes | Relevant only in case SNMP V3 is in use.
SNMP Version | String | Yes | The version of SNMP to use. Possible values are v1, v2c and v3.
Console Server IP Address | String | Yes | The IP address of the console server, in IPv4 format.
Console User | String | Yes |
Console Port | Numeric | Yes | The port on the console server, usually TCP port, which the device is associated with.
Console Password | Password | Yes |
CLI Connection Type | Lookup | Yes | The CLI connection type that will be used by the driver. Possible values are Auto, Console, SSH, Telnet and TCP. If Auto is selected the driver will choose the available connection type automatically. Default value is Auto.
Power Management | Boolean | Yes | Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status. Enabled by default.
Backup Location | String | Yes | The location in which configuration files will be saved in case no backup location input is passed to the Save command.
Sessions Concurrency Limit | Numeric | Yes | The maximum number of concurrent sessions that the driver will open to the device. Default is 1 (no concurrency).
CLI TCP Port | String | Yes | TCP Port to user for CLI connection. If kept empty a default CLI port will be used based on the chosen protocol, for example Telnet will use port 23.
Enable SNMP | Boolean | Yes | If set to True and SNMP isn’t enabled yet in the device the Shell will automatically enable SNMP in the device when Autoload command is called. SNMP must be enabled on the device for the Autoload command to run successfully. True by default.
Disable SNMP | Boolean | Yes | If set to True SNMP will be disabled automatically by the Shell after the Autoload command execution is completed. False by default.


#####  Generic Chassis

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Serial Number | String | No |


#####  Generic Module

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Version | String | No | The firmware version of the resource.
Serial Number | String | No |


##### Generic Sub Module

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Version | String | No | The firmware version of the resource.
Serial Number | String | No |


##### Generic Port

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
MAC Address | String | No |
L2 Protocol Type | String | No | The L2 protocol type configured on the interface. For example POS, Serial.
IPv4 Address | String | No |
IPv6 Address | String | No |
Port Description | String | No | The description of the port as configured in the device.
Bandwidth | Numeric | No | The current interface bandwidth, in MB.
MTU | Numeric | No | The current MTU configured on the interface.
Duplex | Lookup | No | The current duplex configuration on the interface. Possible values are Half or Full.
Adjacent | String | No | The adjacent device (system name) and port, based on LLDP or CDP protocol.
Auto Negotiation | Boolean | No | The current auto negotiation configuration on the interface.


#####  Generic Port Channel

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Associated Ports | String | No | Ports associated with this port channel. The value is in the format “[portResourceName],…”, for example “GE0-0-0-1,GE0-0-0-2”
IPv4 Address | String | No |
IPv6 Address | String | No |
Port Description | String | No | The description of the port as configured in the device.


#####  Generic Power Port

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Serial Number | String | No |
Version | String | No | The firmware version of the resource.
Port Description | String | No | The description of the port as configured in the device.


## Commands
Below is a list of all the commands that will be part of the standard Shell, their names and interfaces. Each firewall Shell that will be released by Quali’s engineering will include implementation for all those commands.

When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output. The “Autoload” command has a special output on success that CloudShell reads when building the resource hierarchy. The “Save” command will return an output on success with the file name (exact syntax below).

Note that the connectivity ApplyConnectivityChanges command behaves differently between Switches and Routers. In Switches, the ApplyConnectivityChanges command can configure VLAN Access or VLAN Trunk on a port, or clear the VLAN configuration from the port. In Routers, the ApplyConnectivityChanges command creates a sub-interface (which isn't modeled in CloudShell) on the port which allows traffic with the specified VLAN tags (both outer and inner) to pass via this port. Clearing the VLAN configuration from a port in a Router translates to removal of the sub-interfaces. This means that a device which is directly connected to a router can be connected only to VLAN service of type Trunk in CloudShell.


### Autoload
```python
def get_inventory (self, context)
```

###### Description
This function queries the device, discovers it's specification and structure and autoload it into CloudShell. When new resource is created Cloudshell asks the user to specify some user input (i.e user name & psasword) and then it calls the get_inventory function.

###### Notes
The standard recommended way of communicating and discovering the device is via SNMP protocol and therefore this command requires SNMP to be configured in the device. In case SNMP isn’t configured in the device and the attribute “Enable SNMP” on the root model is set to True the Autoload command will configure SNMP in the device. If the attribute “Disable SNMP” on the root model is set to True the Autoload command will disable the SNMP in the device once the discovery of the device is completed. In case SNMP isn't configured and "Enable SNMP" on the root model is set to false a relevant error message will be displayed.

###### Display Name
System command, it has no display name

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | object | system parameter | object of type AutoLoadCommandContext which includes API connectivity details and the details of the resource including attributes that the user entered during the resource creation. | - | -
Output | AutoLoadDetails | - | object | Yes | object of type AutoLoadDetails with the discovered resource structure and attributes. | - | -

### Save
```python
def save (folder_path, configuration_type)
```

###### Description
Create and save a configuration file

###### Display Name
Save

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | folder_path | Folder Path | string | No | The path in which the configuration file will be saved. Won't include the name of the file but only the folder. This input is optional and in case this input is empty the value will be taken from the "Backup Location" attribute on the root resource. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".
Input | configuration_type | Configuration Type | string | No | The type of configuration that will be saved. Possible values are StartUp and Running. If kept empty the default configuration type that will be used is Running.
Output | | | string | Yes | <FullFileName>. The configuration file name should be “[ResourceName]-[ConfigurationType]-[DDMMYY]-[HHMMSS]”.

### Restore
```python
def restore (path, configuration_type, restore_method)
```

###### Description
Restore a configuration file

###### Display Name
Restore

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | path | Path | string | Yes | The path to the configuration file, including the configuration file name. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".
Input | configuration_type | Configuration Type | string | No | The configuration type to restore. Possible values are StartUp and Running. If kept empty the configuration type that will be restored is Running.
Input | restore_method | Restore Method | string | No | The restore method to use when restoring the configuration file. Possible Values are Append and Override. If kept empty the restore method will be Override.

### Load Firmware
```python
def load_firmware (path)
```

###### Description
Loads a firmware onto the device

###### Notes
This command is CLI based and applies to the whole device, also in case of multi-chassis device.

###### Display Name
Load Firmware

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | path | Path | string | Yes | The path to the firmware file, including the firmware file name. The path should include the protocol type, for TFTP use "tftp://asdf", for FTP use "ftp://username:password@server_address/folder1/file1.bin".

### Run Custom Command
```python
def run_custom_command (custom_command)
```

###### Description
Executes any custom command entered in the input on the device.

###### Display Name
Run Custom Command

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | custom_command | Custom Command | string | Yes | The command to execute. Note that commands that require a reponse aren't supported.

### Run Custom Config Command
```python
def run_custom_command (custom_command)
```

###### Description
Executes any custom config command entered in the input on the device.

###### Notes
This command should be hidden from the UI.

###### Display Name
Run Custom Config Command

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | custom_command | Custom Command | string | Yes | The command to execute. Note that commands that require a reponse aren't supported.

### Shutdown
```python
def shutdown()
```

###### Description
Sends a graceful shutdown to the device.

###### Notes
Not all devices support a shutdown command. In such cases the command just won’t be implemented.

###### Display Name
Shutdown

###### Parameters
No input parameters.

### Health Check
```python
def health_check()
```

###### Description
Performs checks on the device that validates that the Shell can work. In a firewall device this checks usually include connectivity check for the protocols used by the Shell. The healtcheck result will be visible in the resource live status and command output.

###### Notes
In case the performed checks fail the live status of the resource should be "Error" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] failed".
In case all performed checks passed the live status of the resource should be "Online" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] passed".
CLI check is the check that is currently supported by the networking devices.

###### Display Name
Health Check

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Output | | | string | Yes | The health check result

### orchestration_save
```python
def orchestration_save(mode="shallow", custom_params = null)
```

###### Notes
Based on the Orchestration Save and Restore Standard - https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md
The command wraps the Save command with a standard interface that will be used by the Sandbox orchestration. This command will call the Save command which will create a configuration file.
The command should be hidden from the UI.
In case there is no folder_path input and the attribute "Backup Location" on the root model is empty the command should throw an error.

###### Display Name
orchestration_save

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | mode | mode | string | Yes | The save mode. Possible values are "Shallow" and "Deep". In a firewall device both modes will have the same behavior of saving a configuration file.
Input | custom_params | custom_params | string | Yes | A JSON data structure with optional parameters. If no parameters are passed the defaults defined on the root resource and in the Save command will be used.
Output | saved_artifact_info | saved_artifact_info | string | Yes | A composite data structure that represents the details of the snapshot.

An example for the "custom_params" input:

```json
{
  "custom_params": {
    "configuration_type" : "StartUp"
    "folder_path" : "tftp://10.0.0.1/folder1"
  }
}
```

An example for the "saved_artifact_info" output:
```json
{
  "saved_artifact_info": {
    "resource_name": "CiscoNXOSSwitch1",
    "resource_id" : "5F2EAA6C-E3FD-4DF0-8E2D-F05C81D61631",
    "created_date": "3577-04-27T00:17:48.819Z",
    "restore_rules": {
      "requires_same_resource": true
    },    
    "saved_artifact" :{
      "artifact_type": "tftp",
      "identifier": "/folder1/CiscoNXOSSwitch1-Running-080816-13:20:53",
      "server": "server1"
    }
  }
}
```

The artifact types supported by firewall orchestration_save command are "ftp", "tftp" and "filesystem".
The "requires_same_resource" restore rule for firewall devices is always True.

### orchestration_restore
```python
def orchestration_restore(saved_artifact_info, custom_params = null)
```

###### Notes
Based on the Orchestration Save and Restore Standard - https://github.com/QualiSystems/sandbox_orchestration_standard/blob/master/save%20%26%20restore/save%20%26%20restore%20standard.md
The command wraps the Restore command with a standard interface that will be used by the Sandbox orchestration. This command will call the Save command which will create a configuration file.
The command should be hidden from the UI.
In case the saved artifact type is FTP the FTP credentials are saved on the FTP resource, so the orchestration_restore command will access the FTP resource to get them and pass them to the Restore command.

###### Display Name
orchestration_restore

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | saved_artifact_info | saved_artifact_info | string | Yes | A composite data structure that represents the details of the snapshot. The value that will be passed as input must be the same as the exact value that the save function returned.
Input | custom_params | custom_params | string | Yes | A JSON data structure with optional parameters. If no parameters are passed the defaults defined on the root resource and in the Restore command will be used.

An example for the "custom_params" input:

```json
{
  "custom_params": {
    "path" : "tftp://10.0.0.1/folder1"
    "restore_method" : "Append"
    "configuration_type" : "StartUp"
  }
}
```

An example for the "saved_artifact_info" input:
```json
{
  "saved_artifact_info": {
    "resource_name": "CiscoASAFirewall1",
    "resource_id" : "5F2EAA6C-E3FD-4DF0-8E2D-F05C81D61631",
    "created_date": "3577-04-27T00:17:48.819Z",
    "restore_rules": {
      "requires_same_resource": true
    },    
    "saved_artifact" :{
      "artifact_type" : "ftp",
      "ftp_resource" : "ftp_srv1", 
      "identifier": "/folder1/CiscoNXOSSwitch1-Running-080816-13:20:53"
    }
  }
}
```

The artifact types supported by firewall orchestration_restore command are "ftp", "tftp" and "filesystem".
The "requires_same_resource" restore rule for firewall devices is always True.
