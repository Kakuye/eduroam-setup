
# eduroam Setup:



## Installation of FreeRADIUS

Installation of all necessary packages

For this particular configuration, I am utilizing an Ubuntu 18.04 server that has been configured with a public IP address,and I'm using EthERNet(Ethiopian Education and Research Network) as an example i.e with domain name ethernet.edu.etc. So when trying to copy some files please try to change the domain name based on your domain name.

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
#### Update the eap file with the attached file.
```bash
sudo echo "" > /etc/freeradius/3.0/mods-available/eap
sudo nano /etc/freeradius/3.0/mods-available/eap
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

#### Configure SSL Certificate for FreeRADIUS Server:
1. Open the 'ca.cnf' file for editing using the command:

```bash
sudo nano /etc/freeradius/3.0/certs/ca.cnf
```
2. Update the details within the file (Country Name should be ET) with your email and institution information.
3. Generate 'ca.pem' and 'ca.der' files:

```bash
cd /etc/freeradius/3.0/certs/
sudo make ca.pem
sudo make ca.der
```
4. Edit the 'server.cnf' file to align with the changes made in 'ca.cnf':

```bash
sudo nano /etc/freeradius/3.0/certs/server.cnf
```
5. Ensure the values in 'server.cnf' match those in 'ca.cnf':
6. Generate 'server.pem':

```bash
cd /etc/freeradius/3.0/certs/
sudo make server.pem
```
7. Set appropriate file ownership within the '/etc/freeradius/3.0/certs/' directory:

```bash
sudo chown freerad:freerad ca.*
sudo chown freerad:freerad server.*
sudo chown freerad:freerad index.*
```

#### Setup Testing with 'rad_eap_test':
1. Install necessary packages:

```bash
sudo apt install libnl-genl-3-200 libpcsclite1
```
2. Install 'git' and clone 'rad_eap_test':

```bash
sudo apt install git
git clone https://github.com/CESNET/rad_eap_test.git
```
3. Copy the 'eapol_test' binary to '/usr/local/bin/':
```bash
cd rad_eap_test
sudo cp bin/eapol_test /usr/local/bin/
```

## OpenLDAP Installation
