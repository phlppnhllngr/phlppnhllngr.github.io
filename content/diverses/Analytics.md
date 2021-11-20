---
tags: [Notebooks/Diverses]
title: Analytics
created: '2020-03-23T21:05:49.414Z'
modified: '2021-08-15T13:17:48.578Z'
parent: Diverses
---

# Analytics

## Tracking
- <https://enmascript.com/articles/2019/07/15/efficient-behavioral-tracking-in-javascript-applications>
- **utm query params**
  - https://en.wikipedia.org/wiki/UTM_parameters
- **google analytics**
  - [30+ integrations](https://opentelemetry.io/registry/)
- **plausible.io**
  - https://plausible.io/
  - 💰/cloud oder self hosted
  - *a lightweight website analytics tool. It doesn’t use cookies and is fully compliant with GDPR, CCPA and PECR*
  - *built for privacy-conscious website owners*
- **matomo**
  - https://matomo.org/
  - *powerful web analytics platform that gives you and your business 100% data ownership and user privacy protection*
  - free (self hosted) oder 💰
  - https://github.com/crazy-max/docker-matomo (unofficial)
  - https://github.com/matomo-org/docker (official)
  - Hinweise
    - Adblocker (auch Brave Shield) müssen aus sein
    - Der Browser darf nicht den http-header "DNT=1" senden (do not track). matomo berücksichtigt diesen Header und wertet den Request dann nicht aus. `setDoNotTrack(false)` bewirkt, dass Daten auch gesendet werden, wenn DNT=1 ist, aber ausgewertet werden sie serverseitig trotzdem nicht. Bei `true` werden erst gar keine Requests abgesetzt.
  - 2 Möglichkeiten, per Js zu tracken
    - globale Variable `_paq` (https://developer.matomo.org/guides/tracking-javascript-guide)
      - bei dieser Variante kann man anfangen Events zu sammeln, bevor Matomo initialisiert wurde
    - Tracker-Instanz `window.Matomo.getTracker()` (https://developer.matomo.org/api-reference/tracking-javascript)
  - Tag manager
    - https://matomo.org/docs/tag-manager/
    - *A Tag Manager makes your life easier when you want to modify your website without needing a developer to make the necessary changes for you. Instead of having to contact a developer and waiting for someone to deploy your website, you can easily make the necessary changes yourself without having to wait for anybody else.*
  - Docs
    - track custom events
      - https://matomo.org/docs/event-tracking/#common-event-tracking-use-cases
      - `window._paq.push([ 'trackEvent', 'actions_performed_by_the_user', 'search_executed', 'the_search_term' ]);`
- **Open-Web-Analytics**
  - https://github.com/Open-Web-Analytics/Open-Web-Analytics
  - *an open source alternative to commercial tools such as Google Analytics.*
- **PostHog**
  - https://github.com/PostHog/posthog
  - *open source product analytics, built for developers. Automate the collection of every event on your website or app, with no need to send data to 3rd parties. It's a 1 click to deploy on your own infrastructure, with full API/SQL access to the underlying data.*
- **umami**
  - *Umami is a simple, fast, website analytics alternative to Google Analytics.*
  - https://github.com/mikecao/umami
- **aurora**
  - *Cookieless & Privacy Focus out of the Box*
  - https://github.com/itsrennyman/aurora
- **WebGazer**
  - eye tracking
  - https://github.com/brownhci/WebGazer
  - js
- **hotjar**
  - *heatmaps, recordings, feedback forms, surveys*
  - https://www.hotjar.com/


## A/B Tests
- <https://blog.tjcx.me/p/new-york-times-ab-testing>


## Visualisierung
- **Metabase**
  - https://www.metabase.com/
  - https://github.com/metabase/metabase ⭐20.5k
  - Webapp, die DB-Daten graphisch aufbereitet
  - [unterstützte DBs](https://github.com/metabase/metabase/blob/master/docs/faq/setup/which-databases-does-metabase-support.md): H2, Postgres, mongo, mysql, ...
  - no/low code
  - GUI-Builder für SQL queries, die für Wiederverwendung gespeichert werden können
  - Anzeige als Datensätze oder Charts, Dashboards
  - [Docker-Image](https://www.metabase.com/docs/latest/operations-guide/running-metabase-on-docker.html)

    ```sh
    docker run --rm -p 3000:3000 -v /c/docker/volumes/metabase:/metabase-data -e "MB_DB_FILE=metabase-data/metabase.db" --name metabase metabase/metabase
    ```

  - mehrere Sprachen unterstützt, u. A. DE
  - [Lizenz](https://www.metabase.com/license/): GNU AGPL v3
- **redash**
  - https://github.com/getredash/redash ⭐15.2k
  - *Make Your Company Data Driven. Connect to any data source, easily visualize, dashboard and share your data.*
  - *Redash supports more than [35 data sources](https://redash.io/help/data-sources/supported-data-sources).*
- **kibana**
  - https://www.elastic.co/products/kibana
  - *lets you visualize your Elasticsearch data*
  - → Logging/ELK-Stack
- **grafana**
  - https://grafana.com/
  - https://github.com/grafana/grafana ⭐31k
  - *allows you to query, visualize, alert on and understand your metrics no matter where they are stored*
  - *supports over 30 open source and commercial data sources.*
- **apache superset**
  - https://github.com/apache/incubator-superset ⭐27k
  - ähnlich metabase
  - *modern, enterprise-ready business intelligence web application*
  - *data exploration and visualization web application*
  - *intuitive interface to explore and visualize datasets, and create interactive dashboards*
  - [*support for most SQL-speaking databases*](https://superset.incubator.apache.org/#databases)
- **cubejs**
  - https://github.com/cube-js/cube.js ⭐5500
  - *modular framework to build analytical web applications*
  - node_module

