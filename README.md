# 1/ Context

I have an old laptop from 2011 (Acer X52J) from where I was running Linux but lately I needed a Windows OS available for my online exams with PearsonVue (meaning no VM allowed).

This laptop is working perfectly but only with 4GB of RAM and 2 CPU cores (I just replaced the Hard drive by a SSD)

This hardware configuration shouldn't be a limitation (
[**Windows 11 minimum hardware**](https://www.microsoft.com/en-us/windows/windows-11-specifications)) with Windows 11 but I have tried without applying any work around and it would just show a prompt after the first installation reboot.

It was probably related to missing the Trusted Platform Module (TPM) and UEFI secure boot capable features which my old laptop does not have.

# 2/ Windows 11 Installation support

Create the USB installation support from Microsoft ISO.

From a running Windows, [**Rufus**](https://rufus.ie/en/) can be used, it is very intuitive.

Windows 11 ISO file can be downloaded directly from [**Microsoft website**](https://www.microsoft.com/en-us/software-download/windows11).

From Linux, I have used [**Ventoy**](https://www.ventoy.net/en/index.html).

# 3/ Bypass hardware requirements (TPM, SecureBoot, RAM)

When the USB key is created, boot the new computer with by selecting USB a boot device (F2 > Boot or F11 should both work except for some motherboard manufacturers when the computer is booting).

Windows installation will start and at the beginning, type **ALT + F10**, which will open a terminal.

From there, open the registry editor with:
```
regedit
```

Navigate to **HKEY_LOCAL_MACHINE\SYSTEM\Setup** and create the following DWORDs values (by setting up the Value Data to 1):
```
BypassTPMCheck
BypassSecureBootCheck
BypassRAMCheck
```

# 4/ Bypass online Microsoft account

Later in the installation process, it will ask for a Microsoft acccount.

In case you don't have one or just don't want to use it, it can be bypassed by typing **ALT + F10** and the following command from the terminal:
```
start ms-cxh:localonly
```

This will open a new window for a local account to be created (Username, Password and 3 questions to recover the access).

# 5/ Optimize Windows 11

When the system is installed, update Windows latest packages as well as the drivers if you have specific versions for Windows 11 (those can be found from the hardware vendors websites).

From there, apply the following changes which I found very good to reduce the CPU and memory usage:
-Adjust Visual Effects: Search for "Adjust the appearance and performance of Windows" and select "Adjust for best performance"

-Manage Startup Apps: Press **Ctrl + Shift + Esc** to open Task Manager, go to the 4th tab (Startup apps) and disable unnecessary apps to speed up boot times.
I have just left SecurityHealthSystray (showing security status, security itself is managed via system services)

-Disable Visual Effects:  Search Visual Effects and disable "Transparency effects" and "Animations effects"

-Remove Windgets: that needs to be done via PowerShell (search for Windows Powershell): winget uninstall "Windows Web Experience Pack"

When it is done, check the task manager (**Ctrl + Shift + Esc**) for CPU, Memory and disk usage:
