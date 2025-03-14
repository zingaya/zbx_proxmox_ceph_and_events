# Zabbix Template: Proxmox VE CEPH by HTTP

## Description

This template serves as additional to the official Zabbix template for Proxmox.
It adds additional data regarding CEPH status on Proxmox VE by calling the same API and use the same macros as the official template.

Tested in:\
Proxmox 6.0, 7.0 and 8.0\
Zabbix 6.4 and 7.0

Please report issues or contribute on GitHub: https://github.com/zingaya/zbx_proxmox_ceph

## Author

Leonardo Savoini

## Macros used

|Name|Description|Default|Type|
|----|-----------|-------|----|
|{$CEPH.OPERATIONS.WARN}|How many operations per sec to trigger an alert.|1000|Integer macro|

## Template links

There are no template links in this template.

## Discovery rules

There are no discovery rules in this template.

## Items

|Name|Description|Type|Key and additional info|
|----|-----------|----|-----------------------|
|Get cluster CEPH bytes available| |`Dependent item`|proxmox.cluster.ceph.status.bytes_avail|
|Get cluster CEPH bytes total| |`Dependent item`|proxmox.cluster.ceph.status.bytes_total|
|Get cluster CEPH bytes used| |`Dependent item`|proxmox.cluster.ceph.status.bytes_used|
|Get cluster CEPH health| |`Dependent item`|proxmox.cluster.ceph.status.health|
|Get cluster CEPH health message| |`Dependent item`|proxmox.cluster.ceph.status.message|
|Get cluster CEPH number of objects| |`Dependent item`|proxmox.cluster.ceph.status.num_objects|
|Get cluster CEPH number of objects (change)| |`Dependent item`|proxmox.cluster.ceph.status.num_objects.change|
|Get cluster CEPH read bytes per sec| |`Dependent item`|proxmox.cluster.ceph.status.read_bytes_sec|
|Get cluster CEPH read operations per sec| |`Dependent item`|proxmox.cluster.ceph.status.read_op_per_sec|
|Get cluster CEPH status| |`HTTP agent`|proxmox.cluster.ceph.status|
|Get cluster CEPH write bytes per sec| |`Dependent item`|proxmox.cluster.ceph.status.write_bytes_sec|
|Get cluster CEPH write operations per sec| |`Dependent item`|proxmox.cluster.ceph.status.write_op_per_sec|

## Triggers

## Graphs


## Proxmox events to Zabbix
Endpoint
POST: http://zabbix-frontend/zabbix/api_jsonrpc.php
Content-type: application/json
Authorization: Bearer {{ secrets.token }}

Secrets
token: zabbixapitoken

JSon of the body.
{
  "jsonrpc": "2.0",
  "method": "history.push",
  "params": [
    {
      "host": "lpa-pve-ceph",
      "key": "proxmox.cluster.notifications",
      "value": "[{\"title\": \"{{ title }}\", \"message\": \"{{ url-encode message }}\", \"severity\": \"{{ severity }}\", \"node\": \"{{ fields.hostname }}\", \"event\": \"{{ fields.type }}\"}]"
    }
  ],
  "id": 1
}
