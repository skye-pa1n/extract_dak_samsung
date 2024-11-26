# how_to_heck_your_smsanug
This shety & stoobid guide will teach you on how to extract some funny sakeccert &amp; gakeccert & maibi more thingys from your Samsung device yay !1!1!1!1

Requirements:
You must be on a rooted device.
You must have a working brain (optional).
This was tested on a 2020 samsung device, so any samsa device with a efs partition should be able to it

**notes**
this may even work on other devices too lelelellelelelelel

Run this command on termux as root
```
dd if=/dev/block/bootdevice/by-name/efs of=/sdcard/efs.img
```

Extract the file located at /sdcard/efs.img with zarchiver.

Thats it, its done.

You will have a Funni folder called DAK (Device attestation Keys) and inside this folder you will have:


GAK_EC.private

GAK_EC.val

GAK_RSA.private

GAK_RSA.val

gakeccert.0.der

gakeccert.1.der

gakeccert.2.der

and some other SAK (Samsung attestation keys) shet


now its up to you to decrypt thy keys you found yay1!!1!1! (openssl should do it fine tbh)

Happy hecking or whatever idc lel
