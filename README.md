# ELK-DOCKER-STACK

[![Generic badge](https://img.shields.io/badge/ELK-7.4.2-<COLOR>.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/KIBANA-7.4.2-<COLOR>.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/LOGSTASH-7.4.2-<COLOR>.svg)](https://shields.io/)


## How to run

```console
$ docker-compose build
$ docker-compose up
```

Based on the official Docker images from Elastic:

* [elasticsearch](https://github.com/elastic/elasticsearch-docker)
* [logstash](https://github.com/elastic/logstash-docker)
* [kibana](https://github.com/elastic/kibana-docker) 

By default, the stack exposes the following ports:

* 5000: Logstash TCP input
* 900: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana

## Configuration

**NOTE**: Configuration is not dynamically reloaded.

### Kibana onfiguration

- `kibana/config/kibana.yml`
- `config` (map entire directory instead of a single file)

### Logstash configuration

- `logstash/config/logstash.yml`.
- `config` (map entire directory instead of a single file, 
however you must need a `log4j2.properties` file for it's own logging)

### Elasticsearch configuration

- `elasticsearch/config/elasticsearch.yml`.

Specify the options to override directly via environment variables:

```yml
elasticsearch:

  environment:
    network.host: "_non_loopback_"
    cluster.name: "my-cluster"
```

## Storage

### Persist Elasticsearch data

```yml
elasticsearch:

  volumes:
    - /path/to/storage:/usr/share/elasticsearch/data
```

**NOTE:** 
Beware of the [unprivileged `elasticsearch` user][esuser] is used within the Elasticsearch image, therefore the mounted data directory must be owned by the uid `1000`.

[esuser]: https://github.com/elastic/elasticsearch-docker/blob/016bcc9db1dd97ecd0ff60c1290e7fa9142f8ddd/templates/Dockerfile.j2#L22

## Using a newer stack version

- `.env`

**NOTE**: Pay attention to the [upgrade instructions](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-upgrade.html)
for each individual component before performing a stack upgrade.
  

