
# eduroam Setup:



## Installation of FreeRADIUS

Installation of all necessary packages

For this particular configuration, I am utilizing an Ubuntu 18.04 server that has been configured with a public IP address,and I'm using abc university as an example i.e with domain name abc.edu.etc. So when trying to copy some files please try to change the domain name based on your domain name.

To proceed, execute the following command:
```bash
  sudo apt-get install freeradius freeradius-ldap ldap-utils
```
### Setup eduroam server
After installing the necessary packages, delete all files in the "sites-enabled" directory. Then create two new files called "eduroam" and "eduroam-inner-tunnel".

To accomplish this, execute the following commands:

1. Remove all contents within the "/etc/freeradius/3.0/sites-enabled/" path:
```bash
sudo rm /etc/freeradius/3.0/sites-enabled/*
```
2. Use the "nano" editor. Create and open a new file called "eduroam" in the "/etc/freeradius/3.0/sites-enabled/" directory. Copy and paste the contents from the provided "eduroam" file.

```bash
sudo nano /etc/freeradius/3.0/sites-enabled/eduroam
```
3. Likewise, open a new file named "eduroam-inner-tunnel" in the "/etc/freeradius/3.0/sites-enabled/" folder. Make sure to replicate the content from the original file.


```bash
sudo nano /etc/freeradius/3.0/sites-enabled/eduroam-inner-tunnel
```

#### Update the pre-proxy file with the attached file. 
```bash
sudo echo "" > /etc/freeradius/3.0/mods-config/attr_filter/pre-proxy
sudo nano /etc/freeradius/3.0/mods-config/attr_filter/pre-proxy
```
#### Configure proxy.conf and clients.conf files.
```bash
sudo rm /etc/freeradius/3.0/clients.conf
sudo rm /etc/freeradius/3.0/proxy.conf
```

Then try to download both clients.conf and proxy.conf from the [switchboard](https://switchboard.eduroam.africa/) and paste the content to the new file you created using the below command.
```bash
sudo nano /etc/freeradius/3.0/clients.conf
sudo nano /etc/freeradius/3.0/proxy.conf
```

#### Configure certificate





