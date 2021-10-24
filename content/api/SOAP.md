---
tags: [Notebooks/API]
title: SOAP
created: '2021-06-16T12:13:12.052Z'
modified: '2021-07-02T07:41:51.122Z'
parent: API
---

# SOAP
- → Webdev/Mock Backend
- Simple Object Access Protocol
- stützt sich auf XML zur Repräsentation der Daten
- Die gängigste Kombination ist SOAP über HTTP und TCP
- Eine minimale SOAP-Nachricht besteht aus einem <mark>Envelope</mark> genannten Element, welchem ein lokaler Name zugewiesen werden muss. Dieses Element referenziert mittels eines Namensraum-Attributes auf http://www.w3.org/2003/05/soap-envelope. Kind dieses Elements muss ein <mark>Body</mark>-Element sein. Optional kann zuvor ein <mark>Header</mark>-Element stehen. In diesem können Meta-Informationen, beispielsweise zum Routing, zur Verschlüsselung oder zu Transaktionsidentifizierung, untergebracht werden. Im <mark>Body</mark>-Element sind die eigentlichen Nutzdaten untergebracht.
- Struktur einer SOAP-Nachricht:
  ```xml
  <?xml version="1.0"?>
  <s:Envelope xmlns:s="http://www.w3.org/2003/05/soap-envelope">
      <s:Header>
      </s:Header>
      <s:Body>
      </s:Body>
  </s:Envelope>
  ```
- Postman: Body = raw/XML, Content-Type muss "text/xml" sein
- SOAP v1.1 VS v1.2
  - ...

## WSDL
- [https://de.wikipedia.org/wiki/Web_Services_Description_Language](https://de.wikipedia.org/wiki/Web_Services_Description_Language)
- Web Services Description Language
- plattform-, programmiersprachen- und protokollunabhängige Beschreibungssprache für Netzwerkdienste (Webservices) zum Austausch von Nachrichten auf Basis von XML
- anhand einer .wsdl-Datei (Knoten `wsdl:types`) lassen sich DTOs generieren (Bsp Java: cxf-codegen-plugin für Maven)
- `wsdl:message` und `wsdl:operation` beschreibt soetwas wie Methoden/Funktionen
- `wsdl:portType` und `wsdl:binding` sind soetwas wie Interfaces von Client-Klassen, `wsdl:service` die Implementierung (?)
