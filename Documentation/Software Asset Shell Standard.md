# Software Asset Shell Standard

#### Version 1.0.0


## Introduction
The Software Asset Shell Standard defines a standard for all software assets  that integrate with CloudShell. The standard defines the Shell's data model, commands and a set of guidelins that should be followed in softwer asset Shell development and customization.

A software asset is any software that is installed and configured outside of CloudShell, but is used as an asset in Sandboxes. The Shell allows modelling such software assets in CloudShell inventory with all the information required in order to access and provision it.


## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2017-06-05 | First release of the Software Asset Shell Standard


## Definitions
### Versioning
The Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.


## Data Model Structure

The software asset can either be modeled as a root level entity only or as a group of services. Group of services modelling can apply to a software which is multi-tier or one which consists of multiple services for redundancy. Similar services or ones with similar role can be grouped under a "Service Group". 

### Families & Models

Software Asset
   - Service
   - Service Group
      - Service



##### Example:

Family: SoftwareAsset, Model: (user defined)
   - Family: SoftwareService, Model: Service
   - Family: SoftwareServiceGroup, Model: Service Group


#### Family Rules

Family | Rules
--- | ---
SoftwareAsset | Searchable, Shared By Default, Application
SoftwareService | Searchable, Shared By Default, Application
SoftwareServiceGroup | Searchable, Shared By Default, Application


## Attributes
#### Guidelines
- Attributes which aren’t relevant to the software asset won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### Software Asset

Attribute Name | Details | User input? | Rules
--- | --- | --- | ---
User | User with administrative privileges | No | Configuration, Setting, Admin Only
Password | Attribute of type Password | No | Configuration, Setting, Admin Only
Version | The version of the application | No | Setting, Available for Abstract Resources, Admin Only
Vendor | The name of the device manufacture. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Contact Name | The name of a contact registered in the device. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Location | The device physical location identifier. For example: Lab1/Floor2/Row5/Slot4 | No | Configuration, Available for Abstract Resources, Admin Only
Model | The device model. This information is typically used for abstract resource filtering. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Access Protocol | | No | Configuration, Setting, Admin Only
Access Port | | No | Configuration, Setting, Admin Only
Public IP | | No | Configuration, Setting, Admin Only
Connected Assets | A comma separated list of connected software assets (optional) | No | Configuration, Setting
OS Architecture | | No | Configuration
OS Type | | No | Configuration
OS Distribution | | No | Configuration
OS Version | | No | Configuration


##### Service

Attribute Name | Details | User input? | Rules
--- | --- | --- | ---
User | User with administrative privileges | No | Configuration, Setting, Admin Only
Password | Attribute of type Password | No | Configuration, Setting, Admin Only
Version | The version of the application | No | Setting, Available for Abstract Resources, Admin Only
Vendor | The name of the device manufacture. | No | Configuration, Setting, Avilable for Abstract Resources, Admin Only
Contact Name | The name of a contact registered in the device. | No | Configuration, Setting, Avilable for Abstract Resources, Admin Only
Location | The device physical location identifier. For example: Lab1/Floor2/Row5/Slot4 | No | Configuration, Avilable for Abstract Resources, Admin Only
Model | The device model. This information is typically used for abstract resource filtering. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Access Protocol | | No | Configuration, Setting, Admin Only
Access Port | | No | Configuration, Setting, Admin Only
Public IP | | No | Configuration, Setting, Admin Only
OS Architecture | | No | Configuration
OS Type | | No | Configuration
OS Distribution | | No | Configuration
OS Version | | No | Configuration

#####  Service Group

Attribute Name | Details | User input? | Rules
--- | --- | --- | ---
Service Group Name | | No | Setting, Available for Abstract Resources, Admin Only
Version | The version of the application | No | Setting, Available for Abstract Resources, Admin Only
Vendor | The name of the device manufacture. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Model | The device model. This information is typically used for abstract resource filtering. | No | Configuration, Setting, Available for Abstract Resources, Admin Only
Connected Assets | A comma separated list of connected software assets (optional) | No | Settings, Configuration
OS Architecture | | No | Configuration
OS Type | | No | Configuration
OS Distribution | | No | Configuration
OS Version | | No | Configuration


## Commands
The following chapter describes the list of commands that needs to be supported by the shell. It includes command name, parameters and description of the functionality.

**Interface Implementation** - When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

**Error Handling**: Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output.



### Get Inventory (Shell Autoload)
```python
def get_inventory(self, context)
```

###### Description
This function queries the software assetand validates that it is accessible and its configuration paraemters are correct. When a new resource is created, CloudShell asks the user to specify some user inputs (i.e user name & password) and then it calls the get_inventory function.


###### Display Name
System command, it has no display name.


###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | context | object | system parameter | object of type AutoLoadCommandContext which includes API connectivity details and the details of the resource including attributes that the user entered during the resource creation.
Output | AutoLoadDetails | object | Yes | object of type AutoLoadDetails which the discovered resource structure and attributes.



