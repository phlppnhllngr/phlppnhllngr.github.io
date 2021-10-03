---
tags: [Notebooks/Diverses]
title: Software-Prinzipien
created: '2020-03-28T19:05:49.640Z'
modified: '2020-03-28T19:06:00.110Z'
parent: Diverses
---

# Software-Prinzipien
- https://github.com/dwmkerr/hacker-laws
- break down problem into smaller pieces
- DRY
- KISS
- YAGNI (you aint gonna need it => nicht für das "vielleicht irgendwann mal" planen)
- fail fast (Inputs so früh wie möglich auf Sinnhaftigkeit prüfen)
- make EXACT error clear to caller
- pick the right tool for the right job
- single responsibility
- write defensive code (consider what might go wrong)
- avoid ‘Manager’, ‘Data’, ‘Info’ in class names
- Funktionen mit max 2 Args
- keine boolean Args
- versteckte side effects vermeiden
- "Anytime you're dealing with types which have a sensible 'blank' instance, you should generally return that instead of null when returning" (empty list, Person.getDefault())
- Use methods which have built-in 'if null' mechanics. For example, don't call java.util.Map's get method. Call getOrDefault or computeIfAbsent instead
- transitive Navigation vermeiden: a.getB().getC().doStuff()
- Split your classes to data holders and data 
- SOLID
  - single responsibility: class has only 1 job
  - open-closed: objects should be open for extension, but closed for modification
  - liskov-substitution:
  - interface segregation:
  - dependency inversion: entities must depend on abstractions but not on concretions
