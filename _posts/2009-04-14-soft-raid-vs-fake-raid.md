---
layout: post
title: "[Quote] Soft-RAID is better than Fake-RAID"
author: 史蛋利九的部落格
tags:
- 科技先知
---
# What is fakeRAID?

In the last few years, a number of hardware products have come onto the market claiming to be IDE or SATA RAID controllers. These have shown up in a number of desktop/workstation motherboards. Virtually none of these are true hardware RAID controllers. Instead, they are simply multi-channel disk controllers combined with special BIOS configuration options and software drivers to assist the OS in performing RAID operations. This gives the appearance of a hardware RAID, because the RAID configuration is done using a BIOS setup screen, and the operating system can be booted from the RAID.  

To install Windows onto a RAID device, you must provide a driver (usually on a floppy disk) to the Windows installer in order to access the RAID array. Under Linux, which has built-in softRAID functionality that pre-dates these devices, the hardware is normally seen for what it is -- multiple hard drives and a multi-channel IDE/SATA controller. Hence, fakeRAID.  
![image](/img/in-post/1930207360_m.jpg)

# Why not use a linux software raid?

If you have arrived here after researching this topic on the Internet, you know that a common response to this question is, "I don't know if you can actually do that, but why bother -- Linux has built-in softRAID capability." Also, it's not clear that there is any performance gain using hardware fakeRAID under Linux instead of the built-in softRAID capability; the CPU still ends up doing the work. The most common reason for using fakeRAID is in a dual-boot environment, where both Linux and Windows must be able to read and write to the same RAID partitions. Multiboot configurations are common among cross-over users trying Linux out, for people forced to use Windows for work, and for other reasons. These people shouldn't have to add a separate hard drive just so they can boot Linux. FakeRAID allows these users to access partitions interchangeably from either Linux or Windows.   
[reference link](https://help.ubuntu.com/community/FakeRaidHowto)
