# Save & Restore

#### Version 1.0.1

CloudShell allows users to save the state of a Sandbox and restore the sandbox to one of its previous states, freeing up expensive resources in between.

The sandbox supports 3 commands:
- Save Snapshot - saves the state of all the shells and stores the information in a local repository
- Restore Snapshot - restores the sandbox to a previous snapshot that was saved
- Get Snapshots - retrieves the list of snapshots

The document specifies the standard recommended way of saving and restoring sandboxes.



Version | Date | Notes
--- | --- | ---
1.0.1 | 2016-08-04 | Included support for apps and shell blueprint
1.0.0 | 2016-07-17 | First release of the Save & Restore Standard



# Saving a sandbox snapshot
Saving a snapshot is done by calling the 'Save Snapshot' orchestration command and providing an identifier for that snapshot.

The command creates a new snapshot record for the sandbox which includes all the details that enables CloudShell to go back to the same configuration when a restore is called in the future: metadata, sandbox connectivity details, resources configuration and rules and restrictions.

Each shell is responsible for saving its own state and restoring back to that state, the orchestration command is responsible for collecting all the different configurations, add the general information and store it in a predefined repository.

```python
def save_snapshot (snapshot_ID, override="false")
```

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | snapshot_ID | string | No | A unique identifier for the snapshot, if the ID is not specified use a combination of username + time (YY_MM_DD hh_mm_ss)
Input | override | bool | No | specify whether the snapshot should be overriden in case it already exists


#### Repository:
Any repository can be used to save the snapshot details.  The specifications below present a simple file server repository as an example. However, an ftp server or any other key-value repository can be used.

Note that the repository does not store the resource snapshots and backups.   Each resource saves its own data separately. The repository only stores the results that the resources returns.  The repository will feed the data back upon restore.

Hierarchy | Content
--- | ---
[blueprint name] + [sand box start date] + [owner] | Root folder for all the snapshots of a sandbox i.e: blueprint 2016-07-12 14:35:00 meni.b
/ snapshots | list of snapshots
/ snapshots / [snapshot ID] | the location of a specific snapshot, the snapshot ID will be the unique identifier of the snapshot
/ snapshots / [snapshot ID] / metadata.json | a configuration file that includes general information about that snapshot
/ snapshots / [snapshot ID] / connectivity.json | a configuration file that specifies the connectivity state of the environment
/ snapshots / [snapshot ID] / resources | The location of all the resources configuration files
/ snapshots / [snapshot ID] / resources | resource_name.json - a configuration file that represents the resource state
/ snapshots / [snapshot ID] / abstracts | The location of all the abstracts configuration files
/ snapshots / [snapshot ID] / abstracts / abstract_alias.json | a configuration file that represents the resource state (for abstract resources)
/ snapshots / [snapshot ID] / apps | app_name.json - a configuration file that represents the deployed app state



#### file server - example:
- /blueprint 2016-07-12 14:35:00 meni.b
  - /snapshots
     - /latest
        - metadata.json
        - connectivity.json
        - /resources
          - switch1.json
          - dut1.json
        - /abstracts
          - traffic_generator1.json
        - /apps
          - mysql1.json
     - /my snapshot #3
       - metadata.json
       - connectivity.json
       - /resources
         - switch1.json
         - dut1.json
       - /abstracts
         - traffic_generator1.json

The sandbox repository can be represented as a resource or service in the workspace with: Add, Update, Delete methods.


#### Command Description
**Creating a snapshot that can be restored from the sandbox orchestration:**

1. Check if the snapshot_ID is already in use, and according to the "override" parameter decide whether to continue and save the snapshot or abort.

2. Prepare the snapshot by creating the folder structure that represents the snapshot

3. Create the metadata.json file that holds general information about that snapshot

4. Create the connectivity.json file with the state of all the connections in the sandbox

5. Identify the shells in the sandbox and call the 'save' command for each one of the shells. for each shell, create a resource_name.json file.

6. Shells that were initiated from abstract resources, should be saved under abstracts folder with the abstract title as the file key



**Creating a blueprint that represents the snapshot:**

To enable users to **reserve the blueprint again** and restore the sandbox, a new blueprint that represents the sandbox snapshots should be added to the blueprint catalog.
1. To do this, using the Quali API and export the blueprint.
2. Using the Packaging API - modify the blueprint according to the following specifications:
   - Blueprint name: [blueprint name] + [sand box start date] + [owner]
   - Category: Sandbox Snapshots
   - Inputs: Snapshot ID - string
   - Shells:  Resources, Services & Apps that exist in the sandbox, for shells that were initiated from abstract resources, in case the shell supports restoring on any matching device, keep the abstract resources, for shells that don't support this capability, replace the abstract resource with the exact resource in the sandbox.
   - Connectivity: keep the existing connections and networking services



##### metadata.json
This file includes general information about the snapshot.

```json
{
    "metadata": {
      "ID":"[the snapshot identifier]",
      "Blueprint Name": "[the name of the blueprint]",
      "Sandbox ID": "[the ID of the sandbox]",
      "Sandbox Name": "[the name of the sandbox]",
      "Owner": "[the owner of the sandbox]",
      "DateTime": "[Snapshot date and time, format: YYYY-MM-DD hh:mm:ss]"
  }
}
```


##### connectivity.json
This file stores the connectivity state when the snapshot was saved.

```json
{
  "connectivity": {
    "connections": {
      "connection": {
        "type": "[the type of conncetion: route / connector]",
        "source": "[the name of the source resource]",
        "target": "[the name of the target resource]",
        "state": "[the state of the connection: connected / disconnected]",
        "network": "the name of the network (as defined in the networks node below)"
      }
    },
    "networks": {
      "network": {
        "type": "the type of network - service model: vlan auto, vlan manual",
        "attributes": "attributes of the networking service: allocation range, qnq"
      }
    }
  }
}
```




# Restoring the sandbox
The restore command searches for the snapshot in the snapshot repository, and restores the state of the sandbox.
The command can be called manually during the sandbox lifetime or automatically on setup in case a new sandbox is created from the blueprint that was saved during save_sandbox command.

```python
def restore_snapshot (snapshot_ID)
```

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Input | snapshot_ID | string | No | The unique identifier of the snapshot that needs to be restored


#### Command Description
1. Search for the snapshot_ID in the repository. If the named snapshot does not exist - return an error message.

2. Identify the shells in the sandbox and restore each one separately by:
   -  Read the saved .json file that represents the snapshot of the resource
   -  Based on the blueprint info - validate that the blueprint in the sandbox matches the blueprint in the snapshot - make changes if neededself. For apps, create / edit the app blueprint and deploy the app.
   - Call the restore command on the shell and pass the content of the .json as input so that the shell will be able to restore its state.


3.	Modify the connections according to the connectivity.json file that was saved. The sandbox setup should take care of the default connectivity, the command should compare the state with the snapshot and apply the modifications including disconnect routes, add new connections, change network specifications etc.




# Get available snapshots for a sandbox

```python
def get_snapshots ()
```

###### Parameters
Input / Output | Parameter | Data Type | Required | Description
--- | --- | --- | --- | ---
Output | result | string | No | json that represents the list of snapshots for the sandbox, each snapshot will be represented by the content of its metadata.json file.

```json
{
  "sandbox_snapshots":{
    "snapshot": {
      "ID":"[the snapshot identifier]",
      "Blueprint Name": "[the name of the blueprint]",
      "Sandbox ID": "[the ID of the sandbox]",
      "Sandbox Name": "[the name of the sandbox]",
      "Sandbox Description": "[the description of the sandbox]",
      "Owner": "[the owner of the sandbox]",
      "DateTime": "[Snapshot date and time, format: YYYY-MM-DD hh:mm:ss]"
    }
  }
}
```


#### Command Description
1. Search the sandbox snapshot repository

2. Return the list of available snapshots for the sandbox




# Shell Snapshots
Each shell must implement the save and restore commands and is responsible on saving and restoring its own state.

The standard specifies the interface and functionality that shells expose to the sandbox orchestration: **orchestration_save** & **orchestration_restore**. These two commands are hidden from the end user, their interface uses .json protocol and they should only be used by the sandbox orchestration via API.

 To enable users to save snapshots of a single shell via the user interface, additional save & restore commands may be developed with a user-friendly input parameters, these parameters may differ between shells,  hence they are not part of the standard.



## Saving the state of a shell

```python
def orchestration_save (mode="shallow", custom_params = None)
```
#### Command Input
The 'orchestration_save' command interface supports two modes:
 - Shallow (Default) - saves a snapshot that can later be restored
 - Deep - saves the backup of the resource that can later be restored, this option consumes more disk space as a full backup of the resource is expected to be made.

An example of the difference between these two modes is when saving a snapshot of a virtual machine (i.e in vCenter), a shallow copy will create a vCenter Snapshot whereas a deep copy will save an ovf image and store it on the disk.

Both parameters have default values so that the save can be called without providing any inputs.

Parameter | Data Type | Required | Description
--- | --- | --- | ---
mode | string | No | shallow / deep
custom_params | string | No | a json data structure with specific attributes that the shell may need, in most cases this inputs will stay empty. If some level of configuration is needed, it is recommended to use resource attributes so that the setting can be defined once.


```json
{
  "custom_params": {
    "vrf-management-name": "network-1"
  }
}
```

#### Command Output
The output of this function will be stored as the snapshot details, when trying to restore the state of the resource, the exact information will be provided as input to the restore function.

Parameter | Data Type | Required | Description
--- | --- | --- | ---
saved_artifact_info | string | No | composite data structure that represents the details of the snapshot

```json
{
  "saved_artifact_info": {
    "resource_name": "VM1",
    "resource_id" : "5F2EAA6C-E3FD-4DF0-8E2D-F05C81D61631",
    "created_date": "3577-04-27T00:17:48.819Z",
    "restore_rules": {
      "requires_sames_resource": false
    },    
    "saved_artifact" :{
      "artifact_type": "filesystem",
      "identifier": "//file_server/image.ova"
    }
    "blueprint" :{

    }
  }
}
```

##### Output - Restore Rules
This object represents rules such as whether the same resource must be used when restoring the state of the resources.
Some implementations may require the snapshot to be restored on the same device (preventing the use of abstract resources).
In the future, additional resources may be added to this object.

For example:
```json
{
  "restore_rules": {
    "requires_same_resource": true
  }
}
```

##### Output - Saved artifact
This object represents the snapshot details, it will be different according to the storing technology - e.g. ftp server, vCenter snapshot etc.

Example - a cloud-provider snapshot i.e: the details of an amazon AMI or a vCenter snapshot identifier
```json
{
  "saved_artifact" :{
    "artifact_type": "vm-snapshot",
    "identifier": "snapshot01"
  }
}
```

Example - a shared storage that stores the backup image
```json
{
  "saved_artifact" :{
    "artifact_type": "filesystem",
    "identifier": "//file_server/image.ova"
  }
}
```


Example - image file that is stored in a ftp server
```json
{
  "saved_artifact" :{
      "artifact_type": "ftp",
      "ftp_resource": "ftp_srv1",
      "identifier": "//folder1/image.ova"
  }
}
```

In this example *ftp_srv1* is a resource that represents the ftp server and has the connection details to the server, for example:
address: "192.168.1.45"
user: "user x"
pws: "123456"


Example - saving multiple configuration files
```json
{
  "saved_artifact" :{
    "artifact_type": "multiple-files",
    "identifier": "snapshot-123456",
    "filelist" : [ "file1", "file2" , "file3"]    
  }
}
```



##### Output - blueprint
This object includes information about the shell blueprint state in the sandbox.

**For physical resources** - this object represents the structure of the resource that was part of the reservation.
For example:
```json
{
	"blueprint": {
		"resource_name": "Server1",
		"sub_resources": [{
			"resource_name": "Port1"
		}, {
			"resource_name": "Port2"
		}]
	}
}
```

**For Apps** - this object represents the blueprint that is needed to restore the app, some details are omitted for brevity.
"deploymentService" - includes the deployment service details to deploy this app: selected vCenter, template name etc
"installationService" - includes the script information that needs to be used to deploy the app

For example:
```json
{
	"blueprint": {
		"templateName": "MySQL",
		"appResource": {
			"modelName": "Generic App Model",
			"driver": "Generic Driver"
		},
		"deploymentPaths": [{
			"name": "vCenter VM From Template + Generic Installation Option",
			"default": true,
			"deploymentService": {

			},
			"installationService": {

			}
		}],
	}
}
```

## Restoring a shell to its previous state
The orchestration_restore function is responsible of restoring a shell to its previous saved state.


#### Command Input
```python
def orchestration_restore (saved_artifact_info)
```
Parameter | Data Type | Required | Description
--- | --- | --- | ---
saved_artifact_info | string | No | composite data structure that represents the details of the snapshot, the value that will be passed as input must be the same as the exact value that the save function returned.
