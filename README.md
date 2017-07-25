# itead_gsm_shield
Some documentation on how to get the Diymall Itead RasPi GSM shield set up. 

# Getting Started
## Installation
In order to communcate with the SIM Modem and connect to your internet provider, you'll need to install the following packages.

```
sudo apt-get install ppp picocom elinks
```

Next, we need to edit the boot settings. 

## Editing the boot settings
We need to make sure that we can properly access the shield through the serial interface of the RasPi. To do this, we need to first disable the console control of `/dev/serial0`. Furthermore, if you're using a RasPi 3, you'll need to enable the `uart` interface. This will involve editing `/boot/cmdline.txt` and `/boot/config.txt`.

#### Editing `/boot/cmdline.txt`
Upon opening up `/boot/cmdline.txt`, you'll probably see something like this.

```
dwc_otg.lpm_enable=0 console=serial0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
```

You'll need to remove `console=serial0,115200`. Hence, you'll be left with something like this. 

```
dwc_otg.lpm_enable=0 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait
```

#### Editing `/boot/config.txt`
Upon opening up `/boot/config.txt`, search for the `uart_enable` setting. If not already, make sure that it is enabled by adding the following line...

```
enable_uart=1
```

Be sure to save the changes you've made. 

## Adding the fona and interface files
First git clone this repo by running `git clone https://github.com/Ivraj/itead_gsm_shield`. Next, `cd` into the repo and run the following commands...

```
sudo cp interfaces /etc/network/interfaces
sudo cp fona /etc/ppp/peers/
```

## Adjust the script for your MVNO
Lastly, you'll need to add the Access Point Name (APN) of your SIM Provider to the `fona` script. Go to the fona script and change the following line...

```
connect "/usr/sbin/chat -v -f /etc/chatscripts/gprs -T [your_APN_here]"
```

... to fill in your provider's APN where it says `[your_APN_here]`. 

## TODO
- Add `restart_modem.py` so that the SIM modem is always on. 
- Test out these scripts with older RasPis. 
