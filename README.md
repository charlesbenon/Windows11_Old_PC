# 1/ Context

I have an old laptop from 2011 (Acer X52J) from where I was running Linux but lately I needed a Windows OS available for my online exams with PearsonVue (meaning no VM allowed).

This laptop is working perfectly but only with 4GB of RAM and 2 CPU cores (I just replaced the Hard drive by a SSD).

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

Navigate to **HKEY_LOCAL_MACHINE\SYSTEM\Setup**; create a registry key name LabConfig (I am almost sure the name does not matter).
Within this key (new directory created), create the 3 following DWORDs values (by setting up the Value Data to 1):
```
BypassTPMCheck
BypassSecureBootCheck
BypassRAMCheck
```
<kbd><img width="625" height="369" alt="image" src="https://github.com/user-attachments/assets/77de4190-c454-4fd3-b7f7-b0a58b200212" /></kbd>

# 4/ Bypass online Microsoft account

Later in the installation process, it will ask for a Microsoft acccount.

In case you don't have one or just don't want to use it, it can be bypassed by typing **ALT + F10** and the following command from the terminal:
```
start ms-cxh:localonly
```

This will open a new window for a local account to be created (Username, Password and 3 questions to recover the access).

# 5/ Optimize Windows 11

When the system is installed, update Windows latest packages as well as the drivers if you have specific versions for Windows 11 (those can be found from the hardware vendors websites).

<kbd><img width="466" height="296" alt="image" src="https://github.com/user-attachments/assets/10a19623-2a65-4447-bb07-8b3db8d42a6c" /></kbd>

For the drivers, you check if all the devices are recognized by the operating system by going to the Device Manager:
<kbd><img width="305" height="596" alt="image" src="https://github.com/user-attachments/assets/fa39d12d-3fdc-4a54-9279-5d7484b280ce" /></kbd>

As you can see, some of my device are still unknown (yellow exclamation mark showing in Other Device).

From there, apply the following changes which I found very good to reduce the CPU and memory usage:
* Adjust Visual Effects: Search for "Adjust the appearance and performance of Windows" and select "Adjust for best performance"

<kbd><img width="409" height="551" alt="image" src="https://github.com/user-attachments/assets/cd1959d8-22d2-4f14-8a18-0133593b1730" /></kbd>

* Manage Startup Apps: Press **Ctrl + Shift + Esc** to open Task Manager, go to the 4th tab (Startup apps) and disable unnecessary apps to speed up boot times (I have just left SecurityHealthSystray (showing security status, security itself is managed via system services)
<kbd><img width="877" height="430" alt="image" src="https://github.com/user-attachments/assets/80308cb9-7fd3-4fed-91d6-6e8d4fd3c135" /></kbd>

* Disable Visual Effects:  Search Visual Effects and disable "Transparency effects" and "Animations effects"
<kbd><img width="463" height="290" alt="image" src="https://github.com/user-attachments/assets/e284845e-62f6-48ad-a8f0-4edcaea25c4f" /></kbd>

* Remove Windgets: that needs to be done via PowerShell (search for Windows Powershell): winget uninstall "Windows Web Experience Pack"
<kbd><img width="1014" height="137" alt="powershell-delete" src="https://github.com/user-attachments/assets/4cb5c553-c8f9-407d-8af5-3eb7f4514281" /></kbd>

When it is done, check the task manager (**Ctrl + Shift + Esc**) for CPU, Memory and disk usage:
<kbd><img width="916" height="535" alt="image" src="https://github.com/user-attachments/assets/31d25df4-d5c4-45e3-a10f-d4d7c8802bb3" /></kbd>
