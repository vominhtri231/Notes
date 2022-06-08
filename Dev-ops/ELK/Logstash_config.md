# Logstash config

Logstash is configured under `/usr/share/logstash/pipeline/syslog.conf`

## Input

Logstash has the ability to aggregate logs from multiple inputs, including files, beats, syslogs, tcp, stdin (default), etc.

Since we can create logs from multiple inputs, it is importance to type and tag them so we could properly handle them in latter step

```conf
input {
  file {
    path => [ "/nodejs_server/log/*.json" ]
    type => "json"
  }
}
```

## Filter

Allows us to manipulate, filter, measure data

```conf
filter {
  json {
    source => "message"
    target => "parsedJson"
  }
  json {
    source => "message.message"
    target => "msg"
  }
}
```

## Output

Allows to push data to various locations, services and technologies, such as file, csv, rabbitmq, etc

```conf
output {
  elasticsearch {
    hosts => ["localhost:9200"]
  }
}
```
