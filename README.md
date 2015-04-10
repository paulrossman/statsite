## Description

Installs and configures statsite, statsd implementation. https://github.com/armon/statsite

## Requirements

### Platforms

* Ubuntu 10.04 / Ubuntu 12.04
* Centos 7

### Cookbooks

* python
* git
* runit

## Usage

`recipe[statsite]` install, build and start statsite

## Attributes

### Installation/System Attributes

#### Systemd, Upstart, Init (Debian based) init systems

These attributes are used by Systemd, Upstart, Init (Debian based) init systems.

* `default[:statsite][:service_type]`  - Can be "upstart", "systemd", "init" or
  "runit". Default: "runit"
* `node[:statsite][:conf]` - Default setting:  "/etc/statsite.conf"
* `node[:statsite][:path]` - Default setting:  "/opt/statsite"
* `node[:statsite][:owner]` - Default setting:  "statsite"

#### Upstart and Init (Debian based) specific

In addition to attributes listed above, these attributes are also used by Upstart and Init.

* `node[:statsite][:group]` - Default setting:  "statsite"

#### Init (Debian based) specific

In addition to attributes listed above, this attribute is also used by Init.

* `default[:statsite][:pid_file]` - Default setting: "/var/run/statsite/statsite.pid"

### Build Attributes

* `node[:statsite][:repo]` - Default setting:  "git://github.com/armon/statsite.git"
* `node[:statsite][:ref]` - Default setting: "HEAD"

### Daemon Attributes

* `node[:statsite][:bind_address]` - Default setting: ::1
* `node[:statsite][:tcp_port]` - Default setting: 8125
* `node[:statsite][:udp_port]` - Default setting: 8125
* `node[:statsite][:loglevel]` - Default setting:  "INFO"
* `node[:statsite][:flush_interval]` - Default setting:  10
* `node[:statsite][:timer_eps]` - Default setting:  0.01
* `node[:statsite][:stream_command]` - Optional handler. Default setting:  ''
* `node[:statsite][:binary_stream]` - Optional handler. Default setting:  ''
* `node[:statsite][:use_type_prefix]` - Optional handler. Default setting: ''

## Recipes

* `recipe[statsite]` Installs/Configures statsite

## Roles

### Histogram

Additional histograms can be defined in `node[:statsite][:histogram]` attribute.

Role example:

```
{
...
  "default_attributes": {
    "statsite": {
      "bind_address": "::",
      "udp_port": 18125,
      "stream_command": "python /opt/statsite/sinks/graphite.py graphite.recfut.com 2003 statsite",
      "service_type": "upstart",
      "histogram": {
        "histogram_api": {
          "prefix": "api",
          "min": 0,
          "max": 100,
          "width": 5
        }
      }
    }
  }
...
}
```
