---
title: Leshan broker
group: tools
description: Eclipse Leshan is an OMA Lightweight M2M server and client Java implementation. This documents shows how to register a LwM2M client installed on the frontend SSH with an instance of Leshan server deployed in IoT-LAB.
---

## Introduction

The IETF has created the Constrained Application Protocol (CoAP) which has a client/server model with request/response methods, means of identifying resources, and discovery mechanisms. It is similar to the HTTP protocol but for use on constrained devices. However, the use of standardised protocols does not guarantee interoperability at the application layer. This is why the OMA (Open Mobile Alliance) has defined a standard for IoT or M2M devices with the LwM2M protocol based on CoAP/DTLS. It defines the bootstrap and management of the devices, as well as a [data model](http://www.openmobilealliance.org/wp/omna/lwm2m/lwm2mregistry.html).

<figure style="text-align:center">
  <img src="{{ '/assets/images/docs/lwm2m/' | relative_url}}lwm2m.png" style="width:500px;"/><br/>
  <figcaption>LwM2M architecture (<a href="https://www.avsystem.com/blog/lightweight-m2m-lwm2m-overview/">Source</a>)</figcaption>
</figure>


### Register a LwM2M client

With this example you will learn how to register a client on a LwM2M Leshan server. We will use the [Eclipse Wakaama](https://www.eclipse.org/wakaama/) library (eg. C code) to implement a simple LwM2M client. You can note that the RIOT OS use this library to implement its own LwM2M stack.

```sh
ssh <login>@<site>.iot-lab.info
<login>@<site>:~$ git clone https://github.com/eclipse/wakaama.git
<login>@<site>:~$ cmake wakaama/examples/client
<login>@<site>:~$ make 
<login>@<site>:~$ ./lwm2mclient -h leshan.iot-lab.info
Trying to bind LWM2M Client to port 56830
LWM2M Client "testlwm2mclient" started on port 56830
> Opening connection to server at leshan.iot-lab.info:5683
 -> State: STATE_REGISTERING
22 bytes received from [2001:660:5307:3200::2]:5683
64 41 B4 18  18 B4 50 39  82 72 64 0A  32 4E 75 48   dA....P9.rd.2NuH
39 59 79 71  47 61                                   9YyqGa
 -> State: STATE_READY
```

You can check the registration directly on the [web interface](http://leshan.iot-lab.info) of the Leshan server. 