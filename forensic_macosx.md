# Forensic on MACOSX
plist format is widely used in MACOSX to store informations.
*This is not an exhaustive resource.*

## Persistence : 

* Launch Agents Items: : `/Library/LaunchAgents` matching users processes. `/Library/LaunchDaemons` matching system processes.
* Crontab : `/usr/lib/cront/tabs/` and task : `/private/var/at/jobs`
* Logins/logout hook : `/private/var/root/Library/Preferences/com.apple.loginwindow/plist`
* Autorun after user authentification via GUI : `~/Library/Preferences/com.apple.loginitems.plist` et dans `<application>.app/Contents/Library/LoginItems` `SessionItems/CustomListItems.Name`
* Install History : `~/Library/Receipts/InstallHistory.plist`
* Files ruleset : `/etc/emond.d/rules` and client DB one : `/private/var/db/emondClients` (**T1546/014**)

## Other interesting elements.

* Some volume could be mount in `~/Library/Preferences/com.apple.finder.plist`, there exists a key : **FXDesktopVolumePositions** which match to a mounted **.dmg**.
* Admin System DB : `private/var/db/dslocal/Nodes/Default/groups/admin.plist`
* Users System DB : `private/var/db/dslocal/Nodes/Default/users`
* SQLite3 DB : `Library/Accounts/Accounts3.sqlite`
* Recent items : `Library/Preferences/com.apple.recentitems.plist`
* chrome/safari history are basically sqlite3 DB : `/users/Library/Application Support/Google/Chrome/Default/History`. We could check the downloads with some specific file extensions : `.dmg` , `.pkg` 
* overwriting of Plists : `/var/db/launchd.db`

## MACOS X Malware (Quarantine, Xprotect)

* Malware with extensions : `.dmg, .pkg, et scpt` (Apple Script)
* Identify some hashes in `/var/root/` that could be malicious
* The equivalent of UAC prompt in Windows to authorize to open downloaded files from  `Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2` (OS X >= 10.7 : V2)
* hash research based on the file under quarantine  : `/System.Library/CoreServices/CoreTypes.bundle/Contents/Ressources/XProtect.plist`

## Summary 
```
~/Library/Preferences/com.apple.finder.plist
~/Library/Preferences/com.apple.recenitems.plist
~/Library/Preferences/com.apple.loginitems.plist
~/Library/Logs/Diskutility/log
~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV2
```
```
/private/var/at/jobs/
/var/db/launchd.db
/usr/lib/cront/tabs
```