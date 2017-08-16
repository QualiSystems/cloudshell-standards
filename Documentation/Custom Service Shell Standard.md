# Custom Service Shell Standard

#### Version 1.0.0


## Introduction
The Custom Service Shell standard defines a generic service that integrates with CloudShell. A service can be anything that needs to be represented in the Sandbox diagram and has some automation associated with it. A service is not managed in the inventory and can't be connected to other entities in the Sandbox using CloudShell's L1/L2/L3 connectivity.

Once a service shell is loaded into CloudShell it should be associated with a category in order to be published to the Services catalog of the relevant domain.

This standard is dedicated for custom work. There are other service shell standards for more specific use cases, such as cloud service shell standard and traffic controller shell standard.

## Revision History

Version | Date | Notes
--- | --- | ---
1.0.0 | 2017-16-08 | First release of the Custom Service Shell Standard


## Definitions
### Versioning
The Shell version follows Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Path version is promoted when making backward-compatibility bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a  Major version is promoted when making a backwards incompatible changes.


## Data Model Structure

### Families & Models 

Generic Service

#### Example

Family: Generic Service, Model: [Shell name]

Family: Generic Service, Model: Custom power service

#### Family Rules

Family | Rules
--- | ---
Generic Service | Service Template

### Category

No default category association.


## Attributes
#### Guidelines
- Attributes which aren’t relevant to the specific virtual network won’t be populated by the driver.
- All attributes which aren't user-input are "read only"
- Attributes shouldn’t be removed.
- Custom attributes should be added only to the root level model.
- All attributes are of type String unless mentioned otherwise

##### Generic Service (attributes associated with the family)

No attributes.

## Commands
The following chapter describes the list of commands that needs to be supported by the shell. It includes command name, parameters and description of the functionality. Each virtual networking shell that will be released by Quali's engineering will include implementation for all those commands.

**Interface Implementation** - When creating a new shell according to the standard it is OK not to implement all commands and/or implement additional command, but a command with a functionality that fits one of the predefined list commands should be implemented according to the standard.

**Error Handling**: Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output.


### Generic Service

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
