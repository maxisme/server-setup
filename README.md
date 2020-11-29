# ansible
```shell script
$ cd ansible
$ ansible-galaxy collection install community.crypto
$ ansible-galaxy install maxisme.wireguard_private_networking rossmcdonald.telegraf --force
$ ansible-playbook -i hosts server-setup.yml
```
add hosts to `/etc/ansible/hosts` - e.g:
```
node1 ansible_host=172.104.205.199 vpn_ip=10.1.0.3
[ssh]
node1

[hostname]
node1

[wg]
node1

[telegraf]
node1
```
`ansible all -m ping`

# raspbian
```
echo "deb http://deb.debian.org/debian/ unstable main" | sudo tee --append /etc/apt/sources.list
apt-key adv --keyserver   keyserver.ubuntu.com --recv-keys 04EE7237B7D453EC
apt-key adv --keyserver   keyserver.ubuntu.com --recv-keys 648ACFD622F3D138
sh -c 'printf "Package: *\nPin: release a=unstable\nPin-Priority: 90\n" > /etc/apt/preferences.d/limit-unstable'
apt-get update
apt install wireguard
apt install raspberrypi-kernel-headers
```
# telegraf
add your variables to the `vars/main.yml` :
```yml
influxdburl:
influxdbuser:
influxdbpass:
```

also make sure telegraf can read docker on each host
 
```
$ usermod -aG docker telegraf
```