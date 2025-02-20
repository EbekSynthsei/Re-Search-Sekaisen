---
cssclasses: 
tags:
  - bash
  - fabric
  - done
date: 2025-02-20T11:45:00
---
Keep this all on one line:

```
function yt { [CmdletBinding()] param( [Parameter(Mandatory = $true)] [string]$videoLink ) fabric -y $videoLink --transcript }
```

per un singolo uso nella stessa command line:

`doskey yt=fabric -y $* --transcript`

To make this alias persistent across Command Prompt sessions, you can follow these steps:

1. Create a text file (e.g., "aliases.txt") and add the DOSKEY command to it:

`yt=fabric -y $* --transcript`

1. Save this file in a location you'll remember, such as "C:\Users\YourUsername\aliases.txt".
 
2. Open the Registry Editor (regedit) and navigate to:  
  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor
  
3. Create a new String Value named "AutoRun".
  
4. Set its value to:
`DOSKEY /MACROFILE="C:\Users\YourUsername\aliases.txt"` 

After completing these steps and restarting your Command Prompt, you'll be able to use the "yt" alias followed by your video link argument. For example:

`yt https://www.youtube.com/watch?v=dQw4w9WgXcQ`

This will execute the command:

`fabric -y https://www.youtube.com/watch?v=dQw4w9WgXcQ --transcript`

Remember that the $videoLink argument is mandatory in this setup. If you run the alias without an argument, it will pass an empty string to the fabric command, which may result in an error depending on how the fabric command handles missing arguments

---
# References

[Permanent Aliases in Windows](https://dev.to/xkeshav/how-to-set-permanent-aliases-in-windows-4214)
[Powershell Aliases](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/set-alias?view=powershell-7.5)
[Github aliases](https://gist.github.com/vladikoff/38307908088d58af206b)
