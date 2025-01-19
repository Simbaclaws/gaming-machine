# Gaming Machine Setup

This repository contains remote scripts to install and remove applications on your Windows machine using `winget`, without needing to clone the repository.

# ⚠️ WARNING ⚠️

**Running scripts from the web can potentially compromise your machine.**  
Before executing any script that installs or removes applications, make sure you fully understand what each command does and double-check the content of any files you are fetching.

**Only proceed if you trust the source of the script** and are certain that the applications being installed or removed are what you intend.


## Requirements
- Microsoft.AppInstaller installed from the microsoft store on version 1.8 or higher (use winget --version to check)
- Windows 10 or 11

## How to Use

You can directly fetch and execute the install or uninstall commands from the repository.

### Step 1: Install Applications

Run the following PowerShell command to install all the applications listed in the `install_apps.txt` file from the repository:

```powershell
 $ProgressPreference = 'SilentlyContinue'; (Invoke-WebRequest -Uri https://raw.githubusercontent.com/simbaclaws/gaming-machine/main/install_apps.txt).Content -split "`n" | ForEach-Object {
     $appId = $_.Trim()
     Write-Host "Attempting to install: '$appId'"
     winget install --id $appId --silent --accept-package-agreements --accept-source-agreements
}
```

This command fetches the raw content of the `install_apps.txt` file from the GitHub repository and installs each application listed in that file.

### Customization

If you'd like to customize the apps to be installed or removed, you can:
- Fork this repository and modify the `install_apps.txt` or `remove_apps.txt` files in your own GitHub repository.
- Replace the URLs in the above commands with your own GitHub raw file links.

### Example App Lists

#### Apps to Install (`install_apps.txt`):
(Apps I want installed on my gaming rig)

**The following apps will be installed**
- Bitwarden (password manager)
- SteelSeries GG
- Google Chrome
- Discord
- RSI Launcher
- Steam
- Ubisoft
- VCRedist C++ 2015-2022 (needed for games, is normally installed by specific games)
- GPU-Z (To check specific information about your gpu)
- Epic Games Launcher
- Vulkan SDK
- Razer Installer

### Troubleshooting

If any apps fail to install or uninstall, you may see error messages in PowerShell. You can run the commands manually to troubleshoot or consult the `winget` documentation for more details.

## License

This project is open source under the MIT License.
