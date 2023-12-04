# Praktikum 13 aruanne
Praktikum 13 polnud eriti lihtne, kuid sain vist ikkagi hakkama. Aega kulus umbes 2 tundi. Koodi ja kommentaaride korrektseks nägemiseks palun kasutada code vaadet, sest preview vaade ei ole päris tõetruu.



#Masina nimi (hostname), PowerShelli versioon ja Windowsi versioon
$hostname = hostname
$psVersion = $PSVersionTable.PSVersion
$osVersion = (Get-CimInstance Win32_OperatingSystem).Version

#Võrgu config
$networkConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled='True'" | Select-Object PSComputername, Description, IPAddress, IPSubnet, DefaultIPGateway, DHCPEnabled, MACAddress | Sort-Object DHCPEnabled

#Protsessor ja RAM
$computerSystem = Get-WmiObject Win32_ComputerSystem | Select-Object Description, TotalPhysicalMemory

#Graafika
$videoController = Get-WmiObject Win32_VideoController | Select-Object Name, DriverVersion, DriverDate, VideoModeDescription

#Kõvaketas
$diskInfo = Get-WmiObject Win32_DiskDrive | Select-Object PartitionStyle, Size, FreeSpace

#Draiverid
$pciDevices = Get-WmiObject Win32_PnPEntity | Select-Object Description, Manufacturer, DriverVersion

#Kasutajad
$users = Get-WmiObject Win32_UserAccount | Select-Object Name, Description, LocalAccount, Disabled

#Käimasolevad protsessid
$processCount = (Get-Process).Count

#10 viimast protsessi
$recentProcesses = Get-Process | Sort-Object StartTime -Descending | Select-Object -First 10 Name, ID, StartTime

#Kuu ja kell
$dateTime = Get-Date


#Väljund
Write-Host "Masina nimi: $hostname"
Write-Host "PowerShelli versioon: $($psVersion.Major).$($psVersion.Minor)"
Write-Host "Windowsi versioon: $osVersion"
Write-Host "Võrgu konfiguratsioon: $($networkConfig | Format-List | Out-String)"
Write-Host "Arvuti protsessor: $($computerSystem.Description), RAM: $($computerSystem.TotalPhysicalMemory / 1GB) GB"
Write-Host "Graafikakaart: $($videoController | Format-List | Out-String)"
Write-Host "Kõvaketaste info: $($diskInfo | Format-List | Out-String)"
Write-Host "PCI-siinil olevate seadmete draiverid: $($pciDevices | Format-List | Out-String)"
Write-Host "Arvutis olevad kasutajad: $($users | Format-List | Out-String)"
Write-Host "Käimasolevate protsesside arv: $processCount"
Write-Host "10 viimasena käivitatud protsessi: $($recentProcesses | Format-Table | Out-String)"
Write-Host "Arvuti kuupäev ja kellaaeg: $dateTime"

väljundifaili sisu:


gpt4 faili outputiga kood
Sure, I can help you with that. Here's a basic PowerShell script that should give you the information you need. Please note that you may need to run this script with administrative privileges to access all the information.

```powershell
# Get the hostname, PowerShell version, and Windows version
$hostname = hostname
$psVersion = $PSVersionTable.PSVersion
$winVersion = [System.Environment]::OSVersion.Version

# Get the network configuration
$IP = Test-Connection -ComputerName (hostname) -Count 1 | ForEach { $_.Ipv4Address }
$networkMask = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.IPAddress -eq $IP } | ForEach { $_.IPSubnet }
$gateway = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.DefaultIPGateway }
$DHCPEnabled = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.DHCPEnabled -eq $true }
$MACAddress = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.MACAddress }

# Get the computer's processor description and total physical memory
$compSys = Get-WmiObject -Class Win32_ComputerSystem
$processor = $compSys.Model
$RAM = $compSys.TotalPhysicalMemory / 1GB

# Get the graphics card name, driver version, driver date, and screen resolution
$graphicsCard = Get-WmiObject -Class Win32_VideoController
$graphicsCardName = $graphicsCard.Name
$driverVersion = $graphicsCard.DriverVersion
$driverDate = $graphicsCard.DriverDate
$screenResolution = "$($graphicsCard.CurrentHorizontalResolution) x $($graphicsCard.CurrentVerticalResolution)"

# Get the hard disk information
$disk = Get-WmiObject -Class Win32_DiskDrive
$diskSize = $disk.Size / 1GB
$freeSpace = $disk.FreeSpace / 1GB

# Get the PCI devices driver info
$pciDevices = Get-WmiObject -Class Win32_PnPSignedDriver | Where-Object { $_.DeviceClass -eq "PCI" }

# Get the users on the computer
$users = Get-WmiObject -Class Win32_UserAccount

# Get the number of running processes
$runningProcesses = (Get-Process).Count

# Get the 10 most recently started processes
$recentProcesses = Get-Process | Sort-Object StartTime | Select-Object -Last 10

# Get the current date and time
$date = Get-Date

# Output the information to a file
Out-File -FilePath .\SystemInfo.txt -InputObject "Hostname: $hostname`nPowerShell Version: $psVersion`nWindows Version: $winVersion`nIP Address: $IP`nNetwork Mask: $networkMask`nGateway: $gateway`nDHCP Enabled: $DHCPEnabled`nMAC Address: $MACAddress`nProcessor: $processor`nRAM: $RAM GB`nGraphics Card Name: $graphicsCardName`nDriver Version: $driverVersion`nDriver Date: $driverDate`nScreen Resolution: $screenResolution`nDisk Size: $diskSize GB`nFree Space: $freeSpace GB`nPCI Devices: $pciDevices`nUsers: $users`nRunning Processes: $runningProcesses`nRecent Processes: $recentProcesses`nDate: $date"
```

This script will create a text file named `SystemInfo.txt` in the current directory with all the requested information. Please replace the placeholders with the actual commands to retrieve the information. Also, please note that this is a basic script and may need to be adjusted based on your specific needs and environment. Always test scripts in a safe and controlled environment before use. 

Please let me know if you need further assistance! 😊
