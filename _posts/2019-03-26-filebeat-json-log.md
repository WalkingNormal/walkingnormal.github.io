---
title: filebeat-采集-json-格式的日志
date: 2019-03-26
categories:
tags: elastic
---

## 使用 `filebeat` 采集服务器上的日志，直接上传到 `Elasticsearch`

json 格式日志如下
```
{"id":"32618061","ctime":"2019-03-15 14:00:02","dev_id":"11000026","log_type":"client","info":"{\"msgid\":\"20190315140000\",\"devid\":\"11000026\",\"cmd\":\"41\",\"data\":\"RESULT:0;\"}"}
{"id":"32618062","ctime":"2019-03-15 14:00:02","dev_id":"51615729","log_type":"client","info":"{\"msgid\":\"20190315140000\",\"devid\":\"51615729\",\"cmd\":\"41\",\"data\":\"RESULT:0;\"}"}
{"id":"32618063","ctime":"2019-03-15 14:00:02","dev_id":"49173727081181","log_type":"client","info":"{\"client_id\":\"7f0000010b545c8adbc3\",\"message\":\"C432019031506001170846601DBEF\",\"client_ip\":\"218.204.252.21\"}"}
{"id":"32618061","ctime":"2019-03-15 14:00:02","dev_id":"11000026","log_type":"client","info":"{\"msgid\":\"20190315140000\",\"devid\":\"11000026\",\"cmd\":\"41\",\"data\":\"RESULT:0;\"}"}
...
```

[filebeat 官方手册](https://www.elastic.co/guide/en/beats/filebeat/current/index.html)

修改 `filebeat.yml` 配置文件如下（文件路径默认是: `/etc/filebeat/`）:
```
###################### Filebeat Configuration Example #########################

# This file is an example configuration file highlighting only the most common
# options. The filebeat.reference.yml file from the same directory contains all the
# supported options with more comments. You can use it as a reference.
#
# You can find the full configuration reference here:
# https://www.elastic.co/guide/en/beats/filebeat/index.html

# For more available modules and options, please see the filebeat.reference.yml sample
# configuration file.

#=========================== Filebeat inputs =============================

filebeat.inputs:

# Each - is an input. Most options can be set at the input level, so
# you can use different inputs for various configurations.
# Below are the input specific configurations.

- type: log

  # Change to true to enable this input configuration.
  enabled: true // 修改为 true

  # Paths that should be crawled and fetched. Glob based paths.
  paths:
    # - /var/log/*.log
    - E:/Devlogs/*.log // 增加日志路径。可以设置多个。
    #- c:\programdata\elasticsearch\logs\*
  json.keys_under_root: true // json 配置
  json.overwrite_keys: true  // json 配置
  # Exclude lines. A list of regular expressions to match. It drops the lines that are
  # matching any regular expression from the list.
  #exclude_lines: ['^DBG']

  # Include lines. A list of regular expressions to match. It exports the lines that are
  # matching any regular expression from the list.
  #include_lines: ['^ERR', '^WARN']

  # Exclude files. A list of regular expressions to match. Filebeat drops the files that
  # are matching any regular expression from the list. By default, no files are dropped.
  #exclude_files: ['.gz$']

  # Optional additional fields. These fields can be freely picked
  # to add additional information to the crawled log files for filtering
  #fields:
  #  level: debug
  #  review: 1

  ### Multiline options

  # Multiline can be used for log messages spanning multiple lines. This is common
  # for Java Stack Traces or C-Line Continuation

  # The regexp Pattern that has to be matched. The example pattern matches all lines starting with [
  #multiline.pattern: ^\[

  # Defines if the pattern set under pattern should be negated or not. Default is false.
  #multiline.negate: false

  # Match can be set to "after" or "before". It is used to define if lines should be append to a pattern
  # that was (not) matched before or after or as long as a pattern is not matched based on negate.
  # Note: After is the equivalent to previous and before is the equivalent to to next in Logstash
  #multiline.match: after


#============================= Filebeat modules ===============================

filebeat.config.modules:
  # Glob pattern for configuration loading
  path: ${path.config}/modules.d/*.yml

  # Set to true to enable config reloading
  reload.enabled: false

  # Period on which files under path should be checked for changes
  #reload.period: 10s

#==================== Elasticsearch template setting ==========================

setup.template.settings:
  index.number_of_shards: 3
  #index.codec: best_compression
  #_source.enabled: false
setup.template.name: "yizhongyun_dev_log" // 如果指定了采集的索引名称。这两个参数需要配置下。这个选项是模板名称
setup.template.pattern: "yizhongyun_dev_log-*" // 这个是模板生成正则

#================================ General =====================================

# The name of the shipper that publishes the network data. It can be used to group
# all the transactions sent by a single shipper in the web interface.
#name:

# The tags of the shipper are included in their own field with each
# transaction published.
#tags: ["service-X", "web-tier"]

# Optional fields that you can specify to add additional information to the
# output.
#fields:
#  env: staging


#============================== Dashboards =====================================
# These settings control loading the sample dashboards to the Kibana index. Loading
# the dashboards is disabled by default and can be enabled either by setting the
# options here, or by using the `-setup` CLI flag or the `setup` command.
#setup.dashboards.enabled: false

# The URL from where to download the dashboards archive. By default this URL
# has a value which is computed based on the Beat name and version. For released
# versions, this URL points to the dashboard archive on the artifacts.elastic.co
# website.
#setup.dashboards.url:

#============================== Kibana =====================================

# Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
# This requires a Kibana endpoint configuration.
setup.kibana:

  # Kibana Host
  # Scheme and port can be left out and will be set to the default (http and 5601)
  # In case you specify and additional path, the scheme is required: http://localhost:5601/path
  # IPv6 addresses should always be defined as: https://[2001:db8::1]:5601
  host: "http://xxx:5601" // kibana 地址

  # Kibana Space ID
  # ID of the Kibana Space into which the dashboards should be loaded. By default,
  # the Default Space will be used.
  #space.id:

#============================= Elastic Cloud ==================================

# These settings simplify using filebeat with the Elastic Cloud (https://cloud.elastic.co/).

# The cloud.id setting overwrites the `output.elasticsearch.hosts` and
# `setup.kibana.host` options.
# You can find the `cloud.id` in the Elastic Cloud web UI.
#cloud.id:

# The cloud.auth setting overwrites the `output.elasticsearch.username` and
# `output.elasticsearch.password` settings. The format is `<user>:<pass>`.
#cloud.auth:

#================================ Outputs =====================================

# Configure what output to use when sending the data collected by the beat.

#-------------------------- Elasticsearch output ------------------------------
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["xxx:9200"] // elasticsearch 地址

  # Enabled ilm (beta) to use index lifecycle management instead daily indices.
  #ilm.enabled: false

  index: "yizhongyun_dev_log" // 指定生成的索引名称
  

  # Optional protocol and basic auth credentials.
  #protocol: "https"
  #username: "elastic" // 如果 elasticsearch 需要账号密码，这里需要设置下
  #password: "changeme"

#----------------------------- Logstash output --------------------------------
#output.logstash:
  # The Logstash hosts
  #hosts: ["localhost:5044"]

  # Optional SSL. By default is off.
  # List of root certificates for HTTPS server verifications
  #ssl.certificate_authorities: ["/etc/pki/root/ca.pem"]

  # Certificate for SSL client authentication
  #ssl.certificate: "/etc/pki/client/cert.pem"

  # Client Certificate Key
  #ssl.key: "/etc/pki/client/cert.key"

#================================ Processors =====================================

# Configure processors to enhance or manipulate events generated by the beat.

processors:
  - add_host_metadata: ~
  - add_cloud_metadata: ~
  - decode_json_fields: 
      fields: ["base_data"]  // 可以解析第二层的 JSON 例如这样的数据 {"id":"1115","dev_id":"81742899","position":"113.54370905343,34.79941056950","ctime":"2019-02-23 19:44:09","base_data":"{\"CSQ\":\"12\",\"LNG\":\"E113.5375450\",\"LAT\":\"N34.8004766\",\"SPD\":\"1\",\"COG\":\"257\",\"VSAT\":\"12\",\"USAT\":\"5\",\"ALT\":\"120.5\",\"Ve\":\"190\",\"Vb\":\"4008\",\"ACC\":\"0\"}","@timestamp":"2019-02-23T19:44:09+08:00"} , 采集到 elastic 时, base_data 也会是 JSON
#================================ Logging =====================================

# Sets log level. The default log level is info.
# Available log levels are: error, warning, info, debug
#logging.level: debug

# At debug level, you can selectively enable logging only for some components.
# To enable all selectors use ["*"]. Examples of other selectors are "beat",
# "publish", "service".
#logging.selectors: ["*"]

#============================== Xpack Monitoring ===============================
# filebeat can export internal metrics to a central Elasticsearch monitoring
# cluster.  This requires xpack monitoring to be enabled in Elasticsearch.  The
# reporting is disabled by default.

# Set to true to enable the monitoring reporter.
#xpack.monitoring.enabled: false

# Uncomment to send the metrics to Elasticsearch. Most settings from the
# Elasticsearch output are accepted here as well. Any setting that is not set is
# automatically inherited from the Elasticsearch output configuration, so if you
# have the Elasticsearch output configured, you can simply uncomment the
# following line.
#xpack.monitoring.elasticsearch:

```

## 如何实现不同日志写入不同索引

```yml
filebeat.inputs:

# Each - is an input. Most options can be set at the input level, so
# you can use different inputs for various configurations.
# Below are the input specific configurations.

- type: log

  # Change to true to enable this input configuration.
  # enabled: true

  # Paths that should be crawled and fetched. Glob based paths.
  paths:
    # - /var/log/*-info.log     dev_info
    - E:\wamp\www\dianche\GPSlogs\*-gps.log
    # - E:\wamp\www\dianche\GPSlogs\*-mq.log
    #- c:\programdata\elasticsearch\logs\*
  fields:
    log_source: "gps"
  # json.keys_under_root: true
  # json.overwrite_keys: true
- type: log
  paths:
    - E:\wamp\www\dianche\GPSlogs\*-mq.log
  fields:
    log_source: "mq"
  # json.keys_under_root: true
  # json.overwrite_keys: true
```

定义两个 `type`。增加自定义字段 `log_source`，用在 `elasticsearch` 中写入索引时判断。

```yaml
output.elasticsearch:
  # Array of hosts to connect to.
  hosts: ["xxx:9200"]
  indices:
    - index: "test-liu-one"
      when.equals:
        fields.log_source: "gps"
    - index: "test-liu-two"
      when.equals:
        fields.log_source: "mq"

```
