# Zabbix Template: Proxmox VE by HTTP - CEPH & Proxmox VE by HTTP with backup and notifications

## Proxmox CEPH to Zabbix
It adds additional data regarding CEPH status on Proxmox VE by calling the same API and use the same macros as the official template.
Just add the template on the host or as linked to the official Proxmox template.

Tested in:\
Proxmox 7.0 and 8.0\
Zabbix 7.0

## Proxmox events to Zabbix
At Proxmox, in **Notifications** add a **target**:
![image](https://github.com/user-attachments/assets/12dd1861-38ce-4f06-91de-fd25cd47d470)

Copy & paste the code, and adjust the "host" to the name you have at Zabbix.
```
{
  "jsonrpc": "2.0",
  "method": "history.push",
  "params": [
    {
      "host": "hostname",
      "key": "proxmox.cluster.notifications",
      "value": "[{\"title\": \"{{ title }}\", \"message\": \"{{ url-encode message }}\", \"severity\": \"{{ severity }}\", \"node\": \"{{ fields.hostname }}\", \"event\": \"{{ fields.type }}\"}]"
    }
  ],
  "id": 1
}
```

You'll need Zabbix API secret token, paste it into **secrets**.

Finally, add a notification matcher as you see fit, and select the target that you just added.

Tested in:\
Proxmox 8.0\
Zabbix 7.0
