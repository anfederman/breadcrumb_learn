#### &uarr;[top](https://ubiquityrobotics.github.io/breadcrumb_learn/)

# LiDAR

## Assemble the LiDAR on Breadcrumb

TODO

## LiDAR N301 network setup

In order to make LiDAR work setup static IP
	
	sudo nano /etc/network/interfaces

and make the eth0 interface looks like

	auto eth0
		iface eth0 inet static
		address 192.168.42.125/24 #this IP may depend on your lidar settings
		gateway 0.0.0.0
		dns-nameservers 8.8.8.8
