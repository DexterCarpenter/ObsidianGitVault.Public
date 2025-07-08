###### 2025-07-08
---
Install Excel

TwinCAT 4026 (v3.1.4026.16)
	doesn't have the `TwinCAT.XAE.EventloggerExcelAddIn` package...

You must obtain the package from the **testing feed**!!

### How to Workflow:

1) In Excel, TcEventLogger > Create New Sample or open existing .xlsx file
2) Make edits, etc.
	1) note: edits to the .xlsx do NOT automatically change the EventClass in TwinCAT
3) TcEventLogger > Generate TMC-File
4) If not already added to Project Solution Type System; Type System > Add Existing Item...
	1) Select TMC-File
5) If already added to Project Solution, TwinCAT will automatically detect change to TMC-File and prompt you via popup to update the EventClass

![[image001.png]]