# This guide explains how to enroll a device as hybrid using autopilot.

## Requirements

- Use a currently supported version of Windows.
- Have access to the internet.
- Have access to an Active Directory domain controller.
- Successfully ping the domain controller of the domain being joined.
- Undergo the out-of-box experience (OOBE) on a brand new machine to later collect hash.

---

## Set up Windows automatic MDM enrollment

- Sign in to the Azure portal and select Microsoft Entra ID.

- In the left hand pane, select Manage | Mobility (MDM and WIP) > Microsoft Intune.

- Make sure users who deploy Microsoft Entra joined devices by using Intune and Windows are members of a group included in MDM User scope.

- Use the default values in the MDM Terms of use URL, MDM Discovery URL, and MDM Compliance URL boxes, and then select Save.


---


## Install the Intune Connector for Active Directory

The purpose of the **Intune Connector for Active Directory**, also known as the **Offline Domain Join (ODJ) Connector**, is to join computers to an on-premises domain during the Windows Autopilot process. The Intune Connector for Active Directory creates computer objects in a specified Organizational Unit (OU) in Active Directory during the domain join process.

## Turn off Internet Explorer Enhanced Security Configuration in server manager.

Starting with version 6.2504.2001.8, the updated Intune Connector for Active Directory switched to using **WebView2**, built on Microsoft Edge, instead of WebBrowser, built on Microsoft Internet Explorer. This change means that the Internet Explorer Enhanced Security Configuration setting in Windows Server no longer needs to be turned off. Make sure to install version 6.2504.2001.8 or later of the **Intune Connector for Active Directory** to avoid issues with the Internet Explorer Enhanced Security Configuration setting.

steps to turn it off:

- Open **server manager** in DC(Domain Controller) machine.

- Select **Local Server** on the left hand panel.

- Look for the option **IE Enhanced Security Configuration**





