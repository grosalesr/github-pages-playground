# Kibana Deployment
* [Repository and Installation](#repository-and-installation)
* [Configuration](#configuration)
    * [HTTPS certificate](#https-certificate)
* [Keystore](#keystore)
* [Plugins](#plugins)
* [System service](#system-service)
* [Verification](#verification)

---

# Repository and installation

1. Import the repository key\
`rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch`

1. Create the repository file, /etc/yum.repos.d/kibana.repo, with the following content:
```txt
[kibana-7.x]
name=Kibana repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

1. Install kibana\
`yum -y --enablerepo=kibana install kibana`

# Configuration

1.  Get the configuration file from the [repository]()

    a.  From the main page in the repository go to `kibana/config/`

    b.  There will be a directory per each host that runs Kibana

1.  Copy the appropriate configuration in `/etc/kibana`

## HTTPS certificate

1. Get certificate from **to be defined**

1. Go to /etc/kibana/

1. Create `certs ` directory

1. Copy the certificate to the `certs` directory

1. Change ownership of the certs directory and all its contents\
`chown -R root:kibana certs/`

1.  Change permission of the certs directory and all its contents\
`chmod -R 640 certs/`

# Keystore

1. Create the keystore\
`/usr/share/kibana/bin/kibana-keystore create`

1. Add elasticsearch system password to the keystore\
`/usr/share/kibana/bin/kibana-keystore add elasticsearch.password`

# Plugins

PENDING

# System service

As per configuration file, port 443 is used for HTTPS. Since it is a privileged port[^1] therefore Kibana's systemd unit file needs to be modified in order to bind to this privileged port.

1. Edit Kibana's systemd unit file\
`systemctl edit kibana.service`

1. Add the following to the file
```txt
[Service]
AmbientCapabilities=CAP_NET_BIND_SERVICE
```
    a. Save and close the file

1. Enable & start Kibana service\
`systemctl enable --now kibana`

1. Check service status\
`systemctl status kibana`

1.  Verify by going to the kibana site in a web browser

---
footnotes

[^1]: Ports 0-1023 are the "well known ports" and reserved, so you need higher privileges to bind to any of them
