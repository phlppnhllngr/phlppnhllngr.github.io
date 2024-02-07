---
title: Powershell
parent: Diverses
---

# Powershell
- [Powershell - Notes for Professionals](https://books.goalkicker.com/PowerShellBook/)
- Aliase: <https://stackoverflow.com/questions/24914589/how-to-create-permanent-powershell-aliases/29806921#29806921>
- [The weird world of Windows file paths](https://www.fileside.app/blog/2023-03-17_windows-file-paths/)

## Snippets
**Prüfen, ob Ordner existiert**
```ps1
$exists = Test-Path "C:\foo\bar"
```

**Prüfen, ob Datei existiert; mit Wildcard**
```powershell
if (Test-Path "C:\foo\bar-*.txt" -pathtype leaf) {
  ...
}
```

**CPU- und RAM-Verbrauch ausgeben**
```powershell
# Get process information
$processes = Get-Process

# Select specific properties (ProcessName, CPU, Memory)
$processInfo = $processes | Select-Object ProcessName, CPU, @{Name="Memory(MB)"; Expression={$_.WorkingSet / 1MB}} | Sort-Object -Descending CPU

# Display process information
$processInfo

# If you want to get the total CPU and memory usage of all processes, you can use Measure-Object:
$totalCPU = $processInfo | Measure-Object -Property CPU -Sum | Select-Object -ExpandProperty Sum
$totalMemory = $processes | Measure-Object -Property WorkingSet -Sum | Select-Object -ExpandProperty Sum

# Display total CPU and memory usage
Write-Host "Total CPU Usage: $totalCPU%"
Write-Host "Total Memory Usage: $($totalMemory / 1MB) MB"
Write-Host ""
```
