---
tags: [Notebooks/Diverses]
title: Datum & Zeit
created: '2020-04-02T18:50:06.011Z'
modified: '2021-07-11T09:55:28.407Z'
parent: Diverses
---

# Datum & Zeit
- **UTC**
  - https://en.wikipedia.org/wiki/Coordinated_Universal_Time
  - *no country or territory has UTC as its local time zone. In some countries, the term Greenwich Mean Time (GMT) is [still] used. It is UTC plus zero hours and therefore has the same time as UTC. Z (Zulu Time Zone) is a military time zone that is often used in aviation and the military as another name for UTC+0.*
  - [*<mark>UTC does not change with a change of seasons</mark>, but local time or civil time may change if a time zone jurisdiction observes daylight saving time (summer time).*](https://en.wikipedia.org/wiki/Coordinated_Universal_Time#Daylight_saving_time:~:text=UTC%20does%20not%20change%20with%20a,daylight%20saving%20time%20(summer%20time))
  - Deutschland befindet sich in der Timezone UTC+1. D.h., wenn es nach UTC 18:00 Uhr ist, ist es in DE 19:00 Uhr. Zur Sommerzeit (daylight saving time) ist es in DE 20:00 Uhr. Im Sommer ändert sich der "offset", von UTC+01:00 zu UTC+02:00.
- **Unix Timestamp**
  - https://en.wikipedia.org/wiki/Unix_time
  - *It is the <mark>number of seconds [or milliseconds]</mark> that have elapsed since the Unix epoch, that is the time <mark>00:00:00 UTC on 1 January 1970</mark>, minus leap seconds. Leap seconds are ignored, with a leap second having the same Unix time as the second before it, and every day is treated as if it contains exactly 86400 seconds. Due to this treatment, Unix time is not a true representation of UTC.*
- **ISO 8601**  
  - https://en.wikipedia.org/wiki/ISO_8601
  - *an international standard covering the exchange of date- and time-related data.*
  - Ein Standard, verschiedene Schreibweisen
  - Beispiele:<br/>
    `2020-04-02T16:38:48+01:00` (yyyy-mm-ddThh:mm:ssUTC-offset)<br/>
    `2020-04-02T16:38:48Z` (yyyy-mm-ddThh:mm:ssZ)
- **best practices**
  - [Stack Overflow: Daylight saving time and time zone best practices](https://stackoverflow.com/a/2532962)
  - <https://www.moesif.com/blog/technical/timestamp/manage-datetime-timestamp-timezones-in-api>

