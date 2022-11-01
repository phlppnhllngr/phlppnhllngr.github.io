---
tags: [Notebooks/Diverses]
title: Powershell
created: '2020-03-23T21:01:04.849Z'
modified: '2020-03-23T21:01:07.736Z'
parent: Diverses
---

# Powershell
- [Powershell - Notes for Professionals](https://books.goalkicker.com/PowerShellBook/)
- Aliase: <https://stackoverflow.com/questions/24914589/how-to-create-permanent-powershell-aliases/29806921#29806921>

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
