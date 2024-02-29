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

## Connect to the IoT-LAB Leshan broker

**Important things:**

* Leshan broker is accessible only via IPv6 at **leshan6.iot-lab.info** on port 5683
* Leshan dashboard is accessible only via IPv4 at **[leshan4.iot-lab.info](http://leshan4.iot-lab.info/)** on port 80


### Register a LwM2M client

With this example you will learn how to register a client on a LwM2M Leshan server. We will use the [Eclipse Wakaama](https://www.eclipse.org/wakaama/) library (eg. C code) to implement a simple LwM2M client. You can note that the RIOT OS use this library to implement its own LwM2M stack.

```sh
ssh <login>@<site>.iot-lab.info
<login>@<site>:~$ git clone https://github.com/eclipse/wakaama.git
<login>@<site>:~$ cmake wakaama/examples/client
<login>@<site>:~$ make 
<login>@<site>:~$ ./lwm2mclient -h leshan6.iot-lab.info
Trying to bind LWM2M Client to port 56830
LWM2M Client "testlwm2mclient" started on port 56830
> Opening connection to server at leshan6.iot-lab.info:5683
 -> State: STATE_REGISTERING
22 bytes received from [2a07:2e40:fffe:10::2]:5683
64 41 7B 48  48 7B 21 42  82 72 64 0A  56 4E 73 79   dA{HH{!B.rd.VNsy
64 4B 6C 47  59 71                                   dKlGYq
 -> State: STATE_READY
```

You can check the registration directly on the [web interface](http://leshan4.iot-lab.info/) of the Leshan server. 