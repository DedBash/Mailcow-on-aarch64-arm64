# Installing Mailcow on aarch64/arm64
These instructions will guide you through the process of installing Mailcow on your aarch64/arm64 system.

## Installation Steps
Most parts of the guide are from mailcow itself. You can have a look at them <a href="https://docs.mailcow.email/en/i_u_m/i_u_m_install">here</a>
### Install docker
```bash
curl -sSL https://get.docker.com/ | CHANNEL=stable sh
# After the installation process is finished, you may need to enable the service and make sure it is started (e.g. CentOS 7)
systemctl enable --now docker
```
On Debian/Ubuntu systems:
```bash
apt update
apt install docker-compose-plugin git
```
On Centos 7 systems:
```bash
yum update
yum install docker-compose-plugin git
```
### Install mailcow
```bash
su
umask
#$ 0022 # <- Verify it is 0022
cd /opt
git clone https://github.com/mailcow/mailcow-dockerized
cd mailcow-dockerized
```
### Initialize mailcow
```bash
./generate_config.sh
# Generate a configuration file. Use a FQDN (host.domain.tld) as hostname when asked.
```
###  aarch64/arm64 changes
```bash
# Most docker containers are replaced with the images from ghcr.io/maxtroughear
rm docker-compose.yml
curl -o docker-compose.yml https://raw.githubusercontent.com/DedBash/Mailcow-on-aarch64-arm64/main/docker-compose.yml
# f you use the backup system from mailcow:
rm helper-scripts/backup_and_restore.sh
curl -o helper-scripts/backup_and_restore.sh https://raw.githubusercontent.com/DedBash/Mailcow-on-aarch64-arm64/main/backup_and_restore.sh
chmod +x helper-scripts/backup_and_restore.sh
```
### Start mailcow
```bash
docker compose pull
docker compose up -d
```

## Tested on 
<a href="https://hetzner.cloud/?ref=YSNOAqr7PPxY">Hetzner´s</a> CAX11 cloud server

## Credits
<a href="https://github.com/maxtroughear/docker-images/tree/main/mailcow-dockerized-arm64">maxtroughear</a> created the Docker containers
