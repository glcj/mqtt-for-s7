# mqtt-for-s7

*1. The MQTT protocol*
This project aims to implement MQTT 3.1 protocol on a SIMATIC S7 PLC.
This project is experimental in order to prove a concept and its use in systems that are in production is not recommended.
The MQTT protocol © 1999-2010 Eurotech, International Business Machines Corporation (IBM). All rights reserved. The description of the protocol can be downloaded from [1].

*2. S7 Development*
An interesting example for handling events and alarms is the TSPP [5] protocol, which is used at CERN for reporting events to your SCADA PVSS (aka WinCC OA).

*3. The tools*
3.1 Eclipse IDE [xx], was used for programming functional testing and release management. Also part of the functional tests will be performed using the eclipse-project libraries paho [xx].
3.2 Karaf [xx] is a Java container objects under the OSGI standard, functioning as a core for the deployment of various services. In our specific case the ActiveMQ server, which execute functions broker. Another widely used MQTT broker is mosquitto [xx], which is used as a test platform.
3.3 The protocol to be implemented should be tested in the most realistic possible scenarios for this purpose JMeter tool for load simulation which allows you to arm the scenarios will be used flexibly. In addition JMeter already have batteries of tests for MQTT and JMS.

*References:*

[1. MQ Telemetry Transport (MQTT) V3.1 Protocol Specification.]
(http://www.ibm.com/developerworks/webservices/library/ws-mqtt/index.html)

2. mosquitto. An Open Source MQTT v3.1/v3.1.1 Broker
http://mosquitto.org/

3.SINAUT ST7 Telecontrol configuration examples in Ethernet, secure Internet and (E)GPRS environment
https://support.automation.siemens.com/WW/llisapi.dll?aktprim=4&lang=en&referer=%2fWW%2f&func=cslib.csinfo&siteid=cseus&load=content&groupid=4000003&extranet=standard&viewreg=WW&nodeid4=20229805&objaction=csview

4. Telecontrol Basic
http://w3.siemens.com/mcms/industrial-communication/en/industrial-remote-communication/telecontrol/telecontrol-basic/Pages/Default.aspx?ismobile=true

5. The UNICOS Project - TSPP communications.
https://ab-project-unicos.web.cern.ch/ab-project-unicos/

6.  MQTT dissetor for Wireshark
https://github.com/menudoproblema/Wireshark-MQTT

7. This is the plugin for Jmeter to Test MQTT protocol
https://github.com/tuanhiep/mqtt-jmeter
