---
title: WebAssembly (WASM)
parent: Webdev
---

# WebAssembly (WASM)
- <https://tourofrust.com/webassembly/TOC_en.html>
- <https://training.linuxfoundation.org/announcements/an-introduction-to-webassembly/>


## WASM + Docker
- <https://wasmlabs.dev/articles/docker-without-containers/>
  - *How does Wasm work with Docker? Docker Desktop now includes support for WebAssembly. This means that instead of the typical Windows or Linux containers which would run a separate process from a binary in the container image, you can now run a Wasm application in the WasmEdge runtime, mimicking a container. As a result, the container image does not need to contain OS or runtime context for the running application - a single Wasm binary suffices. This is explained in detail in Docker's [Wasm technical preview article](https://www.docker.com/blog/docker-wasm-technical-preview/).*


## Tools
- <https://github.com/rustwasm/wasm-bindgen>
- <https://github.com/CraneStation/wasmtime>
- <https://github.com/mbasso/awesome-wasm>
- <https://github.com/appcypher/awesome-wasm-langs>
- <https://github.com/vshymanskyy/awesome-wasm-tools>
<br/>
- <u>C#</u>
  - **Blazor**
    - client-side mode & server-side mode:
      *It’s important to distinguish between Blazor hosting models and page rendering. In the client-side model, Blazor runs on WebAssembly (WASM) inside the browser. In the server-side model, Blazor runs on the server and transfers HTML to the client via Signal-R. Both models result in a user experience comparable to SPA frameworks*
    - <https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor>
    - <https://github.com/aspnet/AspNetCore/tree/master/src/Components> *13.750
    - <https://github.com/AdrienTorris/awesome-blazor>
    - learn
      - <https://www.youtube.com/watch?v=Khn7sDUSEJM> (1h)
      - <https://cloudblogs.microsoft.com/industry-blog/en-gb/cross-industry/2019/06/21/use-vs-code-remote-development-to-run-blazor-in-a-docker-container/> (vscode docker setup)
      - <https://www.youtube.com/playlist?list=PL4WEkbdagHIR0RBe_P4bai64UDqZEbQap> (Blazor C# Tutorials, 24 videos)
      - <https://www.youtube.com/watch?v=aqSinXoStAU> (6h 23min)
      - <https://www.youtube.com/watch?v=dCgqTDki-VM> (1h)
    - UI Libs
      - <https://blazor.radzen.com/>
- <u>Java</u>
  - **CheerpJ**
    - <https://leaningtech.com/pages/cheerpj.html>
    - als SaaS ab 750€/Jahr, self-hosted mehr (?)
    - hohe Dateigrößen (Github-Seite gibt Tipps; wesentlich geringer mit gzip/brotli)<br/>
      <https://github.com/leaningtech/cheerpj-meta/wiki>
    - <https://leaningtech.com/announcing-cheerpj-3-0-a-jvm-replacement-in-html5-and-webassembly-to-run-java-applications-and-applets-on-modern-browsers/>
  - **TeaVM**
    - <http://teavm.org/>
    - <https://github.com/konsoletyper/teavm> *1.4k
    - Stand 9.2.20
      - sehr wenig Dokumentation
      - kann aus java/wasm nur numerische Datentypen nach js returnen
      - *emits small files*
      - *WebAssembly support is in experimental status*
  - **JWebAssembly**
    - *JWebAssembly is a Java bytecode to WebAssembly compiler.*
    - *The difference to similar projects is that not a complete VM with GC and memory management should be ported. It's more like a 1:1 conversion. The generated WebAssembly code is similar in size to the original Java class files.*
    - derzeit (15.4.21) kann die Kompilierung nur über ein Gradle-Plugin erfolgen, ein Maven-Plugin ist geplant
    - <https://github.com/i-net-software/JWebAssembly> *435
  - **Bytecoder**
    - *transpile [java] to other languages such as JavaScript, OpenCL or WebAssembly*
    - <https://github.com/mirkosertic/Bytecoder> *413
    - Maven-Plugin
  - **Chicory**
    - *allows you to run WebAssembly programs [in Java]*
    - <https://github.com/dylibso/chicory>
- <u>Go</u>
  - <https://github.com/golang/go/wiki/WebAssembly>
- <u>Rust</u>
  - **yew**
    - *Rust framework for creating multi-threaded front-end web apps with WebAssembly* 
    - <https://github.com/yewstack/yew>
