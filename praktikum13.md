# Praktikum 13 aruanne
Praktikum 13 polnud eriti lihtne, kuid sain vist ikkagi hakkama. Aega kulus umbes 2 tundi.



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

Ma ei tea kuidas väljund saada :(
