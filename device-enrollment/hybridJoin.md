# This guide describes the steps and requirements to enroll a device as Hybrid Joined.

Documentation: https://learn.microsoft.com/en-us/windows/client-management/enroll-a-windows-10-device-automatically-using-group-policy

## Phase 1: Hybrid prep.

# requirements

- device must be at least AD-joined(joined to a local active directory).

- **Entra connect** must be installed and configured.

## 1. Download and install Entra Connect.

- 1.1 Go to Entra admin center(entra.microsoft.com).

- 1.2 On the left hand menu, look for **Hybrid Management** and click it, then click **Microsoft Entra Connect**

- 1.3 In the **Get started** page click on **Manage**, then scroll down a bit and click **Download Connect Sync Agent** then just accept terms and download.

## 2. Configure Entra Connect.

- 2.1 Run Entra Connect App, click **express settings**

- 2.2 In the page that says Connect to Microsoft Entra ID, and use an your entra admin account.


---


## Phase 2: Create GPO with MDM.

- 1. In the Domain Controller Machine we'll need to create a GPO with MDM configured. to do this
open **Group Policy Management** app, go to YourForest > Domains > Group Policy Objects, right-click on an empy space and select new, by doing this we are creating a new GPO, give it a name, source starter GPO is not neccesary.

- 2. Now right-click the recently created GPO and do edit, this opens the **Group Policy Management Editor**, here we go to Policies > Administrative Templates > Windows Components > MDM, now double click MDM and on the right-hand menu double-click **Enable automatic enrollment**.

- 3. By doing the last step, we are sent to configure **MDM Enable automatic enrollment**, here we select **Enabled**, afterwards, in options down below we select **User Credential**, then we save these settings.

- 4. Now we go back to **Group Policy Management** app, right-click your domain, select **link existing GPO** and select your just configured GPO for automatic enrollment.


---


## Phase 3: Intune GPO Enrollment Troubleshooting

Things to check before beginning troubleshooting:

- Licensing
- MDM Scope, this one must be set to all or some(if set to some, you'll have to select a group for this).
- Limit/Platform restrictions.
- Conditional Access: MFA enforcement(Note: GPO is not compatible with Conditional Access since GPO does not work with interactive login).
- Run **gpresult /r** or **rsop** as admin in powershell to check what GPOs were applied to the device(all these in client machine), ultimately we can force a GPO by using the **gpupdate /force** command.
- Run **dsregcmd /status** as admin in powershell to check for AzureADJoin, DomainJoin and AzureADprt(primary refresh token).
- Check task scheduler: Task Scheduler Library > Microsoft > Windows > EnterpriseMgmt
- Keys Registry: delete Enrollments keys
- Check event viewer: applications and services > microsoft > DEviceManagement-Enterprise-Diagnostic-Provider.
- Check GPO is selected to device credentials and not user credentials.
