###### 2025-12-07
---
### Create r2modman profile
Create a new profile using the following code:
`019afa28-ddd7-b44f-ad95-f11b64cc2d08`

### Copy these files into Risk of Rain 2 root
copy
```
%appdata%\r2modmanPlus-local\RiskOfRain2\profiles\<your profile name>
│   .doorstop_version
│   doorstop_config.ini
│   mods.yml (optional)
│   winhttp.dll
│
└───BepInEx
    ├───core
    ├───config
    ├───plugins
    ├───patchers
    └───...
```
*do NOT copy _state

paste
```
...\steamapps\common\Risk of Rain 2\
│   Risk of Rain 2.exe
│   .doorstop_version
│   doorstop_config.ini
│   mods.yml (optional)
│   winhttp.dll
│
└───BepInEx
    ├───core
    ├───config
    ├───plugins
    ├───patchers
    └───...
```

all configs should be copied over as well.

All done!