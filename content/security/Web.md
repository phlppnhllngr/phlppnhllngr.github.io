---
title: Web
parent: Security
---

# Web
- <https://developer.mozilla.org/en-US/docs/Web/Security/Securing_your_site>
- <https://medium.com/simple-security/web-developer-security-checklist-f2e4f43c9c56>
- <https://mozilla.github.io/server-side-tls/ssl-config-generator/> - für diverse Webserver (nginx, Apache, ...)
- <https://github.com/shieldfy/API-Security-Checklist>
- security.txt
  - <https://securitytxt.org/>
  - <https://news.ycombinator.com/item?id=43235972>

## HTML-Attribute
- **integrity** (subresource integrity)
  - <https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity>
- **crossorigin**
  - <https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin>
  - *The "anonymous" keyword means that there will be no exchange of user credentials via cookies, client-side SSL certificates or HTTP authentication as described in the Terminology section of the CORS specification, unless it is in the same origin.*

## Http-Header
- <https://securityheaders.com/>
- <https://www.twilio.com/blog/a-http-headers-for-the-responsible-developer>
- **content security policy**
  - <https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP>
- **x-frame-options**
  - <https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options>

## Cookies
- **Set-Cookie Header-Flags**
  - Secure
    - nur HTTPS
  - HTTPOnly
    - kein Zugriff über JS (document.cookie)
  - SameSite
    - <https://simonwillison.net/2021/Aug/3/samesite/>
