stone-payments.journalbeat
===================

Ansible role to setup a [journalbeat](https://github.com/mheese/journalbeat) log shipper.

## Basic usage
You may use the simplified setup by overriding the defaults on `defaults/main.yml` like this, in a minimalistic setup
that uses an ElasticSearch endpoint:
```yaml
- name: install and configure journalbeat
  hosts: all
  roles: stone-payments.journalbeat
  vars:
    journalbeat_elasticsearch: true
    journalbeat_hosts: { "logs.example.com:9200" }
```

Basically, to use the role you select an endpoint type (elasticsearch, logstash, kafka or redis), set the corresponding
variable to true and set the `journalbeat_hosts` variable to contain the endpoints' list that will have the logs
delivered to.

You also have easily available additional metadata that may be filled with useful information, like this:
```yaml
journalbeat_product: "webserver"
journalbeat_env: "production"
journalbeat_net: "dmz"
journalbeat_dc: "ny1"
```

## Advanced settings
If you need to setup any variable that isn't contained in the easy setup, you may define it in the `journalbeat_conf`
variable that holds a dict exactly the same as the YAML file used to configure the journalbeat daemon, and this
variable will be joined to the default configuration. Like this:
```yaml
journalbeat_conf:
  journalbeat:
    convert_to_numbers: false
  output:
    elasticsearch:
      path: "/somePath"
```

You may find the config file reference in the [original project
reference](https://github.com/mheese/journalbeat/blob/master/etc/journalbeat.yml).
