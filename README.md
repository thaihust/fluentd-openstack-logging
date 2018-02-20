## ISSUES
- ~~Fluentd flushes to elasticsearch with an impatient delay.~~

## To be done
- ~~Categorize the logs in their various indices.~~
- ~~Write all the configs and include them in the `collector.conf`~~
- Set up log rotation. Use [curator](https://github.com/elastic/curator)
- Rabbitmq and Mysql log config
- Parse the request tokens into request id, user id, and tenant id. Look [here](https://review.openstack.org/cat/114485%2C1%2Ctools/ansible-openstack-log/templates/etc/td-agent/td_agent.conf%5E0).
- Parse the log file `/var/log/apache2/keystone.log`
- ~~**Parse the nova-api.log file properly. Skip the stack trace.**~~

## Configuration
### Aggregator
- Fluentd
  - Log level: TRACE
  - IP: 0.0.0.0 (Default is 0.0.0.0)
  - Port: 24220 (Default is 24224)

- Elasticsearch
  - Clustername: sdcloud
  - IP: 0.0.0.0 (Default is 0.0.0.0)
  - Port: 9200 (Default is 9200)
  - Flush interval: 1s
  - Index name: Second tag part
  - Type name: Third tag part

### Collector
- Connet
  - Forward to
    - Active: 10.41.0.112:24220
    - Standby: 10.41.0.111:24220
    
- Compute
  - Forward to
    - Active: 10.41.0.112:24220
    - Standby: 10.41.0.111:24220

## Used plugins
- [Elasticsearch Plugin](https://github.com/uken/fluent-plugin-elasticsearch)
- [Grok Parser](https://github.com/kiyoto/fluent-plugin-grok-parser)
- [Forest Plugin](https://github.com/tagomoris/fluent-plugin-forest)
- [Retag Plugin](https://github.com/algas/fluent-plugin-retag)

## REF
- https://www.fluentd.org/guides/recipes/elasticsearch-and-s3
- https://itlabvn.net/he-thong/cai-dat-va-cau-hinh-fluentd-ket-hop-graylog-server-phan-2
- https://www.digitalocean.com/community/tutorials/how-to-centralize-your-docker-logs-with-fluentd-and-elasticsearch-on-ubuntu-16-04
- http://www.alickwong.com/2017/08/02/managing-logs-using-fluentd-ubuntu/
