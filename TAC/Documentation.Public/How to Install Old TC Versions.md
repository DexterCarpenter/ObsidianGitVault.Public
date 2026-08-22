###### 2026-01-13
---
# How to Install Outdated TwinCAT Build Versions with Package Manager

Open Powershell as Administrator.
Run the following command to list what options you have to install.
If the feed you desire is not listed, you won't be able to install it.
```
tcpkg list TwinCAT.StandardRM.XAE -a
```

If you do not see the version you desire, you may need to add or change your feeds in Package Manager. Look up online how to add/edit feeds. **For previous/outdated versions you must have the Outdated Feed.** 

#### Beckhoff Outdated Feed
```
https://public.tcpkg.beckhoff-cloud.com/api/v1/feeds/outdated
```

Next, run the following command to install your desired version. For example to install **4024.53.9** run...

```
tcpkg install TwinCAT.StandardRM.XAE=4024.53.9
```
*Note the `=` before the version number*
