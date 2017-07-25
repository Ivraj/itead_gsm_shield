# itead_gsm_shield
Some documentation on how to get the Diymall Itead RasPi GSM shield set up. 

# Getting Started
## Installation
In order to communcate with the SIM Modem and connect to your internet provider, you'll need to install the following packages.

```
sudo apt-get install ppp picocom elinks
```

## Editing boot settings
We need to make sure that we can properly access the shield through the serial interface of the RasPi. To do this, we need to first disable the console control of 
