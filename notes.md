# Useful references
- https://github.com/wheaney/XRLinuxDriver?tab=readme-ov-file
# How to set 3d mode properly???
1) Press 'short' button to enable 3d mode
2) Use `xrandr` to verify the default `1920 x 1080` resolution changed to `3840 x 1080`
```sh
# xrandr output
pi@RPI5-BW:~ $ xrandr
Screen 0: minimum 320 x 200, current 1920 x 1080, maximum 8192 x 8192
HDMI-1 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 1920mm x 1080mm
   1920x1080     60.00*+  59.94
HDMI-2 disconnected (normal left inverted right x axis y axis)


# Can't use HDMI splitter when getting into 3840 x 1080 mode
# To enter 3d mode, hold down 'mode' button for ~5 seconds
pi@RPI5-BW:~ $ xrandr
Screen 0: minimum 320 x 200, current 1920 x 1080, maximum 8192 x 8192
HDMI-1 connected primary 1920x1080+0+0 (normal left inverted right x axis y axis) 120mm x 70mm
   3840x1080     60.00 +
HDMI-2 disconnected (normal left inverted right x axis y axis)
  1920x1080 (0x45) 148.500MHz +HSync +VSync
        h: width  1920 start 2008 end 2052 total 2200 skew    0 clock  67.50KHz
        v: height 1080 start 1084 end 1089 total 1125           clock  60.00Hz
```
   -  The only issue with this ^^^ right now is that despite changing the `DISPLAY` resolution to `3840 x 1080` the `DESKTOP` resolution is stuck at `1920 x 1080`

---


# XRLinuxDriver Notes

## Additional packages needed
```sh
sudo apt-get -y update && sudo apt -y upgrade 
sudo apt-get -y install libusb-1.0-0-dev
sudo apt-get -y install libevdev-dev
sudo apt-get -y install libssl-dev
sudo apt-get -y install libjson-c-dev
sudo apt-get -y install libcurl4-openssl-dev
sudo apt-get -y install python3-yaml
```

```sh
T:  Bus=01 Lev=01 Prnt=01 Port=01 Cnt=02 Dev#=  8 Spd=12   MxCh= 0
D:  Ver= 2.01 Cls=ef(misc ) Sub=02 Prot=01 MxPS=64 #Cfgs=  1
P:  Vendor=35ca ProdID=1011 Rev= 2.00
S:  Manufacturer=VITURE One
S:  Product=XR Glasses
S:  SerialNumber=208B37845831
C:* #Ifs= 4 Cfg#= 1 Atr=a0 MxPwr=300mA
A:  FirstIf#= 2 IfCount= 2 Cls=02(comm.) Sub=02 Prot=01
I:* If#= 0 Alt= 0 #EPs= 2 Cls=03(HID  ) Sub=00 Prot=00 Driver=usbhid
E:  Ad=81(I) Atr=03(Int.) MxPS=  64 Ivl=1ms
E:  Ad=01(O) Atr=03(Int.) MxPS=  64 Ivl=1ms
I:* If#= 1 Alt= 0 #EPs= 2 Cls=03(HID  ) Sub=00 Prot=00 Driver=usbhid
E:  Ad=82(I) Atr=03(Int.) MxPS=  64 Ivl=1ms
E:  Ad=02(O) Atr=03(Int.) MxPS=  64 Ivl=1ms
I:* If#= 2 Alt= 0 #EPs= 1 Cls=02(comm.) Sub=02 Prot=01 Driver=cdc_acm
E:  Ad=86(I) Atr=03(Int.) MxPS=   8 Ivl=16ms
I:* If#= 3 Alt= 0 #EPs= 2 Cls=0a(data ) Sub=02 Prot=00 Driver=cdc_acm
E:  Ad=03(O) Atr=02(Bulk) MxPS=  64 Ivl=0ms
E:  Ad=85(I) Atr=02(Bulk) MxPS=  64 Ivl=0ms
```

# Current issues
- The `XR Linux Driver` 
  - Only sets up a base driver for mouse/joystick support
- For virtual display mode stuff, the repository leads --> [here](https://github.com/wheaney/breezy-desktop#setup) 
- In the virtual desktop enviornment repoistory 
  - The only support they have as of 823/24
    - GNOME
      - Despite installing GNOME, still stuck with `1920 x 1080` resolution 
    - Vulkan
- Long story short
  - Doesn't seem like we can use these repos for the RPI5