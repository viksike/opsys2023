# Praktikum 13 aruanne
Praktikum 13 polnud eriti lihtne, kuid sain vist ikkagi hakkama. Aega kulus umbes 2 tundi. Koodi ja kommentaaride korrektseks nägemiseks palun kasutada code vaadet, sest preview vaade ei ole päris tõetruu.

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
$recentProcesses = Get-Process | Sort-Object StartTime -ErrorAction SilentlyContinue | Select-Object -First 10

# Get the current date and time
$date = Get-Date

# Output the information to a file
Out-File -FilePath .\SystemInfo.txt -InputObject "Hostname: $hostname`nPowerShell Version: $psVersion`nWindows Version: $winVersion`nIP Address: $IP`nNetwork Mask: $networkMask`nGateway: $gateway`nDHCP Enabled: $DHCPEnabled`nMAC Address: $MACAddress`nProcessor: $processor`nRAM: $RAM GB`nGraphics Card Name: $graphicsCardName`nDriver Version: $driverVersion`nDriver Date: $driverDate`nScreen Resolution: $screenResolution`nDisk Size: $diskSize GB`nFree Space: $freeSpace GB`nPCI Devices: $pciDevices`nUsers: $users`nRunning Processes: $runningProcesses`nRecent Processes: $recentProcesses`nDate: $date"

