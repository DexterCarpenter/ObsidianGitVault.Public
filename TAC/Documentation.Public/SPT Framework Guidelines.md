###### 2025-07-23
---
## The HMI Struct

`ST_Component_HMI` contains
```
ST_Component_Command
ST_Component_Config
ST_Component_Status
```

`Command` is read/write by higher-level objects
`Config`is read/write by higher-level objects
`Status` is read ONLY by higher-level objects

this is achieved by preserving the .Status of the HMI struct in the property set implementation

e.x.
```
PROPERTY Example_HMI : ST_Example_HMI

SET

VAR
	temp_Example_Status	: ST_Example_Status;
END_VAR

temp_Example_Status := _Example_HMI.Status;

_Example_HMI := Example_HMI;

_Example_HMI.Status := temp_Example_Status;
```