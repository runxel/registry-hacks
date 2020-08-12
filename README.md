# Registry Hacks ®
Windows let's us tune many parts via the allmighty Registry. Take care!  
**Many of these "hacks" need to be applied after every update.**

## How to edit the Registry?

Press <kbd>Windows Key</kbd> + <kbd>R</kbd> to open the <samp>Run</samp> command and type in `regedit`. Hit Ok and the registry editor opens.

You can also use files with the `.reg` extension. Just double click and the changes will be automatically applied. Can be openend and written by any text editor, so you can see what's actually going one.

---

### Change default drag and drop action
- Change the `DefaultDropEffect`DWORD inside
    - `HKEY_CLASSES_ROOT\*` _AND_
    - `HKEY_CLASSES_ROOT\AllFilesystemObjects` to
- `0` → default action
- `1` → always copy
- `2` → always move
- `4` → always create shortcut

Since I need to do this regularly I've created a [`.reg` file](regedits/set_drag_and_drop_to_move.reg) to use.  
<sup>[[source](https://www.tenforums.com/tutorials/38097-change-drag-drop-default-action-windows.html)]</sup>


### Allow double-clicking PowerShell scripts
🛑 Beware! This is potential unwanted behavior and might be a security risk!

- Navigate to `Computer\HKEY_CLASSES_ROOT\Microsoft.PowerShellScript.1\Shell\Open\Command`
- Change default value to `"C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -noLogo -ExecutionPolicy unrestricted -file "%1"`

<sup>[[source](https://stackoverflow.com/questions/10137146/is-there-a-way-to-make-a-powershell-script-work-by-double-clicking-a-ps1-file#20623597)]</sup>


### Change network type
- Navigate to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles`
- That key has a lot sup keys, all in the form of a GUID (like "`{06B3F4E7-FD43-4DAE-B1F9-D3BD22F6D745}`"); look for the right one based on `ProfileName`
- Change the `Category` DWORD to 
    - `0` for Public Network
    - `1` for Private Network
    - `2` for Workplace Network

<sup>[[source](https://www.schieb.de/728318/windows-8-1-netzwerktyp-nachtraeglich-aendern)]</sup>


## 💄 Cosmetic
### Icon spacing on desktop
- Navigate to `Computer\HKEY_CURRENT_USER\Control Panel\Desktop\WindowMetrics`
- Horizontal spacing with `IconSpacing`
- Vertical spacing with `IconVerticalSpacing`
- Values possible between `-480` and `-2730`
- Only visible after an Explorer restart!

<sup>[[source](https://www.deskmodder.de/wiki/index.php?title=Abstand_zwischen_den_Desktop_Icons_verkleinern_Windows_10)]</sup>


### Get rid of OneDrive in Explorer
- Navigate to `HKEY_CLASSES_ROOT\CLSID\{018D5C66-4533-4307-9B53-224DE2ED1FE6}`  
- Change Value of `System.IsPinnedToNameSpaceTree` to `0`

<sup>[[source](https://www.windowscentral.com/how-remove-onedrive-file-explorer-windows-10)]</sup>


### Delete "Bridge" from context menu
To get rid of "Browse in Adobe Bridge"
- Delete the `HKEY_CLASSES_ROOT\Directory\shell\Bridge` key

<sup>[[source](http://blog.ryantadams.com/2010/11/07/remove-browse-in-adobe-bridge-from-context-menu/)]</sup>


### Remove the 3D Objects folder from This PC
- Delete the `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{0DB7E03F-FC29-4DC6-9020-FF41B59E513A}`
- And delete the `HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace\{0DB7E03F-FC29-4DC6-9020-FF41B59E513A}` as well

<sup>[[source](https://www.deskmodder.de/wiki/index.php?title=Abstand_zwischen_den_Desktop_Icons_verkleinern_Windows_10)]</sup>


--- 

## Disclaimer
The author assumes no responsibility or liability for any errors or omissions in the content of this site. The information contained here is provided on an "as is" basis with no guarantees of completeness, accuracy, usefulness or timeliness. Use at your own Risk!
