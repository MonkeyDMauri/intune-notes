## Windows Autopilot for join devices.

Documentation: https://learn.microsoft.com/en-us/autopilot/add-devices#collect-the-hardware-hash

== Prerequisites.

- Windows machine.
- Admin account credentials.

== 1. Get device hash .csv file.

The first thing to do is to get the device hash by running PowerShell as administrator in the device to be enrolled using .

- Login in to the new windows machine using local admin credentials.
- Run PowerShell as administrator, to install the required module run:

```PowerShell
Install-Script -Name Get-WindowsAutoPilotInfo

previous command asks 3 questions, "Y" to questions 1 and 2, and "a" to question 3.

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

== 2. Import .csv file to Entra ID so it's in device inventory.

- Open web browser and sign in to entra and intune management center

In intune admin center:

Devices > devices onboarding > enrollment > devices

- Click **Import** button and select .csv file containing device hardware issue which should be **AutopilotHWID.csv**

Now if you refresh you should be able to see a new device.

== 3. Create deployment profile.

- Open web browser and sign in to entra and intune management center

In intune admin center:

Devices > devices onboarding > enrollment > deployment profiles

here we create a new profile or use an existing one, when creating a new one make sure to assign profile
to the group including the device(s) to be enrolled using autopilot.

4. Create ESP(Enrollment Status Page).

One of the requirements for this enrollment is having a ESP.

The Enrollment Status Page (ESP) in used to track and display the progress of a device setup when a new device is enrolled in Microsoft Intune. It ensures that the device is properly configured before user can access the desktop for the first time.

Admins can configure ESP settings to control what happens if setup fails, whether users can bypass errors, and which apps must be installed before the device is ready.

In intune admin center:

Devices > devices onboarding > enrollment > Enrollment Status Page







