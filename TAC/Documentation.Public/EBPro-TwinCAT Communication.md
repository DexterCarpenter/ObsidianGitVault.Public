###### 2025-08-11
---
# Summary
How to get communication between a Beckhoff PLC and a Weintek (MapleSystems) HMI using TwinCAT and EBPro. Add routes to the HMI and the PLC and import tags. 

Watch [this video](https://youtu.be/C4PKcVwFTMM?si=KQvwzjt3rA7yfhxp) on how to set up the connection. For my specific mewthod that worked, read below.

# Workloads
- TwinCAT 3.1
- EBPro 6.10
# Configure the HMI
### 1) System Setting File
The easiest way to consistantly configure the HMI is to use a System Setting File. System Setting Files can be loaded/saved in

> EBPro > Tool > System Setting Editor.

This should open the EasySystemSetting window. Here you can specify the network configuration under `Network LAN 1` as well as several other settings. These settings are also editable through the HMI itself.

Statically set the IP Address, Subnet Mask, and Default Gateway. I routed my HMI connection through my local home network so my configuration looked like:

> IP Address: `192.168.1.123`
> Subnet Mask: `255.255.255.0`
> Gateway: `192.168.1.1`

Save the file somewhere you can find it later, we will come back to this.
### 2) Adding Beckhoff Device Route to HMI
In EBPro, navigate to

> Home > System Parameters

Add the Beckhoff PLC by clicking `New Device/Server...`

Name: `Beckhoff TwinCAT PLC`
Make sure it is a `Device` not an `HMI`
Location: `Local`
Device type should be `Beckhoff TwinCAT PLC (Ethernet) - Free Tag Names`
I/F: `Ethernet`

![[Pasted image 20250811151356.png]]

For the IP, click `Settings`...

For this, you will need your Beckhoff PLC's IPv4 address and AMS NetId. Enter both of them.

IPv4 Port: `48898`
ADS Port: `851` *(not `801`)*

![[Pasted image 20250811153357.png]]

### 3) Adding HMI Route to TwinCAT
Open TwinCAT and set your target system to your PLC. In the solution tree, go to SYSTEM > Routes.

In Current Routes, add a route. Manually define the route as follows:

Route Name (Target): *can be whatever you want*
AmsNetId: *add `.1.1` to the HMI's IP Address, e.x. `192.168.1.123.1.1`*
Address Info: *IP Address of HMI*

Set is as a `Static` route.

Note: You may get some error popups when you do this, it doesn't appear to be a problem for me.

Be sure to Activate the configuration to the PLC.

![[Pasted image 20250811154917.png]]
### 4) Create Variables to be Shared
I found that using a GVL for inputs and outputs to the HMI works the best. I like to create two GVLs, one input and one output. The name of the GVL will appear in EBPro which is useful for finding which variable you want to link.

Once the GVL(s) are created, save the project and return to EBPro.
### 5) Import Tags into EBPro
Return to the System Parameters Window where you added the Beckhoff TwinCAT device. Click on the device you added. There should be an option to `Import Tags...`

It doesn't seem to matter what WORD format you use.

Choose to import Linear Files (`*.TPY;*.EXP;*.TcDUT;*.TcPOU;*.TcGVL`), click OK

Browse for your GVL (or other) files. Then `Import`.

There's a nice check here that confirms how many individual variables were imported successfully.
### 6) Download HMI Project
If you haven't already, link a variable from the Beckhoff Device to a bit lamp or something so you can verify the connection.

Download the project to the HMI by navigating to Project > Download (PC->HMI)

Be sure to check `Use system settings file` and browse to where you saved your System Settings File.

After you download, you should get no popups on the HMI saying `Device No Response`, additionally whatever elements you linked to the PLC should be showing the live values on the PLC. You can go online with TwinCAT and manually change values to see changes.

