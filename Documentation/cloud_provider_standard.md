# Cloud Provider Standard

#### Version 1.0.1


## Introduction
The Cloud Provider shell standard is a project used to define a new cloud provider in CloudShell. This custom cloud provider is used to extend the system, allowing deployment of applications to an additional private or public cloud. The cloud provider standard may also be used to implement deployment of applications as part of deployment containers.

A cloud provider shell may include more than one deployment type, allowing a variety of options to base the virtual instance on (for example, selecting the image from the marketplace or loading a custom one)


## Revision History

Version | Date | Notes
--- | --- | ---
1.0.1 | 2020-10-01 | Added Private IP attribute to the Deployment Option
1.0.0 | 2018-09-01 | First release of the Cloud Provider Shell Standard


## Definitions
### Granularity
The Cloud Provider Shell Standard defines two separate shells - a Shell for the cloud provider, and a contained service shell for each deployment type. The cloud provider shell defines the attributes and behavior of the cloud provider inventory resource, and contains the driver with the cloud provider specific logic for all deployment types.
The deployment type service shell contains the attributes of the deployment type, visible in the app form, and has no driver.

### Specific Versions Certification
Each released Shell should have a list of certified versions. Version certification can be done only by Quali’s engineering, and it includes validation that all the Shell’s capabilities are working for a specific version.
The Shell should also work for non-certified versions unless specified differently in the Shell's release notes, and in case some gaps are found a new version of the Shell will be released with the gaps addressed and the version certified.

### Versioning
The Cloud Provider and Deployment type Shell versions follow Semantic Versioning Guidelines (see details in http://semver.org). In short, the version structure is Major.Minor.Patch, for example “1.0.2”. A Patch version is promoted when making backward-compatible bug fixes, a Minor version is promoted when adding functionality in a backwards-compatible manner and a Major version is promoted when making any backwards incompatible change. The standard itself follows the same guidelines.

### Dependencies
The Cloud Provider and Deployment type shells are written in Python and have dependencies to Python packages (that follow Semantic Versioning Guidelines) the dependency should be to a range of Patch versions.
The dependency to cloudshell-automation-api should be to the latest Patch version (cloudshell-automation-api package version is of the format “CloudShell_Version.X”, for example 7.0.X”).



## Data Model
### Families & Models

The data model for the custom cloud provider include a model that is derived from CustomCloudProvider model,
representing the inventory cloud provider resource, and one or more models derived from the CustomDeploymentOption model.
The cloud provider model extension will include the attributes that control the behavior of the cloud provider as a whole, for example the region name,
default values for elements created in the cloud etc.
The deployment option extension needs to include the attributes that are needed for every method of deployment in
this cloud. These attributes may be visible in the deployment path tab of the app template form.

When creating a shell from the "cloud-provider" shell template, the projects includes a yaml file for the cloud provider
model definition, and a skeleton of the cloud provider model. Inside the "Deployments" folder there is a yaml file for the deployment option model. If more
than one deployment option is needed, additional yaml files may be added to that folder.

The association between the cloud provider and its relevant deployment options is implicit. A cloud provider shell will
have the deployment options contained in the "Deployments" folder in that shell


#### Cloud Provider Data Model
- CloudProvider
    - (no sub resources)

#### Deployment Option Data Model
- DeploymentOption
    - (no sub resources)



### Attributes
#### Guidelines
- Attributes which aren’t relevant to a device won’t be populated by the driver.
- All attributes which aren't user-input should have the rule "Admin only" enabled.
- It is possible to customize the attribute rules selection after importing the Shell to CloudShell.
- Attributes shouldn’t be removed.

##### Cloud Provider Model

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Networking type | String | Yes | networking type that the cloud provider implements- L2 networking (VLANs) or L3 (Subnets). Possible Values: L2, L3
Region | String | Yes | The public cloud region to be used by this cloud provider.
Networks in use | String | Yes | Reserved network ranges to be excluded when allocating sandbox networks (for cloud providers with L3 networking). The syntax is a comma separated CIDR list. For example "10.0.0.0/24, 10.1.0.0/26"
VLAN Type | String | Yes | whether to use VLAN or VXLAN (for cloud providers with L2 networking)

##### Deployment Option Model

Attribute Name | Data Type | User input? | Description
--- | --- | --- | ---
Autoload | boolean | Yes | Whether to call the autoload command during Sandbox setup (defaults to "true")
Wait for IP | boolean | Yes | if set to false the deployment will not wait for the VM to get an IP address (defaults to "true")
Private IP | string | Yes | Custom private IPs to be allocated to the VM's vNICs. IPs must be within the Subnet range. For example, "10.0.0.2,10.0.0.3-4;10.0.1.2,10.0.1.5,10.0.1.9."

## Commands
Below is a list of all the commands that need to be implemented in order to have a working custom cloud provider.

The driver is part of the cloud provider shell. The deployment options do not have a driver, so the cloud provider driver
implementation needs to take into account all the deployment options that this cloud provider will support.

Some of the commands are mandatory for all custom cloud providers, others are mandatory only for a specific networking type. So, if the
networking type is L2 Networking (VLANs), some commands are mandatory, and others are mandatory for L3 (Subnets).

The driver signature may include additional commands that are not listed here. These commands may be ignored, but not deleted.

Command outputs: On failure an exception containing the error will be thrown and the command will be shown as failed. A failure is defined as any scenario in which the command didn’t complete its expected behavior, regardless if the issue originates from the command’s input, device or the command infrastructure itself. On success the command will just return as passed with no output. The “Autoload” command has a special output on success that CloudShell reads when building the resource hierarchy.



### get_inventory
```python
def get_inventory(self, context)
```

#### Description
Called when the cloud provider resource is created
in the inventory.

The command should validate the values of the cloud provider attributes, entered by the user as part of the cloud provider resource creation.
For example, in a VCenter cloud provider, the get inventory command would check the value provided in data center attribute
to validate that such a datacenter exists in VC.
In addition, this would be the place to assign values pragmatically to optional attributes that were not given a value by the user.

If one of the validations failed, the command should raise an exception


#### Relevance
Mandatory for all cloud providers

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | AutoLoadCommandContext  | system parameter | | - | -
Output | | - | AutoLoadDetails | Yes |  | - | -

### Deploy
```python
def Deploy(self, context, request=None, cancellation_context=None)
```

#### Description
The Deploy command is probably the most important command of the cloud provider shell.
It is called for each app in the sandbox, and its purpose is to
create the compute resource in the cloud provider - VM instance or container.

If the cloud provider supports multiple deployment options, the Deploy command needs to implement the logic for all of them.
The active deployment option of the app is indicated by the "deploymentPath" field in the DeployApp action in the request.

In L2 Networking implementations, the compute resource would normally be associated to a default or management network,
and in a separate command call later in the setup flow (ApplyConnectivityChanges), the compute resource will need be connected to
the network.

In L3 connectivity implementations, we can have implementations that can be divided to two categories:
- Single subnet/network - all sandbox components implicitly are connected to a single network. In this case,
the compute resource needs to be connected  to the single network that exists in the sandbox (Created in CreateSandboxInfra command)
- Multiple subnet mode - Alternatively, an implementation may support modeling of subnets in the sandbox, and allow the
user to connect the apps to one network or the other by drawing connections in the sandbox.
The request will include the details of all the connectors that the compute resource needs to connect to. For each
of these connections required by the blueprint designer, a connection needs to be created (done in PrepareSandboxInfra command)

If the creation of the compute resource has failed, the entire operation will be considered failed. If One of the network connection
has failed, the response needs to reflect this failure. The sandbox will be in "Active with Error" mode but the instance will be created.



#### Relevance
Mandatory for all cloud providers

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Input | cancellation_context | - | CancellationContext | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -

### PowerOn
```python
def PowerOn(self, context, ports)
```

#### Description
The PowerOn command is used to power on (or bring online) the compute resource represented
by the app.
This command has no returned values (method with void return type).
In case of an error the command should raise an exception.
In case of success the server will mark the App component with a green circle live status
in order to indicate the user the compute resource is online.

#### Relevance
Mandatory for all cloud providers

#### Display Name
Power On

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceRemoteCommandContext | system parameter | | - | -
Input | ports | - | NA | system parameter | Legacy parameter, may be disregarded



### PowerOff
```python
def PowerOff(self, context, ports)
```

#### Description
The PowerOff command is used to power off (or bring offline) the compute resource represented
by the app.
This command has no returned values (method with void return type).
In case of an error the command should raise an exception.
In case of success the server will mark the app component with a grey circle live status
in order to indicate the user the compute resource is offline.

#### Relevance
Mandatory

#### Display Name
Power Off

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceRemoteCommandContext | system parameter | | - | -
Input | ports | - | NA | system parameter | Legacy parameter, may be disregarded



### DeleteInstance
```python
def DeleteInstance(self, context, ports)
```

#### Description
Deletes the compute resource.
The method is void.
If completed successfully the deployed app component will be deleted in cloudshell.
In case of error need to raise an exception.

#### Relevance
Mandatory for all cloud providers

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceRemoteCommandContext | system parameter | | - | -
Input | ports | - | NA | system parameter | Legacy parameter, may be disregarded



### GetVmDetails
```python
def GetVmDetails(self, context, requests, cancellation_context):
```

#### Description

This command retrieves information from the cloud provider on a specific instance in the sandbox. The
information includes data on the instance itself, the operating system, the spec, and networking information.
The command may be called from the orchestration setup after the instance is created, and every time the
user clicks the Refresh button in the VM Details side pane.

The information returned from this command is entirely up to the cloud provider implementation. Any data
returned will be displayed in the VM Details tab, unless specified otherwise in the results JSON.
The fields returned  can be the same for all deployment options in this cloud provider, or different for
each deployment option, as decides by the cloud provider implementation.

The implementation is expected to query the cloud provider for the details, and not returned any cached or stored
data.

This command should return a JSON with the VM details info. This JSON is also returned as part of the Deploy
command return object. The refresh VM details command will be called only if changes were made to the
instance or its connectivity after instance deployment.

if an error should be returned, raise an exception from this command. When called from setup, such an exception
will cause the sandbox to go into "Active with Error" state.


#### Relevance
Mandatory

#### Display Name
System command, it has no display name

#### Parameters

Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Input | cancellation_context | - | CancellationContext | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -




### remote_refresh_ip
```python
def remote_refresh_ip(self, context, ports, cancellation_context)
```

#### Description

Retrieve from the cloud provider an updated IP address
for an instance. The IP of the main network interface needs
to be retrieved from the cloud provider.
Both private and public IP need to be retrieved (when
relevant).

The command is called during orchestration setup after the instance is created
and connected to networks. It is also called when the user
manually triggers the refresh IP command in the sandbox.

The retrieved IP address needs to be set by calling API
methods, and not by returning the values from the command.
Please see details in the Quali Dev Guide.

#### Relevance
Mandatory

#### Display Name
Refresh IP

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceRemoteCommandContext | system parameter | | - | -
Input | cancellation_context | - | CancellationContext | system parameter | | - | -
Input | ports | - | NA | system parameter | Legacy parameter, may be disregarded



### ApplyConnectivityChanges
```python
def ApplyConnectivityChanges(self, context, request)
```

#### Description
This command is used to connect the instances in
the sandbox to the network elements, in an L2 connectivity
use case. It is called during the orchestration setup in order to connect the
elements includes in the blueprint, and is also called in a live sandbox when
and instance is connected or disconnected from a VLASN
service or from another instance (P2P connection).

The VLAN IDs are allocated by the Quali server,
according to the definition in the VLAN Service.
These IDs are sent to the command as parameters. The
implementation of this commands needs to be able to support
Access mode, Trunk mode, support VLAN and VXLAN ranges, if supported by
your cloud provider. Additionally, the implementation needs to support
a range of VLAN iDs.

The command receives an action in the parameter request for each
connection that needs to be created or disconnected.
In case of P2P connections, there will be 2 requests, one
one for each app.

Like other commands, this command needs to return an action
in the response per connection. In case of failure, indicate the
failure in the returned action or raise an exception. In case of an error, the
sandbox will go into "Active with Error" state when called from the setup.


#### Relevance
Mandatory for all cloud providers with Networking Type = L2

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -



### PrepareSandboxInfra
```python
def PrepareSandboxInfra(self, context, request, cancellation_context)
```

#### Description
This command is used to prepare all of the required infrastructure needs for
a sandbox operating with L3 connectivity. For example, creating networking infrastructure
like VPC, subnets or Routing tables in AWS, Storage entities such as S3 buckets, or
keyPair objects for authentication. In general, any other entities needed on the sandbox level can be created
here.

This command is called for L3 Networking type implementations in the beginning of the orchestration flow (preparation stage),
even before Deploy is called.

if anything fails in this command, and I would like to fail the sandbox creation as a result, an exception can be raised, or
an error can be set in the response object of the relevant action

#### Relevance
Mandatory for all cloud providers with Networking Type = L3

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Input | cancellation_context | - | CancellationContext | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -


### CleanupSandboxInfra
```python
def CleanupSandboxInfra(self, context, request)
```

#### Description
Use this command to clean any sandbox level entities created in the cloud provider, usualy entities created in the
PrepareSandboxInfra command. This is the last command called in the orchestration flow. Please note that the deployed
apps themselves are destroyed in the DeleteInstances command, and not here.

if anything fails in this command an exception can be raised, or an error can be set in the response object of the relevant action


#### Relevance
Mandatory for all cloud providers with Networking Type = L3

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Input | cancellation_context | - | CancellationContext | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -


### SetAppSecurityGroups
```python
def SetAppSecurityGroups(self, context, request)
```

#### Description
Use this command to programmatically set which ports will be open on each of the apps in the sandbox, and from
where they can be accessed. This is an optional command that may be implemented.

Normally, all outbound traffic from a deployed app should be allowed. For inbound traffic, we may use this command to
specify the allowed traffic.
An app may have several networking interfaces in the sandbox. For each such interface, this command allows to set
which ports may be opened, the protocol and the source CIDR

#### Relevance
Optional comamnd

#### Display Name
System command, it has no display name

#### Parameters
Input / Output | Parameter | Alias | Data Type | Required | Description
--- | --- | --- | --- | --- | ---
Input | context | - | ResourceCommandContext | system parameter | | - | -
Input | request | - | str (JSON str) | system parameter | | - | -
Output | | - | str (JSON str) | Yes |  | - | -
