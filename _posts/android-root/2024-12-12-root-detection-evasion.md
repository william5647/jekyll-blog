---
layout: post
title:  "Android Root Detection Evasion"
date:   2024-12-12 10:00:00 +0700
categories: jekyll update
usemathjax: true
tag:
  - tips
  - android
  - mobile
image: 
  - /root-detection-evasion/img1.PNG
image1:
  - /root-detection-evasion/img2.PNG
image2:
  - /root-detection-evasion/img4.PNG
image3:
  - /root-detection-evasion/img3.PNG
image4:
  - /root-detection-evasion/img5.PNG
---

### Magisk Hide Module

If your device has been rooted with Magisk, you can make use of the "MagiskHide" feature within the Magisk application.

1. Download the [MagiskHide](https://github.com/HuskyDG/MagiskHide) from GitHub and install it from your device's storage.
2. Enable the MagiskHide module.
3. Navigate to Settings > Enable Zygisk > Enable Enforce Deny List > Configure DenyList > Select the Application.

<figure>
<img src="{{ page.image }}" alt="MagiskHide">
<figcaption>MagiskHide</figcaption>
</figure>

### Community Script and Tool

The first essential step when using Frida is to set up the Frida server on your Android device.
This can be done easily by installing the [Frida Server](https://github.com/ViRb3/magisk-frida). Simply enable the module and restart your device.

<figure>
<img src="{{ page.image1 }}" alt="Frida Server">
<figcaption>Frida Server</figcaption>
</figure>

**Keep in mind that Frida cannot run simultaneously with MagiskHide. It is important to disable all settings applied in the previous tutorial before attempting these steps**

Another option is to download the Frida server for your specific Android platform (ARM, ARM64, x86, x86_64). You can find the Frida servers on their official release page: [Frida](https://github.com/frida/frida/releases).

```bash
$ adb push frida-server /data/local/tmp/
$ adb shell “chmod 755 /data/local/tmp/frida-server”
$ adb shell “/data/local/tmp/frida-server &”
```

#### Frida Script

This is the most commonly used and widely recognized method for bypassing root detection.

1. Connect your device to your computer using the USB cable.
2. Running the Frida script will launch the targeted application.

Here is my most used community [script](https://gist.github.com/pich4ya/0b2a8592d3c8d5df9c34b8d185d2ea35) for bypassing root detection and overcoming general protections.

```bash
frida -U -f package.name -l root-detection.js
frida -l root-detection.js -U -n 'appname'
```

<figure>
<img src="{{ page.image2 }}" alt="Frida Script">
<figcaption>Frida Script</figcaption>
</figure>


#### FridaAntiRootDetection

The next [root evasion tool](https://github.com/AshenOneYe/FridaAntiRootDetection) I’d like to share is Frida Anti Root Detection by AshenOneYe. This tool works by attaching itself to the application's processes.

All you need to do is change the target's package name in the Python script, and you're good to go! While it can be fun to experiment with these tools, always remember that responsible and ethical use of your skills is key to contributing positively to the digital community. 😁

```bash
import frida
import os

device = frida.get_usb_device()
print(device)

target = com.packagename.value
```
<figure>
<img src="{{ page.image3 }}" alt="FridaAntiRootDetection">
<figcaption>FridaAntiRootDetection</figcaption>
</figure>

#### Objection

Last but not least, we have Objection. In addition to providing root bypass functionality, it offers a wide range of versatile features, including runtime mobile exploration.

```bash
objection --gadget com.packagename.value explore
```

```bash
objection --gadget com.packagename.value explore -s "android root disable"
```

<figure>
<img src="{{ page.image4 }}" alt="Objection">
<figcaption>Objection</figcaption>
</figure>
