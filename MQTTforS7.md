# MQTT for S7 #

This project aims to implement MQTT 3.1 protocol on a SIMATIC S7 PLC.

**This project is experimental in order to prove a concept and its use in systems that are in production is not recommended.**



  * [Objetive](MQTTforS7#Objective.md)
  * [General architecture](MQTTforS7#General_architecture.md)
  * [Tools](MQTTforS7#Tools.md)
  * [References](MQTTforS7#References.md)


## Objetive ##

The next noise in the area of ​​Information Technology is the IoT (Internet of thing), or what is the same information management for highly distributed devices (cell phones, TV, cars, etc..) And connecting means intermittent and limited band width. However I have seen very few examples running on PLC's

The backbone of all this is the MQTT protocol developed by IBM for telemetry applications.

Based on the foregoing, I developed the protocol MQTT to S7 in the first stage and being functional PCS7 in the near future.

The MQTT protocol is specially designed for use in systems with limited bandwidth and possible failures in communication links, eg a typical case of the oil & gas applications or where water treatment stations are separated geographically.

Due to the characteristics of the protocol is a suitable candidate for development into a S7, without the use of special communication cards.


Possible applications:

  1. Gas and oil pipes
  1. Treatment waters.
  1. Reporting Systems (S88 Batch)
  1. RPC for S7

I'll be releasing the code as open source, so that it is available for those wanting to experience the MQTT protocol.

## General architecture ##

![https://mqtt-for-s7.googlecode.com/git-history/master/docs/arquitectura02.png](https://mqtt-for-s7.googlecode.com/git-history/master/docs/arquitectura02.png)

Figure 1.

A usage scenario for MQTT protocol is the telemetry in geographically distributed systems, case type industries OIL & GAS and water treatment. Figure 1 shows the typical case where each monitoring station must report to the central server the events in the process or equipment failures that are considered important. Generally is required that the generated events are not lost in the event of a fall of the communications link.

In the industry and many protocols exist which perform this function, for example DNP 3.0, IEC 60870-5-101 and IEC 60870-5-104, owners as well as development for Motorola MDLC developed for their RTU. In any case are already standardized protocols and field-tested in each of their domains.


![https://mqtt-for-s7.googlecode.com/git-history/master/docs/images/figure02.png](https://mqtt-for-s7.googlecode.com/git-history/master/docs/images/figure02.png)
Figure 2.



Another use case for the protocol can be found in the food and beverage industry. Processes in these industries many processes are executed in batch, or sequential, as shown in Figure 2.

For example, during the execution of a process, run a transition "T", you must make the request to a server new parameters recipes work for the "A" activity that will be executed by the PLC.

In many cases the interaction of a PLC to an external server is relatively complex and slow especially given the way the PLC runs programs. An example of this can be found in OpenBatch based servers which define a complex interface called PLI, which is relatively slow in terms of executing a PLC given the number of execution cycles required.

An interesting solution would be the implementation of RPC (Remote Procedure Call) on the PLC using the MQTT as transportation and services running on the server.

## Tools ##

For testing the protocol will be used the following tools:

  * **mosquitto**: A broker that implements the MQTT protocol 3.1, which also has client programs (subcriberse leg and publish messages to topics.
  * **Jmeter**: This tool allows to establish test scenarios against different types of servers. It will load testing against PLC.
  * **mqtt-jmeter**: Is the Jmeter plugin that allows the use of MQTT protocol to build test scenarios.
  * **Step7**: The programming software for PLC Siemens S7.
  * **Eclipse paho**: Internet server and Java client librarys.

With these tools we can build tests under different load scenarios to the PLC, which we will explain later.

## References ##

[1](http://www.ibm.com/developerworks/webservices/library/ws-mqtt/index.html). MQ Telemetry Transport (MQTT) V3.1 Protocol Specification.


[2](http://mosquitto.org/). mosquitto. An Open Source MQTT v3.1/v3.1.1 Broker


[3](https://support.automation.siemens.com/WW/llisapi.dll?aktprim=4&lang=en&referer=%2fWW%2f&func=cslib.csinfo&siteid=cseus&load=content&groupid=4000003&extranet=standard&viewreg=WW&nodeid4=20229805&objaction=csview).SINAUT ST7 Telecontrol configuration examples in Ethernet, secure Internet and (E)GPRS environment.

[4](http://w3.siemens.com/mcms/industrial-communication/en/industrial-remote-communication/telecontrol/telecontrol-basic/Pages/Default.aspx?ismobile=true). Telecontrol Basic

[5](https://ab-project-unicos.web.cern.ch/ab-project-unicos/). The UNICOS Project - TSPP communications.

[6](https://github.com/menudoproblema/Wireshark-MQTT). MQTT dissetor for Wireshark

[7](http://www.eclipse.org/paho/). Eclipse paho project.

[8](http://jmeter.apache.org/). Apache JMeter.

[9](https://github.com/tuanhiep/mqtt-jmeter). JMeter MQTT plugin.