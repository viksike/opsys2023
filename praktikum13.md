# Praktikum 13 aruanne
Praktikum 13 polnud eriti lihtne, kuid sain vist ikkagi hakkama. Palju abi oli tehisintellektist. Aega kulus umbes 2 tundi. Koodi ja kommentaaride korrektseks nägemiseks palun kasutada code vaadet, sest preview vaade ei ole päris tõetruu. Lisasin koodi kommentaarid selgitamaks, mis osa skriptist mida teeb.

#Sellega saab hostnamei PS versiooni ja Windowsi versiooni
$hostname = hostname
$psVersion = $PSVersionTable.PSVersion
$winVersion = [System.Environment]::OSVersion.Version

#network config
$IP = Test-Connection -ComputerName (hostname) -Count 1 | ForEach { $_.Ipv4Address }
$networkMask = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.IPAddress -eq $IP } | ForEach { $_.IPSubnet }
$gateway = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.DefaultIPGateway }
$DHCPEnabled = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.DHCPEnabled -eq $true }
$MACAddress = Get-WmiObject -Class Win32_NetworkAdapterConfiguration | Where-Object { $_.MACAddress }

#Protsessori ja füüsilise mälu andmed
$compSys = Get-WmiObject -Class Win32_ComputerSystem
$processor = $compSys.Model
$RAM = $compSys.TotalPhysicalMemory / 1GB

#Graafikakaardi info, draiveri versioon, ekraani resolutsioon
$graphicsCard = Get-WmiObject -Class Win32_VideoController
$graphicsCardName = $graphicsCard.Name
$driverVersion = $graphicsCard.DriverVersion
$driverDate = $graphicsCard.DriverDate
$screenResolution = "$($graphicsCard.CurrentHorizontalResolution) x $($graphicsCard.CurrentVerticalResolution)"

#Kõvaketta info
$disk = Get-WmiObject -Class Win32_DiskDrive
$diskSize = $disk.Size / 1GB
$freeSpace = $disk.FreeSpace / 1GB

#PCI info
$pciDevices = Get-WmiObject -Class Win32_PnPSignedDriver | Where-Object { $_.DeviceClass -eq "PCI" }

#Kasutajad
$users = Get-WmiObject -Class Win32_UserAccount

#Kõik jooksvad protsessid
$runningProcesses = (Get-Process).Count

#10 viimast protsessi
$recentProcesses = Get-Process | Sort-Object StartTime -ErrorAction SilentlyContinue | Select-Object -First 10

#Kuupäev ja kellaaeg
$date = Get-Date

#output faili systeminfo.txt
Out-File -FilePath .\SystemInfo.txt -InputObject "Hostname: $hostname`nPowerShell Version: $psVersion`nWindows Version: $winVersion`nIP Address: $IP`nNetwork Mask: $networkMask`nGateway: $gateway`nDHCP Enabled: $DHCPEnabled`nMAC Address: $MACAddress`nProcessor: $processor`nRAM: $RAM GB`nGraphics Card Name: $graphicsCardName`nDriver Version: $driverVersion`nDriver Date: $driverDate`nScreen Resolution: $screenResolution`nDisk Size: $diskSize GB`nFree Space: $freeSpace GB`nPCI Devices: $pciDevices`nUsers: $users`nRunning Processes: $runningProcesses`nRecent Processes: $recentProcesses`nDate: $date"

