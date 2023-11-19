## Debian 11 amd64 - Package install of ver 9.0 piaware, dump1090-fa, piaware-web, dump978-fa

### STEP-1: Add this repository to list of apt sources by following 3 commands:
_**First two commands are long. Please scroll right to see and copy them in FULL.**_
```
sudo wget -O /etc/apt/sources.list.d/abcd567a.list https://abcd567a.github.io/debian11/abcd567a.list 
```
```
sudo wget -O /etc/apt/trusted.gpg.d/abcd567a-key.gpg https://abcd567a.github.io/debian11/KEY2.gpg  
```
```
sudo apt update  
```

</br>

### STEP-2: Install packages
```
sudo apt install piaware  
```
```
sudo apt install dump1090-fa  
```
```
sudo apt install piaware-web  
```
```
sudo reboot  
```
</br></br>
## For USA only - dump978-fa
```
sudo apt install dump978-fa  
```

```
sudo piaware-config uat-receiver-type sdr  
```


If you want to receive both ES1090 and UAT978, then two dongles are required, one for 1090 MHz and other for 978 MHz. In this case you will have to serialize dongles so that correct dongle+antenna sets are used by dump1090-fa and dump978-fa.
Serialize dongles as follows </br>

**For 1090 Mhz dongle: use 8-digit serial # 00001090** </br>
**For 978 Mhz dongle : use 8-digit serial # 00000978** </br>

(1) Issue following command to install serialization software: </br>
```
sudo apt install rtl-sdr 
``` 
</br>

(2) Unplug ALL DVB-T dongles from RPi

(3) Plugin only that DVB-T dongle which you want to use for dump1090-fa. All other dongles should be unplugged.

(4) Issue following command. </br>
```
rtl_eeprom -s 00001090 
``` 
</br>
Say yes when asked for confirmation to change serial number.


(5) Unplug 1090 dongle

(6) Plugin only that DVB-T dongle which you want to use for dump978-fa. All other dongles should be unplugged.

(7) Issue following command. </br>
```
rtl_eeprom -s 00000978 
``` 
</br>
Say yes when asked for confirmation to change serial number.


(8) Unplug 978 dongle

IMPORTANT: After completing above commands, unplug and then replug both dongles.


### (9) Configure dump1090-fa and dump978-fa to use their respective dongles.

```
sudo sed -i 's/^RECEIVER_SERIAL=.*/RECEIVER_SERIAL=00001090/' /etc/default/dump1090-fa  
```

```
sudo sed -i 's/driver=rtlsdr[^ ]* /driver=rtlsdr,serial=00000978 /' /etc/default/dump978-fa  
```  

```
sudo reboot 
```

&nbsp;

### NOTE: REMOVING ENTRY OF MY REPOSITORY FROM YOUR COMPUTER:
If anytime in future you want to delete my repository from your Computer’s apt sources list, use following commands:

```
sudo rm /etc/apt/sources.list.d/abcd567a.list 
```

```
sudo apt update 
```
