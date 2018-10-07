# Pegasus Multi-firmware UI
No more Mr. Nice Gaius!

## MacOS
install libusb using brew

brew install libusb
or install libusb using macports

sudo port install libusb
## Windows
If your target device is not HID, you '''must''' install a driver before you can communicate with it using libusb. Currently, this means installing one of Microsoft's WinUSB, [http://sourceforge.net/apps/trac/libusb-win32/wiki libusb-win32] or [http://libusbk.sourceforge.net/UsbK3/index.html libusbK] drivers. Two options are available:

Recommended: Use the most recent version of '''[http://zadig.akeo.ie Zadig]''', an Automated Driver Installer GUI application for WinUSB, libusb-win32 and libusbK...
Alternatively, if you are only interested in WinUSB, you can download the [https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/libusb-winusb-wip/winusb%20driver.zip WinUSB driver files] and customize the inf file for your device.
For version 1.0.21 or later, you can also use usbdk backend. [https://cgit.freedesktop.org/spice/win32/usbdk usbdk] provides another driver option for libusb Windows backend. For 1.0.21, usbdk is a compile-time option, but it becomes a runtime option from version 1.0.22 onwards, so you need to specify the usbdk backend using something like the following.

```
libusb_context * ctx = NULL;
libusb_init(&ctx);
libusb_set_option(ctx, LIBUSB_OPTION_USE_USBDK);
```

## Linux
Edit/create the file:

```
sudo vi /etc/udev/rules.d/50-myusb.rules
```

Copy/paste the contents and save it:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5742", GROUP="users", MODE="0666"
SUBSYSTEM=="tty", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="5742", GROUP="users", MODE="0666"
SUBSYSTEM=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="df11", GROUP="users"  MODE="0666"
```

Then, run

```
sudo udevadm control --reload
```

add yourself to the dialout group for tty/serial permissions

```
sudo usermod -a -G dialout $USER
```
