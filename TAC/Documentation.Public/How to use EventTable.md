###### 2025-07-21
---

[Event Table](https://infosys.beckhoff.com/content/1033/tc3_plc_intro/3524166155.html?id=4373836669159094324)
	[Configuration of the event table](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/3524180363.html&id=)
	[FB_ReadTc3Events](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/11028199435.html&id=) (for 4026)
	[FB_AdsReadEvents](https://infosys.beckhoff.com/content/1033/tcplclib_tc2_utilities/3524194955.html?id=3350434744136909984) (for 4024)
## Libraries
`VisuElemEventTable` (1.0.4.2)
`Tc2_Utilities` (3.9.2.0)
Adding a Visualization adds all `System_Visu...` libraries needed

## Preparation
Navigate to...
PLC Project > Right Click > Properties > ...
- Visualization Profile > Compatible Visualization Extensions
	- ✅ VisuElemEventTable is checked ACTIVE
- Visualization > Advanced > 
	- ✅ Visible
		- ❌ Activate property handling in all element properties
		- ✅ Activate implicit checks for visualization POUs 
- Compile > Settings > Compiler defines:
	- This should be *empty*

A target or web visualization is **REQUIRED** for the Event Table to function
Navigate to...
	Visualization Manager > Right Click > Add > ...

Connect the Event Table 'Event data array' property to
`fbReadTc3Events.aEvents` (not `.aEvents[]`)

Be sure to call this cyclically

```
fbReadTc3Events (
    bReadEvents          := bReadEvents, 
    nLanguageID          := 1033, // English
    eDateAndTimeFormat   := E_DateAndTimeFormat.de_DE,
    bClearTable          := bClear,);
```
`bReadEvents` must be `TRUE`

