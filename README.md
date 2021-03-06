CloudEvents Java API
====================

Java API for CloudEvents(https://github.com/cloudevents/spec)

# Features

* Standard Java Bean for cloud events
* Builder Pattern to build events
* Json support by Jackson adapter
* CloudEvents JSON Schema: https://github.com/linux-china/cloud-events-java-api/blob/master/cloud-events-schema.json

# How to use

* Extend CloudEvent class:

```
public class LoginEvent extends CloudEvent<String> {

    public LoginEvent(String email, String ip) {
        setData(email);
        setContentType("text/plain");
        setExtension("ip", ip);
    }
}
```

* Create object directly

```
CloudEvent<String> loginEvent = new CloudEvent<String>("text/plain", "jacky.chenlb@alibaba-inc.com");
```

* Event Builder

```
CloudEvent<String> loginEvent = CloudEventBuilder.<String>newInstance().contentType("text/plain").data("jacky.chenlb@alibaba-inc.com").build();
```

# ObjectMapper

* ObjectMapper creation
```
ObjectMapper objectMapper = new ObjectMapper();
objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL);
objectMapper.enable(SerializationFeature.INDENT_OUTPUT);
```

* write as String
```
objectMapper.writeValueAsString(loginEvent);
```

* read from json text
```
objectMapper.readValue(jsonText, new TypeReference<CloudEvent<String>>() {});
```

# Protocol Buffer

Please refer CloudEventMapper for converter between JavaBean and ProtoMessage.

# Event Logging

CloudEvent ships with default toString pattern: CloudEvent{cloudEventsVersion='0.1',eventID='xxx'}

```
12:49:22,076 |-INFO in ch.qos.logback.classic.LoggerContext[default] - CloudEvent{cloudEventsVersion='0.1',eventID='xxx'}
```

# Event Broker

Please consider NATS or NATS Streaming to post or subscribe cloud events.

# References

* CloudEvents Specification: https://github.com/cloudevents/spec
* CloudEvents Date format: https://tools.ietf.org/html/rfc3339
* NATS: https://nats.io/
