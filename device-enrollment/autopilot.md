## Windows Autopilot for join devices.

Documentation: https://learn.microsoft.com/en-us/autopilot/add-devices#collect-the-hardware-hash

== Prerequisites.

- Windows machine.
- Admin account credentials.

1. Get device hash .csv file.

The first thing to do is to get the device hash by running PowerShell as administrator in the device to be enrolled using .

- Login in to the new windows machine using local admin credentials.
- Run PowerShell as administrator, to install the required module run:

```PowerShell
Install-Script -Name Get-WindowsAutoPilotInfo

-To get and save hash info run:

```PowerShell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
New-Item -Type Directory -Path "C:\HWID"
Set-Location -Path "C:\HWID"
$env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
Install-Script -Name Get-WindowsAutopilotInfo
Get-WindowsAutopilotInfo -OutputFile AutopilotHWID.csv

Steps above will create and save a .csv file containing the device's hash info.
Get-WindowsAutopilotInfo.ps1 script saves the hardware hash locally on the device as a CSV file. This method is normally used on devices that already underwent Windows Setup and OOBE.





