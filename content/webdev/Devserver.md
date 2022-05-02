---
tags: [Notebooks/Webdev]
title: Devserver
created: '2019-02-14T20:07:51.438Z'
modified: '2021-09-05T12:16:56.294Z'
parent: Webdev
---

# Devserver
- **webpack-dev-server**
  - <https://github.com/webpack/webpack-dev-server>
  - <https://webpack.js.org/configuration/dev-server/>
  - *Provides the ability to execute custom middleware*
- **tapio/live-server**
  - <https://github.com/tapio/live-server>
  - Dev Server mit live reload
- **vite** → JavaScript/Entwicklungstools
- **local-web-server**
  - <https://www.npmjs.com/package/local-web-server>
- **cors-anywhere**
  - <https://github.com/Rob--W/cors-anywhere>
  - *NodeJS reverse proxy which adds CORS headers to the proxied request*
- **web-dev-server**
  - vorher: "es-dev-server"
  - <https://modern-web.dev/docs/dev-server/overview/>


## https
- <https://letsencrypt.org/docs/certificates-for-localhost/>
- <https://bogomolov.tech/localhost-https/>
- **mkcert**
  - *A simple zero-config tool to make locally trusted development certificates with any names you'd like*
  - <https://github.com/FiloSottile/mkcert>
- **smallstep**
  - *makes using TLS in dev & pre-prod environments a whole lot easier*
  - <https://smallstep.com/blog/step-v0-8-6-valid-HTTPS-certificates-for-dev-pre-prod.html>
- **hotel**
  - *A simple process manager for developers. Start apps from your browser and access them using local domains*
  - <https://github.com/typicode/hotel>
- **https-portal**
  - *A fully automated HTTPS server powered by Nginx, Let's Encrypt and Docker.*
  - *By using it, you can run any existing web application over HTTPS, with only one extra line of configuration. The SSL certificates are obtained, and renewed from Let's Encrypt automatically.*
  - <https://github.com/SteveLTN/https-portal>
- **localdots**
  - *HTTPS domains for localhost.*
  - *Generates SSL/TLS certificates automatically*
  - *combines Caddy and smallstep/certificates with automated configuration and hot reload*
  - <https://github.com/luisfarzati/localdots>


## ngrok und Alternativen
- **ngrok**
  - <https://ngrok.com/>
  - *ngrok exposes local servers (localhost) behind NATs and firewalls to the public internet over secure tunnels*
  - *has a request log in its web UI. And, it allows replaying requests*
  - <https://www.npmjs.com/package/ngrok>
  - [Hackernews: Roll your own Ngrok with Nginx, Letsencrypt, and SSH reverse tunnelling](https://news.ycombinator.com/item?id=30891494)
- **sish**
  - *HTTP(S)/WS(S)/TCP Tunnels to localhost using only SSH.*
  - *An open source serveo/ngrok alternative.*
  - <https://github.com/antoniomika/sish>
- **localhost.run**
  - *a client-less tool to instantly make a locally running application available on an internet accessible URL*
  - <https://localhost.run/docs/>
- **localtunnel**
  - *allows you to easily share a web service on your local development machine without messing with DNS and firewall settings*
  - *will assign you a unique publicly accessible url that will proxy all requests to your locally running webserver.*
  - <https://theboroer.github.io/localtunnel-www/>
- **bore**
  - *CLI tool for making tunnels to localhost*
  - *will expose your local port at localhost to the public internet at bore.pub:PORT*
  - *Similar to localtunnel and ngrok, except bore is intended to be a highly efficient, unopinionated tool for forwarding TCP traffic that is simple to install and easy to self-host, with no frills attached.*
  - <https://github.com/ekzhang/bore>