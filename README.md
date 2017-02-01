# Cloushell Standards

This repository contain the following:

## Documentation

This folder contain the official documentation for all defined shell standards.
This is applicable for all CloudShell versions (unless stated specificlly in the standard).

## TOSCA Specisifcation

This folder contains TOSCA definition files of CloudShell standards, per standard version.
Applicable for CloudShell 8.0 and above


[TOSCA Simple Profile in YAML Version 1.0](http://docs.oasis-open.org/tosca/TOSCA-Simple-Profile-YAML/v1.0/csprd02/TOSCA-Simple-Profile-YAML-v1.0-csprd02.html)

### Install TOSCA Parser

```bash
$ pip install  tosca-parser
```

### Validate file 
```bash
$ tosca-parser --template-file=toscaparser/tests/data/tosca_helloworld.yaml
```



