# Logstash Deployment
* [Repository and installation](#repository-and-installation)
* [Mount filer storage](#mount-filer-storage)
* [Configuration](#configuration)
* [System service](#system-service)

---

# Repository and installation

1. Import the repository key\
`rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch`

1. Create the repository file `/etc/yum.repos.d/logstash.repo` with the following content:
```txt
[logstash-7.x]
name=Elastic repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

1. Install Logstash\
`yum install -y --enablerepo=logstash logstash`

# Mount filer storage

1. Create the mountpoint teraelastic in `/mnt`\
`mkdir /mnt/teraelastic/elastic5`

1. Edit `/etc/fstab` and add the following:\
`//teraelastic.ter.teradyne.com/elasticstack/elastic5 /mnt/teraelastic/ cifs credentials=/root/.teraelastic,rw,uid=logstash,gid=logstash 0 0`

1. Create the credentials file as below\
    a. Create the credentials file
    `vim /root/.teraelastic`

    b. add the following content
    ```txt
    username=srv-elastic
    password=<service_account_password>
    ```
    c. Save and close the file

    d. Change the file permission to only allow *read & write* to root\
    `chmod 600 /root/.teraelastic`

1. Mount the filer storage\
`mount -a`

    a. If above command throws an error, check previous steps for a typo.

# Configuration

1. Get the configuration files from the [repository]()

    a. From the main page in the repository, go to `logstash/config`

1. Copy the files for the node that is being configured in `/etc/logstash/`

# Verification

1. Go to `/etc/logstash`

1. Check Logstash configuration file\
`/usr/share/logstash/bin/logstash -t --path.settings /etc/logstash`

1. Check pipeline configuration file\
`/usr/share/logstash/bin/logstash --config.test_and_exit -f simple.conf`

1. If both files are fine, proceede with the next section

# Start Service

1. Enable & start Logstash service
`systemctl enable --now logstash`

1. Check service status
`systemctl status logstash`

