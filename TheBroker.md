# The Broker #

From WikiPedia:

> "The purpose of the broker is to receive incoming messages from applications and perform certain actions with them. Here are some examples of possible actions by the broker:

  * Route messages to one or more other destinations
  * Transforming messages to an alternative embodiment
  * Perform an aggregation of messages, messages on various components decompose messages, forwarding them to their destinations, then recompose the answers to a single message to be sent to the user
  * Interacting with an external reservoir to augment a message or store
  * Invoke a Web service to query data
  * Reply to events or errors
  * Provide routing of messages based on their content or topics using the model of public / subscribe. "

Load tests were carried out on the PLC using two servers freely available "mosquitto" and server paho Eclipse project.


## mosquitto ##

The local server to be used "mosquitto" will be the latest version 1.3.2.

"mosquitto" has a configuration file called "mosquitto.conf" where you will be able to make adjustments such as listening port (default 1883), level of logging for debugging, use authentication, etc..

As authentication is implemented in the libraries of the PLC, is part of a possible implementation establish a VPN from the PLC to the server, a task that is not evaluated in this project.

### mosquitto broker ###

The mosquitto broker can be installed like a resident service in "windows" or daemons in "linux", in this test we used mosquitto from the command line.

We recommend the use of the option  verbose ("-v"), with this option we can make a trace of the protocol between the broker ante client. Next you can see the diferent options from the command line
e.

```
mosquitto version 1.3.2 (build date 13/07/2014 23:30:47.79)

mosquitto is an MQTT v3.1 broker.

Usage: mosquitto [-c config_file] [-d] [-h] [-p port]

-c : specify the broker config file.
-d : put the broker into the background after starting.
-h : display this help.
-p : start the broker listening on the specified port.
      Not recommended in conjunction with the -c option.
-v : verbose mode - enable all logging types. This overrides
      any logging options given in the config file.

See http://mosquitto.org/ for more information.
```

### mosquitto subscriber ###

The "mosquitto\_sub" is a client for the command line, can easily connect to the broker (mosquito or paho) and receive the messages sent to a topic or a list of predefined topics.

The different program options "mosquitto\_sub":

```
mosquitto_sub is a simple mqtt client that will subscribe to a single topic and print all messages it receives.
mosquitto_sub version 1.3.2 running on libmosquitto 1.3.2.

Usage: mosquitto_sub [-c] [-h host] [-k keepalive] [-p port] [-q qos] [-R] -t topic ...
                     [-T filter_out]
                     [-A bind_address]
                     [-i id] [-I id_prefix]
                     [-d] [-N] [--quiet] [-v]
                     [-u username [-P password]]
                     [--will-topic [--will-payload payload] [--will-qos qos] [--will-retain]]
                     [{--cafile file | --capath dir} [--cert file] [--key file]
                      [--ciphers ciphers] [--insecure]]
                     [--psk hex-key --psk-identity identity [--ciphers ciphers]]
       mosquitto_sub --help

-A : bind the outgoing socket to this host/ip address. Use to control which interface
      the client communicates over.
-c : disable 'clean session' (store subscription and pending messages when client disconnects).
-d : enable debug messages.
-h : mqtt host to connect to. Defaults to localhost.
-i : id to use for this client. Defaults to mosquitto_sub_ appended with the process id.
-I : define the client id as id_prefix appended with the process id. Useful for when the
      broker is using the clientid_prefixes option.
-k : keep alive in seconds for this client. Defaults to 60.
-N : do not add an end of line character when printing the payload.
-p : network port to connect to. Defaults to 1883.
-q : quality of service level to use for the subscription. Defaults to 0.
-R : do not print stale messages (those with retain set).
-t : mqtt topic to subscribe to. May be repeated multiple times.
-u : provide a username (requires MQTT 3.1 broker)
-v : print published messages verbosely.
-P : provide a password (requires MQTT 3.1 broker)
--help : display this message.
--quiet : don't print error messages.
--will-payload : payload for the client Will, which is sent by the broker in case of
                  unexpected disconnection. If not given and will-topic is set, a zero
                  length message will be sent.
--will-qos : QoS level for the client Will.
--will-retain : if given, make the client Will retained.
--will-topic : the topic on which to publish the client Will.
--cafile : path to a file containing trusted CA certificates to enable encrypted
            certificate based communication.
--capath : path to a directory containing trusted CA certificates to enable encrypted
            communication.
--cert : client certificate for authentication, if required by server.
--key : client private key for authentication, if required by server.
--ciphers : openssl compatible list of TLS ciphers to support.
--tls-version : TLS protocol version, can be one of tlsv1.2 tlsv1.1 or tlsv1.
                 Defaults to tlsv1.2 if available.
--insecure : do not check that the server certificate hostname matches the remote
              hostname. Using this option means that you cannot be sure that the
              remote host is the server you wish to connect to and so is insecure.
              Do not use this option in a production environment.
--psk : pre-shared-key in hexadecimal (no leading 0x) to enable TLS-PSK mode.
--psk-identity : client identity string for TLS-PSK mode.

See http://mosquitto.org/ for more information.
```

### mosquitto publisher ###

Besides receive messages, you have the "mosquitto\_pub" application which lets you connect to the broker from the command line and send messages to a specific topic.

The different program options "mosquitto\_sub":

```
mosquitto_pub is a simple mqtt client that will publish a message on a single topic and exit.
mosquitto_pub version 1.3.2 running on libmosquitto 1.3.2.

Usage: mosquitto_pub [-h host] [-p port] [-q qos] [-r] {-f file | -l | -n | -m message} -t topic
                     [-A bind_address]
                     [-i id] [-I id_prefix]
                     [-d] [--quiet]
                     [-M max_inflight]
                     [-u username [-P password]]
                     [--will-topic [--will-payload payload] [--will-qos qos] [--will-retain]]
                     [{--cafile file | --capath dir} [--cert file] [--key file]
                      [--ciphers ciphers] [--insecure]]
                     [--psk hex-key --psk-identity identity [--ciphers ciphers]]
       mosquitto_pub --help

-A : bind the outgoing socket to this host/ip address. Use to control which interface
      the client communicates over.
-d : enable debug messages.
-f : send the contents of a file as the message.
-h : mqtt host to connect to. Defaults to localhost.
-i : id to use for this client. Defaults to mosquitto_pub_ appended with the process id.
-I : define the client id as id_prefix appended with the process id. Useful for when the
      broker is using the clientid_prefixes option.
-l : read messages from stdin, sending a separate message for each line.
-m : message payload to send.
-M : the maximum inflight messages for QoS 1/2..
-n : send a null (zero length) message.
-p : network port to connect to. Defaults to 1883.
-q : quality of service level to use for all messages. Defaults to 0.
-r : message should be retained.
-s : read message from stdin, sending the entire input as a message.
-t : mqtt topic to publish to.
-u : provide a username (requires MQTT 3.1 broker)
-P : provide a password (requires MQTT 3.1 broker)
--help : display this message.
--quiet : don't print error messages.
--will-payload : payload for the client Will, which is sent by the broker in case of
                  unexpected disconnection. If not given and will-topic is set, a zero
                  length message will be sent.
--will-qos : QoS level for the client Will.
--will-retain : if given, make the client Will retained.
--will-topic : the topic on which to publish the client Will.
--cafile : path to a file containing trusted CA certificates to enable encrypted
            communication.
--capath : path to a directory containing trusted CA certificates to enable encrypted
            communication.
--cert : client certificate for authentication, if required by server.
--key : client private key for authentication, if required by server.
--ciphers : openssl compatible list of TLS ciphers to support.
--tls-version : TLS protocol version, can be one of tlsv1.2 tlsv1.1 or tlsv1.
                 Defaults to tlsv1.2 if available.
--insecure : do not check that the server certificate hostname matches the remote
              hostname. Using this option means that you cannot be sure that the
              remote host is the server you wish to connect to and so is insecure.
              Do not use this option in a production environment.
--psk : pre-shared-key in hexadecimal (no leading 0x) to enable TLS-PSK mode.
--psk-identity : client identity string for TLS-PSK mode.

See http://mosquitto.org/ for more information.
```

## Eclipse paho ##

In the web we can find many projects around IoT or MQTT protocol for high level programming languages.  For many of our developments we used extensive Java like language of choices. The Eclipse fundation, support several open source projects oriented to machine to machine solutions, one on them is the "paho" project.

> "The Paho project provides scalable open-source client implementations of open and standard messaging protocols aimed at new, existing, and emerging applications for Machine‑to‑Machine (M2M) and Internet of Things (IoT)."

From the web page of the project we can obtain the name of the broker server "iot.eclipse.org" and the listener port 1883. A simple pin gives to us the IP address of this server.

```
Haciendo ping a iot.eclipse.org [198.41.30.241] con 32 bytes de datos:
Respuesta desde 198.41.30.241: bytes=32 tiempo=124ms TTL=47
Respuesta desde 198.41.30.241: bytes=32 tiempo=308ms TTL=47
Respuesta desde 198.41.30.241: bytes=32 tiempo=135ms TTL=47
Respuesta desde 198.41.30.241: bytes=32 tiempo=198ms TTL=47

Estad¡sticas de ping para 198.41.30.241:
    Paquetes: enviados = 4, recibidos = 4, perdidos = 0
    (0% perdidos),
Tiempos aproximados de ida y vuelta en milisegundos:
    M¡nimo = 124ms, M ximo = 308ms, Media = 191ms
```

In the section dedicated to the PLC we will show how connect us to this server.