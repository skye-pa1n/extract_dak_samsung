# Extract DAK from any 2020 Samsung Device
This guide will teach you on how to extract the Device Attestation Keys from your 2020 Samsung Device.

# Requirements:
You must be on a rooted device.

You must have a working brain (optional).

You need to have termux installed.

This was tested on a Galaxy S20FE (2020 Samsung device), but theoretically any Samsung device with a EFS partition should be able to it.

# **Notes**

You **need** to be rooted.

This guide **WILL NOT** guide you on how to decrypt the EC & RSA keys. (They are prob encrypted to industry standart.) (Or them may be encrypted by a private key inside the BL/EDL, idk.)

# **How-to**

Run this command on termux as root to move your efs partition to your internal memory.
```
dd if=/dev/block/bootdevice/by-name/efs of=/sdcard/efs.img
```

Extract the file located at /sdcard/efs.img with ZArchiver.

You will have a folder called efs, enter it, you will have a folder called DAK(Device attestation Keys) and inside this folder you will have:


GAK_EC.private

GAK_EC.val

GAK_RSA.private

GAK_RSA.val

gakeccert.0.der

gakeccert.1.der

gakeccert.2.der

And some other SAK (Samsung attestation keys) & SGAK Keys.

# *"Decrypt"* .der files (Certificates) (They aren't even encrypted, they are as-is)
Run this on termux at the directory the .der files are at
```
openssl x509 -noout -text -inform der -in NAMEOFTHECERT.der
```

# What about .private/.val keys

Well, now its up to you to decrypt the keys you found (or no).

They Are encrypted with an unknown private key from what ive seen, so good luck trying to be the first to decrypt them (or just decrypting one of them at all).

Now its of to the races!!!

## Proofs
# This is how one of the **Google** (GAK) .der certificates from the S20FE looks alike.

```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            bc:39:35:3a:ca:bb:9a:97:42:c1:28:5a:57:20:9a:ee
        Signature Algorithm: ecdsa-with-SHA256
        Issuer: title=TEE, serialNumber=d2015920be6e5b8c34301ea0e3641131
        Validity
            Not Before: Jan 13 21:08:54 2021 GMT
            Not After : Jan 11 21:08:54 2031 GMT
        Subject: title=TEE, serialNumber=22314d9fc6a15bfca55a6f7f58022ae2
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (256 bit)
                pub:
                    04:37:7a:12:18:ee:55:14:47:d8:0f:cc:66:3c:55:
                    98:21:03:ae:e9:ba:f8:e1:64:ae:c8:0b:59:17:87:
                    1b:80:7a:cb:5d:a0:56:81:9c:a8:84:d8:a6:75:44:
                    19:aa:04:93:f4:c8:fc:06:44:c3:cb:47:f4:dd:25:
                    42:dc:1c:c3:10
                ASN1 OID: prime256v1
                NIST CURVE: P-256
        X509v3 extensions:
            X509v3 Subject Key Identifier:
                96:69:43:06:A2:0D:65:AA:12:C9:D6:F7:09:7D:F5:25:81:16:8C:48
            X509v3 Authority Key Identifier:
                C9:54:37:EE:46:86:54:0D:51:71:DA:59:04:C0:27:EF:C2:D6:13:25
            X509v3 Basic Constraints: critical
                CA:TRUE
            X509v3 Key Usage: critical
                Certificate Sign
    Signature Algorithm: ecdsa-with-SHA256
    Signature Value:
        30:65:02:30:31:9d:e9:c2:7b:09:26:47:09:6d:10:6c:02:d3:
        6d:12:d1:ee:80:ce:18:e2:94:13:d7:93:70:06:17:b4:dc:f9:
        c9:c0:bc:4c:bb:1c:ba:22:31:7f:22:a9:9d:7a:57:ca:02:31:
        00:84:34:80:80:cb:68:55:1a:88:c5:7d:5a:51:77:c2:34:c4:
        84:4c:5d:a9:31:56:f8:7a:3c:26:99:eb:fc:c0:85:3d:d1:5c:
        c1:a3:e5:f2:aa:cc:07:e4:0d:8b:19:94:70
```


# How does one of the **Samsung** .der (SAK) Certificates from the S20FE looks alike?

```
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number: 1644359894 (0x6202f0d6)
        Signature Algorithm: ecdsa-with-SHA384
        Issuer: C=KR, L=Suwon city, OU=Samsung Mobile, CN=Samsung corporation
        Validity
            Not Before: Feb  8 22:38:14 2022 GMT
            Not After : Feb  3 22:38:14 2042 GMT
        Subject: C=BR, L=SEDAC, O=Samsung Electronics Co. Ltd, OU=Mobile Communications Division, CN=oity6xt3Q84prQA1bzuw1rJcmycNYYRuawn31PwxtYQ=, DC=SM-G780G, UID=SAK_V2:20220208193751:811:AdTJyFBOD_0bjX1lwDpENuWYFYZtu-19-ZUyquz8zfw=:oity6xt3Q84prQA1bzuw1rJcmycNYYRuawn31PwxtYQ=
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (384 bit)
                pub:
                    04:ff:c7:41:1c:49:2d:6f:50:5a:98:4a:a5:b5:80:
                    a2:0a:ae:26:49:30:5c:e4:da:d2:17:49:90:18:c4:
                    ff:0b:34:28:7c:d4:4c:6d:3a:d6:5f:49:56:ee:f6:
                    7e:c5:b9:4a:95:65:80:6a:a5:95:13:75:e6:83:6e:
                    6b:58:d7:17:88:1a:c4:64:59:61:7f:df:56:b9:8f:
                    79:b9:aa:55:e3:3e:6e:fd:cb:6d:0f:28:2a:36:07:
                    9c:2f:14:f4:8e:1f:81
                ASN1 OID: secp384r1
                NIST CURVE: P-384
        X509v3 extensions:
            X509v3 Basic Constraints: critical
                CA:TRUE, pathlen:0
            X509v3 Key Usage: critical
                Certificate Sign, CRL Sign
            X509v3 Subject Key Identifier:
                44:9B:6E:78:EB:A4:8B:AD:C3:87:84:E3:82:89:42:75:22:F6:3D:3E
            X509v3 Authority Key Identifier:
                66:EC:4E:7F:84:09:F4:C0:2A:56:12:90:83:FE:86:40:34:D5:2E:FF
            Authority Information Access:
                OCSP - URI:http://ocsp.samsung.com/security/
            X509v3 CRL Distribution Points:
                Full Name:
                  URI:http://crl.samsung.com/security/rdevices.crl
    Signature Algorithm: ecdsa-with-SHA384
    Signature Value:
        30:81:87:02:42:01:49:98:48:63:92:da:f2:91:23:fb:03:a6:
        f2:6e:ce:84:76:7c:65:6f:36:b3:36:ba:b0:26:f0:eb:40:15:
        2f:35:50:5c:f0:32:26:bb:44:c9:32:78:6c:09:87:3d:35:89:
        59:47:46:33:cb:ee:00:8f:5e:44:ca:b9:02:26:12:f8:89:02:
        41:25:4f:eb:dd:33:45:86:80:61:38:d6:09:fe:99:57:4f:be:
        a2:c5:72:68:66:10:9f:b6:54:d0:48:ac:fb:9c:f4:ea:37:55:
        05:ff:9b:18:cc:1b:e2:7a:a6:a9:1a:a6:11:49:2d:a2:1c:67:
        88:be:84:92:24:47:98:6e:ee:ea:58:f6
```

# License
This project is licensed under the GPLv2.
