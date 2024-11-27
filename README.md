# Extract DAK from any 2020 Samsung Device
This guide will teach you on how to extract the Device Attestation Keys from your 2020 Samsung Device.

Requirements:
You must be on a rooted device.
You must have a working brain (optional).
You need to have termux installed.
This was tested on a 2020 samsung device, but theoretically any samsung device with a efs partition should be able to it.

# **Notes**

You **need** to be rooted.
This guide won't guide you on how to decrypt the keys.

# **How-to**

Run this command on termux as root
```
dd if=/dev/block/bootdevice/by-name/efs of=/sdcard/efs.img
```

Extract the file located at /sdcard/efs.img with ZArchiver.

Thats it, its done.

You will havea folder called efs, enter it, you will have a folder called DAK(Device attestation Keys) and inside this folder you will have:


GAK_EC.private

GAK_EC.val

GAK_RSA.private

GAK_RSA.val

gakeccert.0.der

gakeccert.1.der

gakeccert.2.der

And some other SAK (Samsung attestation keys) & SGAK Keys.


Now its up to you to decrypt thy keys you found.

Happy hecking or whatever idc lel
