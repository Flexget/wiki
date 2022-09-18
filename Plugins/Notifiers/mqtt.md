---
title: mqtt
description: 
published: true
date: 2022-09-18T05:25:52.942Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:50.356Z
---

# [Notifiers](/Plugins/Notifiers) > mqtt
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; MQTT is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|


### Sorry, Beautiful documentation is work-in-progress. Use this for now / fix me.

```text
broker_address: "iot.eclipse.org"
topic: "flexget/notifications"
[broker_port: 1883]
[broker_timeout: 30]
[broker_transport: ['tcp','websockets'] ]
[broker_protocol: ['MQTTv31', 'MQTTv311'] ]
[username: yourUsernameHere]
[password: yourPasswordHere]
[encrypted_communication: True/False]
[certificates:
    broker_ca_cert: /path/to/pem/encoded/broker_ca_certificate.crt
    client_cert: /path/to/pem/encoded/client_certificate.crt
    client_key: /path/to/pem/encoded/client_certificate.key
    validate_broker_cert: True/False
    tls_version: ['tlsv1.2', 'tlsv1.1', 'tlsv1']
]
[qos: [0,1,2] ]
[retain: True/False]
```