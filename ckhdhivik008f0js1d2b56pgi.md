## Adding Jetbrains Apps To Context Menu

I have been using [PHPStorm]. for a few years now. and over the years I found it very hard to open a project.  as I need to fire-up the [PHPStorm] App first then using the `File` menu I got to open the project. 

For it, I was not that easy as I keep switching from 1 project to another and I like to have 1 project per window. _so I did not use the multiple project feature_

And at the same time [PHPStorm] or any other app developed by [JetBrains] had no option to open a project via **Context Menu** (menu which displays when we press right-click)

So I search the internet and found a useful script that can add `PHPStorm` to the context menu in windows 

### BAT File
```bat
@echo off
SET PHPStormVersion="201.6668.153"
SET PhpStormPath="E:\development-tools\apps\PhpStorm\ch-0\\%PHPStormVersion%\\bin\PhpStorm64.exe"
 
echo Adding file entries
@reg add "HKEY_CLASSES_ROOT\*\shell\PhpStorm" /t REG_SZ /v "" /d "Open in PhpStorm - %PHPStormVersion%"   /f
@reg add "HKEY_CLASSES_ROOT\*\shell\PhpStorm" /t REG_EXPAND_SZ /v "Icon" /d "%PhpStormPath%,0" /f
@reg add "HKEY_CLASSES_ROOT\*\shell\PhpStorm\command" /t REG_SZ /v "" /d "%PhpStormPath% \"%%1\"" /f
 
echo Adding within a folder entries
@reg add "HKEY_CLASSES_ROOT\Directory\Background\shell\PhpStorm" /t REG_SZ /v "" /d "Open with PhpStorm - %PHPStormVersion%"   /f
@reg add "HKEY_CLASSES_ROOT\Directory\Background\shell\PhpStorm" /t REG_EXPAND_SZ /v "Icon" /d "%PhpStormPath%,0" /f
@reg add "HKEY_CLASSES_ROOT\Directory\Background\shell\PhpStorm\command" /t REG_SZ /v "" /d "%PhpStormPath% \"%%V\"" /f

echo Adding folder entries
@reg add "HKEY_CLASSES_ROOT\Directory\shell\PhpStorm" /t REG_SZ /v "" /d "Open with PhpStorm - %PHPStormVersion%"   /f
@reg add "HKEY_CLASSES_ROOT\Directory\shell\PhpStorm" /t REG_EXPAND_SZ /v "Icon" /d "%PhpStormPath%,0" /f
@reg add "HKEY_CLASSES_ROOT\Directory\shell\PhpStorm\command" /t REG_SZ /v "" /d "%PhpStormPath% \"%%1\"" /f
```

Great now I got an option to add it context menu right? 
## NO 

This script needs to be RAN again once we update the [PHPStorm] as **Jetbrains** Stores `exe` files inside of `version` folder something like this `PhpStorm\ch-0\201.6668.153\bin\phpstorm64.exe`

And still, I haven't figured a way to automatically find the new version. 

But what I found is there is no centralized place where we can find the same script for all the Jetbrains apps

So I decided to create a Github Repository where I generated script for each and every app.

> As of now I have added only for the Windows platform
> Planing to add support for Linux too.

%[https://github.com/varunsridharan/jetbrains-context-menu]

## How to use?

1. Make sure you download the script for the right platform (as of now we have only for windows) 
2. Locate the app folder inside `platform/app` . Example `windows/PhpStorm` 
3. Edit `enable.cmd` 
4. replace `E:\development-tools\apps` which is the install path where all your JetBrains app are stored.
5. replace `201.6668.153` which is the version number for that app.
6. Save it.
7. Right-click `enable.cmd` and click `Run As Administrator`
8. That's it. now it's configured. you can verify it by right-clicking anywhere 

### To Remove From Context Menu
1. Locate the app folder inside `platform/app` . Example `windows/PhpStorm` 
2. Right-click `disable.cmd` and click `Run As Administrator`

%[https://github.com/varunsridharan/jetbrains-context-menu]

[PHPStorm]: https://www.jetbrains.com/phpstorm/
[JetBrains]: https://jetbrains.com/

---

Questions or feedback?  Please comment below. 

See all my projects at <a href=https://github.com/varunsridharan/>Github</a>.

Follow me on <a href="https://twitter.com/varunsridharan2">Twitter for updates</a>