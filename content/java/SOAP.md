---
title: SOAP
parent: Java
---

# SOAP
- → API/SOAP
- [https://www.baeldung.com/java-soap-web-service](https://www.baeldung.com/java-soap-web-service)
- [https://github.com/eugenp/tutorials/tree/master/jee-7/src/main/java/com/baeldung/soap](https://github.com/eugenp/tutorials/tree/master/jee-7/src/main/java/com/baeldung/soap)
- **Code-Generierung mit Maven**
    - → Maven-Plugins: jaxws, cxf-codegen
- **Logging**
    ```
    -Dcom.sun.xml.ws.transport.http.client.HttpTransportPipe.dump=true
    -Dcom.sun.xml.internal.ws.transport.http.client.HttpTransportPipe.dump=true
    -Dcom.sun.xml.ws.transport.http.HttpAdapter.dump=true
    -Dcom.sun.xml.internal.ws.transport.http.HttpAdapter.dump=true
    -Dcom.sun.xml.internal.ws.transport.http.HttpAdapter.dumpTreshold=999999
    ```
- **Server**
    ```java
    // server.FooService
    @WebService @SOAPBinding
    interface FooService {
        @WebMethod String findFoo(String bar);
    }

    // server.FooServiceImpl
    @WebService(endpointInterface="server.FooService")
    class FooServiceImpl implements FooService {
        @override
        findFoo(String bar) {
            return "qux";
        }
    }

    // server.Main
    javax.xml.ws.Endpoint endoint = Endpoint.create(new server.FooServiceImpl());
    endpoint.publish("http://localhost:8888/ws");
    ```
- **Client**
    ```java
    // generated.client.FooService
    @WebService @SOAPBinding
    interface FooService {
        @WebMethod @WebResult @Action String findFoo(@WebParam String bar);
    }

    // generated.client.FooServiceImplService
    @WebServiceClient
    class FooServiceImplService extends javax.xml.ws.Service {
        @WebEndpoint
        generated.client.FooService getFooServiceImplPort() {
            return super.getPort(...);
        }
        ...
    }

    // client.Main
    FooServiceImplService implService = new generated.client.FooServiceImplService();
    generated.client.FooService fooService = implService.getFooServiceImplPort();
    fooService.findFoo("bar");
    ```
