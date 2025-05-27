https://logi.wiki/index.php/Single_user_mode
## Create a new user in Single User Mode (This creates a new Administrator Account)

You can create a new administrator account by restarting the Setup Assistant:

1. Boot into Single User Mode: Start/restart your Mac. As soon as you hear the startup tone, press and hold ⌘ + S until you see a black screen with white lettering. (If you end up back on the login screen after a flash of the black screen with white lettering, enter your password and it will return to the black screen.)
2. Mount the drive by typing `/sbin/mount -uw /` then ↩ enter.
3. Remove the Apple Setup Done file by typing `rm /var/db/.AppleSetupDone` then ↩ enter.
4. Reboot by typing `reboot` then ↩ enter.
5. Complete the setup process, creating a new admin account.

With macOS Catalina, the APFS volume scheme is a little different. Change step 2 to `/sbin/mount -uw /System/Volumes/Data` . Continue to step 3.

## Creating a new user with macOS Catalina, Big Sur and Monterey using Terminal in recovery mode.

It appears that with Big Sur, you loose Admin privileges in single user mode. So in order to delete the Apple Setup Done file, we now have to boot into Recovery mode first and use Terminal to carry out our command. Very similar to the above method of removing the file .AppleSetupDone, we need to locate the db folder in the Macintosh HD Data partition. With macOS Big Sur and Monterey, the db folder has now been relocated in an additional "private" folder.

1. First, Boot into Recovery Mode with CMD+R
2. Access Disk Utility and mount the Data volume. Should be called Macintosh HD - Data
3. Close Disk Utility and open Terminal.
4. From terminal enter this the new command. `rm /Volumes/Macintosh\ HD\ -\ Data/private/var/db/.AppleSetupDone` then enter.
5. Reboot by typing `reboot` then enter
6. Complete the setup process, creating a new admin account.

More information on this method can be found here. [https://discussions.apple.com/docs/DOC-250002676](https://discussions.apple.com/docs/DOC-250002676)

## Delete test account in Single User Mode (This removes any test acct and creates a new Admin acct)

1. ⌘+S
2. `/sbin/mount -uw /`
3. `cd /var/db/dslocal/nodes/Default/users/`
4. `rm test.plist`
5. `rm -rf /Users/test`
6. `rm /var/db/.AppleSetupDone`
7. `reboot`

With macOS Catalina, the APFS volume scheme is a little different. Change step 2 to `/sbin/mount -uw /System/Volumes/Data` . Continue to step 3.