If you are interested, read the **WHOLE** guide.

Special thanks to the Italian (I'm Italian) - Polyglot (/MultiLingual) Telegram group that helped me in this project, [@HackintoshLife_it](https://t.me/HackintoshLife_it) and TomZanna.

I have used **Clover Bootloader r5121** because I think it's the
best option right now for my pc, I know it's not the latest version, but I don't update to Big Sur so I can also stop here.
I know OpenCore would make everything more like a **real Mac**, but it sucks for my computer, perhaps because it is neutered by the manufacturer HP or because it is pre-assembled. Just to clarify, I've tried OpenCore and it boots, but I don't need to migrate to that Bootloader, It's really unstable, tedious, pisses off the whole computer (BIOS and etc) Clover is really well done for this PC.
#Specs:
Thats a pre-assembled computer, here: **[HP 550-132nl](https://support.hp.com/us-en/document/c05244082/?openCLC=true)** (from
the original specs I only changed the Storage and the WiFi-
Bluetooth card) . I'll write that down:

**Component** | **Description**
:--|:-- 
**PC MODEL** | HP 550 - 132 nl
**CPU**  | Intel Core i7 6700 3.40GHz - Skylake - 4 Cores - 8 Threads (R0)
**RAM** | 12GB Dual-Channel DDR3 (1x 4GB and 1 x 8GB) 1600 MHz
**MOBO** | HP 2B47 (U3E1) 1.04
**iGPU** | Intel HD Graphics 530 (HP)
**dGPU** | 4095MB NVIDIA GeForce GT 730 GDDR3 (MSI)
**AUDIO** | Realtek High Definition Audio ALC3863-CG
**NETWORK CARD** | LAN Realtek RTL8161 (Realtek PCIe GbE Family Controller)
**STORAGE** | Samsung SSD Sata 500GB
**BIOS VERSION / DATE** | AMI A0.20 - 01/18/2018 (lastest)

#What is not Working:
- ###### **Apple TV + / Streaming on Safari**:
hard to resolve, it's a DRM Compatibility Problem, thats because of the dGPU GT 730. Infacts my Hackintosh is NV + IGPU, IM / MM and therefore you can only see the trailers and download some epidodes, not streaming. For resolving this problem i should buy a AMD dGPU (AMD+IGPU, IM/MM), like the AMD RX 580 for example, that (GPU would be perfect for my Hackintosh. [More INFO HERE](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.Chart.md)

- ###### **Deleting things from NVRAM (Clover)**: 
In Clover I can emulate the NVRAM, and it works. But deleting objects from it is not allowed for me. I really don't know how can i solve it, when i type `sudo nvram -c`. It gives me an error which I will show later. Even if i type the command in the `sudo su` shell, even without the sudo... I have tried even pressing F11 on Clover GUI and this freezed Clover. Tried also the Single User boot arg and the Clover Shell, but nothing worked. The error we're talking about:
>`nvram: Error clearing firmware variables
(iokit/common) not permitted`

- ###### **OpenCore NVRAM**:
I Tried OpenCore 0.6, boots up but unfortunately there is no way to make the NVRAM go, not even by emulating it. I just don't know why. But taking away this problem, with OpenCore everything else works, just like Clover, so for my case there is no reason to migrate to OpenCore now, it's also more difficult for me, in my opinion Clover is the easiest bootloader for Hackintoshing.

- ###### **Big Sur**:
Big Sur it cannot be installed on this PC, I have tried hundreds of attempts with different settings and versions of both bootloaders .. arrives at the Recovery menu, I install Big Sur but it doesn't get to the language selection, it keeps giving kernel panic and rebooting. (But the Big Sur files are there in the partition)

#My Difficulties:
- ###### **Dual Monitor**:
In fact during my hack, i discovered that my iGPU it didn't work properly, in fact the HD 530 didn't have audio and video output. To solve this problem I had to create a connector patch. Now the iGPU is working properly, this can be useful with the advent of macOS Big Sur, if the GT 730 was not supported.

- ###### **NVRAM**:
It was difficult to get it to go with Clover (i got it using the RC Scripts), natively non-existent but by emulating it I managed to make it work, very unstable and due to the *preassembled PC motherboard* it has many *limitations*.. I can't clean it, once created it is difficult to refresh it and often gives many problems, This motherboard also gave problems with the iGPU because it *preallocated too little video memory* to the processor... From the BIOS it is impossible to set it in any other way. The NVRAM it could be resetted by removing the *CMOS* battery on the motherboard.

- ###### **WiFi**:
Not compatible. So i just bought a WiFi+Bluetooth m2 card (So instead of keeping useless hardware, I take out the incompatible and replace it with the compatible one) for 30$ from AliExpress, [LINK to WiFi+BT Hackintosh Compatible HERE](https://it.aliexpress.com/item/32918457901.html) with AirDrop and Handoff. Since the WiFi card pre-installed on my PC only had one antenna and two WiFi Antenna Connection Ports, I took an extra couple of antennas, so the signal will be enhanced and will work better on my hackintosh. [Here's the link](https://www.amazon.it/dp/B08JTDK334).

- ###### **FaceTime and iMessage**:
Even with a valid serial number Apple had blacklisted my account, I solved it by calling the Apple Customer Support ([I found their phone number on this link](https://support.apple.com/en-us/HT201232)) making me activate my account. [MORE INFO HERE](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#customer-code-error)
- ###### **USB 3.0 used as USB 2.0**:
I had to create a Custom Kext with Hackintool, including the M2 slot on the mobo, for the WiFi Card. [Hackintool link here](https://github.com/headkaze/Hackintool/releases/)
#####I WANT TO PAY PARTICULAR ATTENTION TO THE SSDT CUSTOM THAT I CREATED, IT WAS VERY COMPLICATED BUT IN THE END I MADE IT SO MUCH TO MAKE MY HACKINTOSH THE MOST SIMILAR TO THE ORIGINAL IMAC 17.1, I'LL GIVE MY lOREG AND THE IOREG TO THE ORIGINAL IMAC 17.1, with obviously the modified application capable of reading Apple original Mac ioreg.

After all, everything work just fine, even Apple Services and
HW Acceleration, File Vault 2 is fully working (although it
slows down the boot time considerably even on sata ssd),
USB 3.0, NVRAM (working but needs to be emulated),
BootCamp and the Internal Card Reader, also Sleep (Sleep needs an adjustment via Hackintool, Power section and "Screwdriver" button at the bottom).
The thing I can't understand is why with Chrome I have 2.5mb / s in download
but with Safari I have 1.1mb / s in download. The important
thing that it works, even if with Chrome. (I have a network
that goes at maximum 2.6mb / s in download and with
Chrome I have the maximum speed so, NICE), Performance it has been tested with Benchmarks, holds up well .. nothing to say.

#*MY EFI AND BIOS SETTINGS*:
[GitHub Link HERE](https://github.com/Francesco146/hp-505-132nl-Hackintosh)
(Ethernet Kext is not up to date because the 2.3.0 it gives me
problems, ethernet no longer works when used. Just used
the 2.2.2 and that worked flawlessly).
Update the config.plist with your serial number.


This guide is written by me, Francesco M.

It's the only guide for my PC, I hope it will be useful to those who have my own Preassembled PC, 
I would have wanted a guide like this when I started, I'm sorry but this is for macOS Catalina 10.15.7, no Big Sur Support.


#*Conclusion:*
This is not a good PC, neither for performance nor for compatibility, but we managed to come up with a decent and 99% compatible Hackintosh, I don't recommend buying this PC to follow this guide, but if you have my own PC then here is the guide ready for you. Perfect PC for understand completely how an Hackintosh works and learn how to troubleshoot the whole process, perfect also for coding, web surfing, Plex Web Server.
If you also have this PC and find improvements to my EFI, making you go things that I have not been able to get working (like Big Sur) please contact me in any way you want, like a fork on GitHub or private messages on Reddit. 