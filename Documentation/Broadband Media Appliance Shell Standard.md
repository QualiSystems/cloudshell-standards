# Broadband Media Appliance Shell Standard

#### Version 1.0.0


## Introduction
The Broadband Media Appliance Shell standard defines a broadband media appliance integration with CloudShell. A broadband media appliance can be a cable modem, set-top boxes (STB) and more. The standard defines the Shell's data model, commands and a set of guidelines that should be followed in Broadband Media Appliance Shell development and customization.

## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2017-09-01 | First release of the Broadband Media Appliance Standard


## Definitions
### Generic Data Model
All Broadband Media Appliance Shells share the same generic data model, except the model of the root level which is different per each Shell. The data model shouldn’t be modified.
The attributes associated with those generic models are also shared by all broadband media appliance Shells and their values are populated by the driver. It is allowed to add custom attributes only to the root level model, and it isn’t allowed to remove attributes from any level.

### Versioning
The Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.

### Dependencies
In case the broadband media appliance shell is written in Python and has dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions, for example to “cloudshell-broadbandmedia 2.1.X”.
The dependency to cloudshell-automation-api will be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).


## Data Model
### Families & Models 

Broadband Media Chassis
   - Media Port
   - WiFi Card
   - Power Port

##### Example

Family: Broadband Media Chassis, Model: Arris Docsis Media Chassis
   - Family: Port, Model: Generic Media Port
   - Family: WiFi Card, Model: Generic WiFi Card
   - Family: Power Port, Model: Genric Power Port 

#### Family Rules

Family | Rules
--- | ---
Broadband Media Chassis | Searchable
Port | Searchable, Connectable, Locked By Default
WiFi Card | Searchable
Power Port | Searchable, Connectable, Locked By Default

#### Resource Name and Address
Family | Model | Resource Name | Resource Address
--- | --- | --- | ---
Broadband Media Chassis | [Vendor] [OS] Media Chassis | (user defined) | (user defined - IP)
Port | Generic Media Port | The name of the interface as appears in the device with the prefix "Eth_" or "Coax_" or "Phone_" or "FW_" or "HDMI_" according to Media Type attribute value. Any “/” character is replaced with “-“, spaces trimmed. | (taken from the device)
WiFi Card | Generic WiFi Card | WF[ID] | WF[ID]
Power Port | Generic Power Port | PP[ContainerID][ID] | PP[ContainerID][ID]

Note: The [ID] for each sub-resource is taken from the device itself (corresponds to the names defined in the device).

## Attributes
#### Guidelines
- Attributes which aren’t relevant to the specific virtual network won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### Broadband Media Chassis

Attribute Name | Data Type | User Input? | Description
--- | --- | --- | --- 
Chipset | String | No | Description of the chipset used by this broadband media appliance
Subscriber ID | String | No |
Account Number | String | No | 
User | String | Yes | User with administrative privileges
Password | Password | Yes | 
Enable Password | Password | Yes | The enable password is required by some CLI protocols such as Telnet and is required according to the device configuration.
Power Management | Boolean | Yes | Used by the power management orchestration, if enabled, to determine whether to automatically manage the device power status
System Name | String | No | A unique identifier for the device, if exists in the device terminal/os.
Vendor | String | No | 
Contact Name | String | No | The name of a contact registered in the device.
Location | String | No | he device physical location identifier. For example: Lab1/Floor2/Row5/Slot4
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Model Name | String | No | Automatically populated model name that will be presented in the Sandbox diagram
Sessions Concurrency Limit | Numeric | Yes | The maximum number of concurrent sessions that the driver will open to the device. Default is 1 (no concurrency).
Version | String | No | 
Serial Number | String | No | 
OS Version | String | No | Version of the Operating System.
SNMP Read Community | Password | Yes | The SNMP Read-Only Community String is like a password. It is sent along with each SNMP Get-Request and allows (or denies) access to device.
SNMP Write Community | Password | Yes | The SNMP Write Community String is like a password. It is sent along with each SNMP Set-Request and allows (or denies) chaning MIBs values.
SNMP V3 User | String | Yes | Relevant only in case SNMP V3 is in use.
SNMP V3 Password | Password | Yes | Relevant only in case SNMP V3 is in use.
SNMP V3 Private Key | String | Yes | Relevant only in case SNMP V3 is in use.
SNMP Version | String | Yes | The version of SNMP to use. Possible values are v1, v2c and v3.
Enable SNMP | Boolean | Yes | If set to True and SNMP isn’t enabled yet in the device the Shell will automatically enable SNMP in the device when Autoload command is called. SNMP must be enabled on the device for the Autoload command to run successfully. True by default.
Disable SNMP | Boolean | Yes | If set to True SNMP will be disabled automatically by the Shell after the Autoload command execution is completed. False by default.
Console Server IP Address | String | Yes | The IP address of the console server, in IPv4 format.
Console User | String | Yes | 
Console Port | Numeric | Yes | The port on the console server, usually TCP port, which the device is associated with. Default is 0.
Console Password | Password | Yes
CLI Connection Type | Lookup | Yes | The CLI connection type that will be used by the driver. Possible values are Auto, Console, SSH, Telnet and TCP. If Auto is selected the driver will choose the available connection type automatically. Default value is Auto.
CLI TCP Port | Numeric | Yes | TCP Port to user for CLI connection. If kept empty a default CLI port will be used based on the chosen protocol, for example Telnet will use port 23.
Backup Type | String | Yes | Supported protocols for saving and restoring of configuration and firmware files. Possible values are "File System", "FTP" and "TFTP". Default value is "File System".
Backup User | String | Yes | Username for the storage server used for saving and restoring of configuration and firmware files.
Backup Password | Password | Yes | Password for the storage server used for saving and restoring of configuration and firmware files.
Backup Location | String | Yes | The location in which configuration files will be saved in case no backup location input is passed to the Save command.
TR069 User | String | Yes |
TR069 Password | Password | Yes | 

##### Generic Power Port

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Model | String | No | The device model. This information is typically used for abstract resource filtering.
Serial Number | String | No |
Version | String | No | The firmware version of the resource.
Port Description | String | No | The description of the port as configured in the device.


##### Generic Media Port

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Media Type | String | No | Values can be "Ethernet", "Coax", "Phone", "Firewire" or "HDMI".
Transport Technology | String | No | Voice Packet Transmistion Type (e.g. SIP/MGCP)
MAC Address | String | No | 
IPv4 Address | String | No | 
IPv6 Address | String | No | 
Bandwidth | Numeric | No | The current interface bandwidth, in MB.
Class of Service | String | No | The current Class (or type) of Service to this device; Programs, Package or Contract names acceptable
Public IP | String | No | Public facing IP Address (vs. internal network IP)
Core Platform | String | No | The core services platform the port is currently provisioned for.
Telephone Number | String | No | Current phone number assigned to this port, relevant for a phone port.


##### WiFi Card

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
MAC Address | String | No | 
WiFi Protocol | String | No | Wi-Fi protocol type (e.g. 802.11n, 802.11ac)
Chipset | String | No | Description of the chipset used by this broadband media appliance
Frequency | String | No | Values can be "2.5 GHz" or "5 GHz"


## Commands
The following chapter describes the list of commands that needs to be supported by the shell. It includes command name, parameters and description of the functionality. Each virtual networking shell that will be released by Quali's engineering will include implementation for all those commands.

**Interface Implementation** - When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

**Error Handling**: Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output.


### [Vendor] [OS] Switch or [Vendor] [OS] Router - one VM & multi VMs solutions


#### Autoload
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

#### Save
```python
def save (self, context, folder_path, configuration_type)
```

###### Description
Create and save a configuration file

###### Notes
This command isn't a hidden command and should be visible in the UI.

###### Display Name
Save

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | folder_path | Folder Path | string | No | The path in which the configuration file will be saved. Shouldn't include the name of the file but only the folder. This input is optional and if empty the value will be taken from the "Backup Location" attribute on the root resource. The path should include the protocol type, for TFTP use "tftp://server_address/folder1", for FTP use "ftp://username:password@server_address/folder1".
Input | configuration_type | Configuration Type | string | No | The type of configuration that will be saved. Possible values are StartUp and Running. If kept empty the default configuration type that will be used is Running.
Output | | | string | Yes | <FullFileName>. The configuration file name should be “[ResourceName]-[ConfigurationType]-[DDMMYY]-[HHMMSS]”.

#### Restore
```python
def restore (self, context, path, configuration_type, restore_method)
```

###### Description
Restore a configuration file

###### Notes
This command isn't a hidden command and should be visible in the UI.

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
def load_firmware (self, context, path)
```

###### Description
Loads a firmware onto the device

###### Notes
This command is CLI based and applies to the whole device, also in case of multi-chassis device.
This command isn't a hidden command and should be visible in the UI.

###### Display Name
Load Firmware

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | path | Path | string | Yes | The path to the firmware file, including the firmware file name. The path should include the protocol type, for TFTP use "tftp://server_address/folder1/file1.bin", for FTP use "ftp://username:password@server_address/folder1/file1.bin".

#### Run Custom Command
```python
def run_custom_command (self, context, custom_command)
```

###### Description
Executes any custom command entered in the input on the device.

###### Notes
This command isn't a hidden command and should be visible in the UI.

###### Display Name
Run Custom Command

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | custom_command | Custom Command | string | Yes | The command to execute. Note that commands that require a reponse aren't supported.

#### Run Custom Config Command
```python
def run_custom_config_command (self, context, custom_command)
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
def shutdown(self, context)
```

###### Description
Sends a graceful shutdown to the device.

###### Notes
Not all devices support a shutdown command. In such cases the command just won’t be implemented.
This command isn't a hidden command and should be visible in the UI.

###### Display Name
Shutdown

###### Parameters
No input parameters.

### Health Check
```python
def health_check(self, context)
```

###### Description
Performs checks on the device that validates that the Shell can work. In a networking device this checks usually include connectivity check for the protocols used by the Shell. The healtcheck result will be visible in the resource live status and command output.

###### Notes
In case the performed checks fail the live status of the resource should be "Error" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] failed".
In case all performed checks passed the live status of the resource should be "Online" and both the live status description and the output of the command should be "Health check on resource [root_resource_name] passed".
CLI check is the check that is currently supported by the networking devices.
This command isn't a hidden command and should be visible in the UI.

###### Display Name
Health Check

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Output | | | string | Yes | The health check result

### Save & Restore in sandbox orchestration  
The shell must implement the save and restore commands and is responsible on saving and restoring its own state. The standard specifies the interface and functionality that shells expose to the sandbox orchestration. These two commands are hidden from the end user, their interface uses .json protocol and they should only be used by the sandbox orchestration via API.


```python
def orchestration_save (mode="shallow", custom_params = null)
```

```python
def orchestration_restore (saved_details)
```

**For more details:** [Orchestration Standard - Save & Restore ](http://goo.gl/L8pUjP)