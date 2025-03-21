# Mullvad-Reconnect-Scripts

Bash Script
```
@echo off
setlocal enabledelayedexpansion

set count=0

:: Get a list of available Mullvad country codes and pick a random one
for /f "tokens=2 delims=()" %%A in ('mullvad relay list ^| findstr /R "(..)"') do (
    set /a count+=1
    set "country[!count!]=%%A"
)

:: Pick a random country
set /a rand=%random% %% %count% + 1
set "random_country=!country[%rand%]!"

echo Connecting to a Mullvad server in: !random_country!

:: Connect to a random server in the selected country
mullvad relay set location !random_country!
mullvad connect
```

Powershell Script
```
# PowerShell Script

# Get a list of available Mullvad country codes
$countries = mullvad relay list | Select-String -Pattern "\((\w{2})\)" | ForEach-Object { $_.Matches.Groups[1].Value } | Sort-Object -Unique

# Pick a random country
$randomCountry = $countries | Get-Random
Write-Host "Connecting to a Mullvad server in: $randomCountry"

# Connect to a random server in the selected country
mullvad relay set location $randomCountry
mullvad connect
```
