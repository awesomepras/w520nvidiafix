# w520nvidiafix
## how to fix display drivers for nvida optimus in Thinkpad W502
* sudo add-apt-repository ppa:graphics-drivers/ppa
* sudo add-apt-repository ppa:ubuntu-toolchain-r/test
* sudo apt install build-essential manpages-dev software-properties-common
* 
* sudo apt update && sudo apt install gcc-11 g++-11
* apt-get install -y nvidia-modprobe libnvidia-compute-390 nvidia-driver-390 nvidia-utils-390 nvidia-settings ubuntu-drivers-common xserver-xorg-video-nvidia-390  
### Detect the hardware first 
```
ubuntu-drivers devices
sudo ubuntu-drivers list
sudo ubuntu-drivers install nvidia:390
sudo get-edid|parse-edid
sudo nvidia-xconfig
sudo lspci | grep -i vga/nvidia (empty output)
sudo modprobe -v nvidia 
sudo lspci -k | grep -EA3 'VGA|3D|Display
```

## Re-install
sudo apt purge nvidia* then restart and reinstall the driver you need 

#### Use following script
github.com/porczynski/add-display-resolution

##### Ref:
https://askubuntu.com/questions/1193045/wrong-resolution-missing-1920x1080-on-lenovo-w520-after-update-to-ubuntu-18-04
https://ubuntu.com/server/docs/nvidia-drivers-installation


####  After update to ubuntu 24.04 (noble) the kernel header is incompatible with 390 version driver
Remove everything
```
sudo apt-get remove --purge '^nvidia-.*'; sudo apt-get autoremove --purge
sudo rm -rf /etc/X11/xorg.conf.d/10-nvidia.conf
sudo rm -rf /var/lib/dkms/nvidia
sudo rm -rf /usr/share/X11/xorg.conf.d/10-nvidia.conf
```
Rebuild the kernel header
```
sudo apt install --reinstall linux-headers-$(uname -r)
```
OPtionally you can try and run the driver file from following URL but it fails at running the modules
wget https://download.nvidia.com/XFree86/Linux-x86_64/390.157/NVIDIA-Linux-x86_64-390.157.run
Dont forget to reboot
