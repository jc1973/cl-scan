# cl-scan

### Ubuntu instructions:

Installation of docker and components:

```bash
apt-get install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-get update
apt-get install docker-ce
```

Add user(s) to docker groups  

Make docker listen on port (needs to see if necessary):
```bash
vi /lib/systemd/system/docker.service
```
Line should be:
```
ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375 -H fd://
```
Change Kernel parametes:
```bash
vi /etc/sysctl.conf
```
Add line:
```
vm.max_map_count=262144
```
reload the docker deamon and sysctl
```bash
systemctl daemon-reload
service docker restart
sysctl -p
```
Install go:
```
wget https://dl.google.com/go/go1.9.3.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.9.3.linux-amd64.tar.gz
```
Add go bin to $PATH  (`vi /etc/environment`)

Install docker-compose:
```bash
curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
```
Install clair-scanner from here:
https://github.com/arminc/clair-scanner/releases
```bash
wget -O /usr/local/bin/clair-scanner 'https://github.com/arminc/clair-scanner/releases/download/v8/clair-scanner_linux_amd64
chmod 0755 /usr/local/bin/clair-scanner
```

