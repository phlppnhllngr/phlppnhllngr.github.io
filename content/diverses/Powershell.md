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
