---
tags: [Notebooks/Cloud+SaaS]
title: Serverless
created: '2019-07-06T18:18:03.958Z'
modified: '2021-03-14T15:08:02.295Z'
parent: Cloud
---

# Serverless
- FaaS: Functions as a service
- Prinzip: man bezahlt die tatsächliche Verwendung der Anwendung (z.B. jeden REST-API-Aufruf) statt einen permanent laufenden Server
- Vorteil: optimale Ressourcenauslastung, Skalierbarkeit
- Voraussetzung: gute Performance (v.a. Bootzeit) der Anwendung
- *Serverless compute options can be broken down into two broad categories:*
  - *Containers as a Service (e.g. Google Cloud Run, Fly.io)*
  - *Functions as a Service (e.g. AWS Lambda, Cloudflare Workers, Fastly Compute @ Edge, Suborbital)*
  - *Additionally, there are self-hosted offerings within each category as well (e.g. Firecracker sort-of for the former, OpenFaaS for the latter).*

## Plattformen & Frameworks
- **fn**
  - *The container native, cloud agnostic serverless platform*
  - *supports building serverless applications in Go, Java, JavaScript, Python, Ruby, C#*
  - *use any Docker container as your Function*
  - <https://github.com/fnproject/fn>
- **serverless**
    - *Build web, mobile and IoT applications with serverless architectures using AWS Lambda, Azure Functions, Google CloudFunctions & more!*
    - https://github.com/serverless/serverless *30.800
    - Node-CLI mit Starter für java-, js-, ... Projekte
- **OpenFaaS**
  - <https://www.openfaas.com/>
  - <https://github.com/openfaas/faas>
  - *deploy event-driven functions and microservices to Kubernetes without repetitive, boiler-plate coding*
  - *Build both microservices & functions in any language.*
  - *Avoid lock-in through the use of Docker. Run on any public or private cloud.*
- **serverless-stack**
  - *framework that makes it easy to build serverless apps. Set breakpoints and test your functions locally*
  - *It's an extension of AWS CDK and it features: A Live Lambda Development environment*
  - <https://github.com/serverless-stack/serverless-stack>