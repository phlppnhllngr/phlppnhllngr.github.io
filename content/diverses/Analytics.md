---
title: Analytics, Business Intelligence
parent: Diverses
---

# Analytics, Business Intelligence

## Tracking, Analytics
- <https://enmascript.com/articles/2019/07/15/efficient-behavioral-tracking-in-javascript-applications>
- **utm query params**
  - https://en.wikipedia.org/wiki/UTM_parameters
- **google analytics**
  - [30+ integrations](https://opentelemetry.io/registry/)
- **plausible.io**
  - <https://plausible.io/>
  - 💰/cloud oder self hosted
  - *a lightweight website analytics tool. It doesn’t use cookies and is fully compliant with GDPR, CCPA and PECR*
  - *built for privacy-conscious website owners*
- **matomo**
  - <https://matomo.org/>
  - *powerful web analytics platform that gives you and your business 100% data ownership and user privacy protection*
  - free (self hosted) oder 💰
  - <https://github.com/crazy-max/docker-matomo> (unofficial)
  - <https://github.com/matomo-org/docker> (official)
  - Hinweise
    - Adblocker (auch Brave Shield) müssen aus sein
    - Der Browser darf nicht den http-header "DNT=1" senden (do not track). matomo berücksichtigt diesen Header und wertet den Request dann nicht aus. `setDoNotTrack(false)` bewirkt, dass Daten auch gesendet werden, wenn DNT=1 ist, aber ausgewertet werden sie serverseitig trotzdem nicht. Bei `true` werden erst gar keine Requests abgesetzt.
  - 2 Möglichkeiten, per Js zu tracken
    - globale Variable `_paq` (<https://developer.matomo.org/guides/tracking-javascript-guide>)
      - bei dieser Variante kann man anfangen Events zu sammeln, bevor Matomo initialisiert wurde
    - Tracker-Instanz `window.Matomo.getTracker()` (<https://developer.matomo.org/api-reference/tracking-javascript>)
  - Tag manager
    - <https://matomo.org/docs/tag-manager/>
    - *A Tag Manager makes your life easier when you want to modify your website without needing a developer to make the necessary changes for you. Instead of having to contact a developer and waiting for someone to deploy your website, you can easily make the necessary changes yourself without having to wait for anybody else.*
  - Docs
    - track custom events
      - <https://matomo.org/docs/event-tracking/#common-event-tracking-use-cases>
      - `window._paq.push([ 'trackEvent', 'actions_performed_by_the_user', 'search_executed', 'the_search_term' ]);`
- **Open-Web-Analytics**
  - <https://github.com/Open-Web-Analytics/Open-Web-Analytics>
  - *an open source alternative to commercial tools such as Google Analytics.*
- **PostHog**
  - <https://github.com/PostHog/posthog>
  - *open source product analytics, built for developers. Automate the collection of every event on your website or app, with no need to send data to 3rd parties. It's a 1 click to deploy on your own infrastructure, with full API/SQL access to the underlying data.*
- **umami**
  - *Umami is a simple, fast, website analytics alternative to Google Analytics.*
  - <https://github.com/mikecao/umami>
- **aurora**
  - *Cookieless & Privacy Focus out of the Box*
  - <https://github.com/itsrennyman/aurora>
- **WebGazer**
  - eye tracking
  - <https://github.com/brownhci/WebGazer>
  - js
- **hotjar**
  - *heatmaps, recordings, feedback forms, surveys*
  - <https://www.hotjar.com/>
- **goatcounter**
  - *Easy web analytics. No tracking of personal data.*
  - *available as a hosted service (free for non-commercial use) or self-hosted app.*
  - *easy to use and meaningful privacy-friendly web analytics as an alternative to Google Analytics or Matomo.*
  - <https://github.com/arp242/goatcounter>
- **Rudderstack**
  - <https://www.rudderstack.com/> 
- **Apache Doris**
  - *an easy-to-use, high performance and unified analytics database.*
  - *can better meet the scenarios of report analysis, ad-hoc query, unified data warehouse, Data Lake Query Acceleration, etc. Users can build user behavior analysis, AB test platform, log retrieval analysis, user portrait analysis, order analysis, and other applications on top of this.*
  - <https://github.com/apache/doris> 
- **counter.dev**
  - <https://github.com/ihucos/counter.dev>
- **fathom** 💰
  - *Google Analytics alternative that doesn’t compromise visitor privacy for data. We revolutionized website analytics by making them easy to use and respectful of privacy laws (like GDPR and more).* 
  - <https://usefathom.com/>
- **Openpanel**
  - *All the goodies from both Mixpanel and Plausible combined into one tool.*
  - *simple analytics tool for logging events on web, apps and backend*
  - <https://github.com/Openpanel-dev/openpanel>
- **quary**
  - *Open-source BI for engineers* 
  - <https://github.com/quarylabs/quary> 


## A/B Tests
- <https://blog.tjcx.me/p/new-york-times-ab-testing>


## Visualisierung
- <https://github.com/obazoud/awesome-dashboard>
- **Metabase**
  - <https://www.metabase.com/>
  - <https://github.com/metabase/metabase> <img loading="lazy" src="https://img.shields.io/github/stars/metabase/metabase?style=flat-square"/>
  - Webapp, die DB-Daten graphisch aufbereitet
  - [unterstützte DBs](https://github.com/metabase/metabase/blob/master/docs/faq/setup/which-databases-does-metabase-support.md): H2, Postgres, mongo, mysql, ...
  - no/low code
  - GUI-Builder für SQL queries, die für Wiederverwendung gespeichert werden können
  - Anzeige als Datensätze oder Charts, Dashboards
  - [Docker-Image](https://www.metabase.com/docs/latest/operations-guide/running-metabase-on-docker.html) `docker run --rm -p 3000:3000 -v /c/docker/volumes/metabase:/metabase-data -e "MB_DB_FILE=metabase-data/metabase.db" --name metabase metabase/metabase`
  - mehrere Sprachen unterstützt, u. A. DE
  - [Lizenz](https://www.metabase.com/license/): GNU AGPL v3
- **redash**
  - <https://github.com/getredash/redash> <img loading="lazy" src="https://img.shields.io/github/stars/getredash/redash?style=flat-square"/>
  - *Make Your Company Data Driven. Connect to any data source, easily visualize, dashboard and share your data.*
  - *Redash supports more than [35 data sources](https://redash.io/help/data-sources/supported-data-sources).*
- **kibana**
  - <https://www.elastic.co/products/kibana>
  - *lets you visualize your Elasticsearch data*
  - → Logging/ELK-Stack
- **Apache Superset**
  - <https://github.com/apache/superset> <img loading="lazy" src="https://img.shields.io/github/stars/apache/superset?style=flat-square"/>
  - ähnlich metabase
  - *modern, enterprise-ready business intelligence web application*
  - *data exploration and visualization web application*
  - *intuitive interface to explore and visualize datasets, and create interactive dashboards*
  - [*support for most SQL-speaking databases*](https://superset.incubator.apache.org/#databases)
  - Bug "LegacyRow is not JSON serializable" mit DB2: <https://github.com/apache/superset/issues/24130>
  - <https://github.com/apache-superset/awesome-apache-superset>
  - Zugriff auf JSON-APIs, HTML, CSV, ... mit Lib "Shillelagh"
    - <https://github.com/betodealmeida/shillelagh>
    - <https://preset.io/blog/accessing-apis-with-superset/> 
- **cubejs**
  - <https://github.com/cube-js/cube.js> <img loading="lazy" src="https://img.shields.io/github/stars/cube-js/cube.js?style=flat-square"/>
  - *modular framework to build analytical web applications*
  - node_module
- **Power BI**
  - *Access data from hundreds of supported on-premises and cloud-based sources*
  - *Power BI Desktop (free to use) and Power BI Pro (available for a low monthly price per user).*
  - <https://powerbi.microsoft.com/>
  - Power BI Gateway
    - *Connect to on-premises data sources* 
    - <https://powerbi.microsoft.com/en-us/gateway/>
- **Lightdash**
  - *The open-source Looker alternative* 
  - <https://github.com/lightdash/lightdash> 
- **Rath**
  - *Augmented analytic engine for discovering patterns, insights, and causals. A fully-automated way to explore your data set and visualize your data with one click.*
  - *interactive data dashboard (including a automated dashboard designer which can provide suggestions to your dashboard).*
  - *Import data from online databases or CSV/JSON files.*
  - <https://github.com/Kanaries/Rath>
- **evidence**
  - *Business Intelligence as code*
  - *SQL + Markdown → Beautiful Reports*
  - <https://evidence.dev/>
  - <https://news.ycombinator.com/item?id=35645464>
- **chartbrew**
   - *used to create live reporting dashboards from APIs, MongoDB, Firestore, MySQL, PostgreSQL, and more*
  - *connect directly to databases and APIs and use the data to create beautiful charts*
  - <https://github.com/chartbrew/chartbrew>
- **Rill**
  - <https://github.com/rilldata/rill> 
