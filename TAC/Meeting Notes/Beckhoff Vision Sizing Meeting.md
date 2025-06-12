###### 2025-06-12
---
10fps (40fps total 4x cameras) @ 720p
there isn't really an 'equation' that can determine what processing requirements you will have
cameras must be free streaming since they've got to count boards that pass
beckhoff cameras are not 720p, but we can narrow down the frame if needed
there are no photoeyes as backup, they are not required.
Customer wants precise timestamping
Are cameras accessible to any computer? **Yes**- they aren't bound to a Beckhoff PLC. They're Gigy
C++ development is also possible, you have to use TwinCAT libraries though. But function calls are pretty much 1-to-1 to OpenCV
Array of regions, grab brightness of each region, if above threshold, then that boolean is TRUE.
Is there a large performance hit using C++ vs. Structured Text? It's not significant enough to impact a decision one way or the other. Pro to using ST is it occurs in real-time and is available with ADS, etc.
For simulation, you can drop in a bitmap/png and can imitate a simmed camera 
monochrome camera
lighting is currently ambient light
Thoughts about using an IR light and filter the cameras to only see IR so that when they turn on/off lights in the factory it doesn't affect vision
Controlling Gigy vision camera states??
	Todd will kick sample program to Brent, TC program that shows camera states and such

### Chat Log:
[https://www.beckhoff.com/en-us/products/ipc/embedded-pcs/cx5600-amd-ryzen/cx2500-0062.html](https://www.beckhoff.com/en-us/products/ipc/embedded-pcs/cx5600-amd-ryzen/cx2500-0062.html "https://www.beckhoff.com/en-us/products/ipc/embedded-pcs/cx5600-amd-ryzen/cx2500-0062.html")
They are IPC form factor, but the **C6025-0010** and **C6030-0080** also come with 2.5G native.
https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/14666927499.html?id=5590670370547318243
https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/6789193099.html?id=2229161530588360474
https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/4360672267.html?id=2729457735100044965
There is file source, but there is also a stream recording and playback option: [https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/6112688907.html](https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/6112688907.html "https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/6112688907.html")
[https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/4333986955.html?id=6166133478361286762](https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/4333986955.html?id=6166133478361286762 "https://infosys.beckhoff.com/content/1033/tf7xxx_tc3_vision/4333986955.html?id=6166133478361286762")

### Debrief
