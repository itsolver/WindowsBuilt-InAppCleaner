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
2. Open the Win32 Content Prep Tool and select **Create a package**.
3. In the **Package Details** section, provide a name and other required information for the package.
4. In the **Installer** section, select **Add Installer** and specify the path to the `RunScript.bat` file.
5. In the **Detection** section, specify a method for detecting whether the package has already been installed.
6. In the **Dependencies** section, specify any files or programs that are required for the script to run correctly.
7. In the **Finish** section, specify a location to save the package and click the **Create** button.

## Deploying the Win32 App Package through Intune

To deploy the Win32 app package through Microsoft Intune:

1. Log in to your Microsoft Intune account.
2. Select **Apps** from the sidebar and click **Add**.
3. Select **Line-of-business app** and click **Select**.
4. In the **App package file** section, select **Upload** and browse to the location of the Win32 app package created in the previous step.
5. Fill in the required details, including the name, publisher, and installation command.
6. Under **App install behavior**, select **Only once per user** to ensure that the Win32 app runs only once during the device provisioning process.
7. Assign the app to a group of devices or users and click **Save**.

Once the app is deployed, it will run the PowerShell script to remove the built-in Windows apps specified in the `WindowsCleanup.ps1` file. The log file for the script will be stored in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs\win32-WindowsCleanup.log`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
