# Win32 App Package for Windows Built-In App Cleaner

This repository contains a PowerShell script and batch file to remove built-in Windows apps during device provisioning. The script can be wrapped into a Win32 app package for deployment through Microsoft Intune.

## Prerequisites

To create and deploy the Win32 app package, you will need the following:

- [Microsoft Win32 Content Prep Tool](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool/releases)
- PowerShell script file: `WindowsCleanup.ps1`
- Batch script file: `RunScript.bat`
- Access to Microsoft Intune

## Creating the Win32 App Package

To create the Win32 app package:

1. Clone or download this repository to your local computer.
2. Open cmd and go to the path of the Win32 Content Prep Tool (IntuneWinAppUtil).
3. Run the following command to create the Win32 app package:
```
   IntuneWinAppUtil -c <path_to_cloned_repository> -s <path_to_RunScript.bat> -o <output_folder> <-q>
```
4. This command will generate the .intunewin file from the specified source folder and setup file.
   For MSI setup file, this tool will retrieve required information for Intune.
   If -a is specified, all catalog files in that folder will be bundled into the .intunewin file.
   If -q is specified, it will be in quiet mode. If the output file already exists, it will be overwritten.
   Also, if the output folder does not exist, it will be created automatically.

## Deploying the Win32 App Package through Intune

To deploy the Win32 app package through Microsoft Intune:
[label](https://endpoint.microsoft.com/)
1. Log in to your Microsoft Intune account.
2. Select **Apps** > **Windows** from the sidebar and click **Add**.
3. Select **Windows app (Win32)** and click **Select**.
4. In the **App package file** section, select **Upload** and browse to the location of the Win32 app package created in the previous step.
5. Fill in the required details, including the name, publisher, install (``RunScript.bat``) and uninstall (``RunScript.bat``) command.
6. Under Detection rules, select **Manually configure detection rules** and click **Add rule**. Select **File or folder exists** and enter:
 Path: ``C:\ProgramData\Microsoft\IntuneManagementExtension\Logs``
 File or folder: ``win32-WindowsCleanup.log``
 Detection method: ``file or folder exists``
 Associated with a 32-bit app on 64-bit clients: ``No``
7. Assign the app to a group of devices or users and click **Save**.

Once the app is deployed, it will run the PowerShell script to remove the built-in Windows apps specified in the `WindowsCleanup.ps1` file. The log file for the script will be stored in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs\win32-WindowsCleanup.log`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
