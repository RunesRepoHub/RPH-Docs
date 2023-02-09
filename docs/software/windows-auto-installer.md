# Windows Auto Installer 

![pic](../img/windows.jpg)

[Download](https://github.com/rune004/Windows-Auto-Installer/archive/refs/tags/Alpha-1.2-USB.zip){ .md-button }
[Github](https://github.com/rune004/Windows-Auto-Installer/releases/tag/Alpha-1.2-USB){ .md-button }

??? info "Use-case"
  
    This batch script has been made to make it easy to keep track of, and installing software on a freshly re-installed Windows pc.

    This is done by using the Exe folder to contain all setup.exe and the WAI.bat to run the installation of these setup.exe 

    This will not automated the individual setup.exe 

    It will automated the "running" of the next setup.exe when you have finshed a installation. This can be helpfully if you have to do helpdesk tasks while installing software.   



??? example "How to use it?"

    ## How to use it?

    * Download the latest release for USB.

    * Move the downloaded zip file to a USB.
    
    * Copy the zip file to "target" machine.

    -> You have to manuelly download WordMat and put it into the Exe folder and rename it to "WordMat.exe"

    -> You have to manuelly download Papercut and put it into the Exe folder and rename it to "Papercut.exe"

    -> You have to manuelly download AppWriter and put it into the Exe folder and rename it to "AppWriter.exe"

    * Unzip on the desktop (The only way it will work for now)
    * Open the folder on the desktop 
    * Run the WAI.bat

    ## Easy way to use it

    * "Pre-download" Wordmat, Papercut and AppWriter

    * Unzip the folder

    * Move Wordmat, Papercut and AppWriter into the Exe folder

    * Zip the folder back up (I recommend zipping it again to avoid running it on the USB drive. This will not work)

    * Move the zip folder to the USB ready for use
 

??? "How to modify it for my use?"

    ## Modify

    This is a "cell" or in other words this is the "variables" for one pices of software.

    ````
    call "c:\Users\%Username%\Desktop\Windows-Auto-Installer-Master-USB\OfficeSetup.exe"
    ECHO.
    echo Please Wait...
    timeout /t 3 /nobreak > nul
    ECHO.
    pause
    ````

    All you need to change is the `call "c:\Users\%Username%\Desktop\Windows-Auto-Installer-Master-USB\Exe\your-software.exe"`

    You should just put your new exe file into the "Exe" folder and change the Exe file name in the end of the string.
