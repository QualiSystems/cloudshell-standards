# Cloud Service Shell Standard

#### Version 1.0.0


## Introduction
The Cloud Service Shell standard defines how a cloud service integrates with CloudShell. A cloud service can be anything that needs to be represented in the Sandbox diagram and has some automation associated with it. A service is not managed in the inventory and can't be connected to other entities in the Sandbox using CloudShell's L1/L2/L3 connectivity.

Once a service shell is loaded into CloudShell it should be associated with a category in order to be published to the Services catalog of the relevant domain.

This standard is dedicated for cloud services, such as AWS CloudFront service, Azure Load Blanacer etc.

## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2017-08-16 | First release of the Cloud Service Shell Standard


## Definitions
### Versioning
The Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.


## Data Model Structure

### Families & Models 

Cloud Service

#### Example

Family: Cloud Service, Model: [Shell name]

Family: Cloud Service, Model: AWS CloudFront Service

#### Family Rules

Family | Rules
--- | ---
Cloud Service | Service Template

### Category

Importing this shell will associate the Cloud Service family with the following category:

Cloud Services

## Attributes
#### Guidelines
- Attributes which aren’t relevant to the specific cloud service won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### Cloud Service (attributes associated with the family)

Attribute Name | Data Type | User Input? | Description
--- | --- | --- | ---
Address | String | Yes | 
User | String | Yes | User with administrative privileges
Password | Password | Yes | 
Cloud Provider | String | Yes | Cloud provider resource name

## Commands
The following chapter describes the list of commands that needs to be supported by the shell. It includes command name, parameters and description of the functionality. Each cloud service shell that will be released by Quali's engineering will include implementation for all those commands.

**Interface Implementation** - When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

**Error Handling**: Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, cloud service or the command infrastructure itself. On success the command will just return as passed with no output.


### Cloud Service

#### Example Command
```python
def example_function (self, context)
```

###### Description
Just an example for a regular command

###### Notes
This command doesn't do anything, it is just here as an example.

###### Display Name
Example Command

###### Parameters

No parameters.

#### Example Commands With Parameters
```python
def example_function_with_params (self, context, user_param1, user_param2)
```

###### Description
Just an example for a regular command with parameters.

###### Notes
This command doesn't do anything, it is just here as an example.

###### Display Name
Example Command With Params

###### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | user_param_1 | User Parameter 1 | string | Yes | Example string input. Has a default value "some default".
Input | user_param_2 | User Parameter 2 | lookup | Yes | Example lookup input. Allowed values are Yes and No.
