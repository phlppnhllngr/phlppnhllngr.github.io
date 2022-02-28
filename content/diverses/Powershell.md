---
tags: [Notebooks/Diverses]
title: Powershell
created: '2020-03-23T21:01:04.849Z'
modified: '2020-03-23T21:01:07.736Z'
parent: Diverses
---

# Powershell
- [Powershell - Notes for Professionals](https://books.goalkicker.com/PowerShellBook/)

## Snippets
**Prüfen, ob Ordner existiert**
`$exists = Test-Path "C:\foo\bar"`

**Prüfen, ob Datei existiert; mit Wildcard**
```powershell
if (Test-Path "C:\foo\bar-*.txt" -pathtype leaf) {
  ...
}
```
