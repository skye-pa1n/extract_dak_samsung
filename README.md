# Extract DAK from any 2020 Samsung Device
This guide will teach you on how to extract the Device Attestation Keys from your 2020 Samsung Device.

Requirements:
You must be on a rooted device.
You must have a working brain (optional).
You need to have termux installed.
This was tested on a 2020 samsung device, but theoretically any samsung device with a efs partition should be able to it.

# **Notes**

You **need** to be rooted.

This guide **WILL NOT** guide you on how to decrypt the keys. (They are prob encrypted to industry standart.)

# **How-to**

Run this command on termux as root to excract you efs partition.
```
dd if=/dev/block/bootdevice/by-name/efs of=/sdcard/efs.img
```

Extract the file located at /sdcard/efs.img with ZArchiver.

Thats it, its **done.*

You will have a folder called efs, enter it, you will have a folder called DAK(Device attestation Keys) and inside this folder you will have:


GAK_EC.private

GAK_EC.val

GAK_RSA.private

GAK_RSA.val

gakeccert.0.der

gakeccert.1.der

gakeccert.2.der

And some other SAK (Samsung attestation keys) & SGAK Keys.

# **"Decrypt"* .der files (Certificates)
Run this on termux at the directory the .der files are at
```
openssl x509 -noout -text -inform der -in NAMEOFTHECERT.der
```

# What about .private/.val keys

Well, now its up to you to decrypt the keys you found.

They Are encrypted with an unknown private key from what ive seen, so good luck trying to be the first to decrypt them (or just decrypting one of them at all).

Its of to the races!!!
