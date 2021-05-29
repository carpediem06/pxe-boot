# PxE server

Linux uEFI
* Ubuntu 20.04 (Focal)
* Ubuntu 16.04 (Xenial)
* Centos 7.0


## Documentation

	See [pxespec.pdf](http://www.pix.net/software/pxeboot/archive/pxespec.pdf) 

## Requirements (Tested on ubuntu 18.04)

* Install a dhcp server
		```sudo apt install isc-dhcp-server```
* Configure it
		```sudo xdg-open /etc/dhcp/dhcpd.conf```
	
	Add the following lines
		``` 
		### PXE ###
		allow bootp;
		allow booting;
		subnet 192.168.5.0 netmask 255.255.255.0 {
		option broadcast-address 192.168.5.255;
		range 192.168.5.220 192.168.5.229;
		filename "pxelinux.0";
		next-server 192.168.5.2;
		ping-check = 1;
		}	```
		
* Set your IP @
		```ifconfig eno1 192.168.5.2```
		
* Restart it and check its status
		```sudo service isc-dhcp-server restart```

* Install a tftp server
		```sudo apt install tftpd-hpa ```
* Configure it
		```sudo xdg-open /etc/default/tftpd-hpa	``` 
		
	Add the following lines
		``` 
		TFTP_USERNAME="name"
		TFTP_DIRECTORY="/tftpboot"
		TFTP_ADDRESS="192.168.5.2:69"
		TFTP_OPTIONS="--secure"
		RUN_DAEMON="yes"
		``` 
* Enable port 69 through firewall
		```sudo ufw allow to any port 69 from 192.168.1.0/24	``` 
		
* Ready to boot over network
		
	
