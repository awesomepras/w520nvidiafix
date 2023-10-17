# w520nvidiafix
## how to fix display drivers for nvida optimus in Thinkpad W502
* sudo apt install build-essential manpages-dev software-properties-common
* sudo add-apt-repository ppa:ubuntu-toolchain-r/test
* sudo apt update && sudo apt install gcc-11 g++-11
* apt-get install -y nvidia-modprobe nvidia-utils-390 nvidia-settings ubuntu-drivers-common xserver-xorg-video-nvidia-390
### Detect the hardware first 
```
ubuntu-drivers devices
sudo get-edid|parse-edid
sudo nvidia-xconfig
sudo lspci | grep -i vga/nvidia (empty output)
sudo modprobe -v nvidia 
sudo lspci -k | grep -EA3 'VGA|3D|Display
```
#### Use following script
github.com/porczynski/add-display-resolution

##### Ref:
https://askubuntu.com/questions/1193045/wrong-resolution-missing-1920x1080-on-lenovo-w520-after-update-to-ubuntu-18-04
