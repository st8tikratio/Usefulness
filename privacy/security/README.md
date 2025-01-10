# Table of Contents

## Cybersecurity
- [Cybersecurity Sessions](/privacy/security/cyber-security-sessions.md)

# GPG Key Import
- [Yubikey](https://developers.yubico.com/PGP/Importing_keys.html)
  - Pre-requiites
    - GnuPG version 2.0.22 or later 
    - YubiKey’s OpenPGP module must be 1.0.5 or later
      ```
      Insert your YubiKey

      gpg-connect-agent --hex "scd apdu 00 f1 00 00" /bye
      ```
```
Introduction
This is a short description of how to import an already existing PGP key to a YubiKey with PGP support.

Prerequisites
For this procedure to work you must have GnuPG version 2.0.22 or later installed on your computer. The version of the YubiKey’s OpenPGP module must be 1.0.5 or later. To check this version you may run, after inserting your YubiKey:

gpg-connect-agent --hex "scd apdu 00 f1 00 00" /bye
D[0000]  01 00 05 90 00                                     .....
OK
Where "01 00 05" means version 1.0.5.

If you have an existing key you want to import, that key must be a RSA 2048 bit key.

You’ll also need the YubiKey’s Admin PIN.

Generate a key
Skip this step if you already have a key.

gpg --gen-key

gpg (GnuPG) 2.0.22; Copyright (C) 2013 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
Your selection?
As there are key size and type limits depending on the type of your YubiKey, see the comparison page, we will select option 1, and go with the default of 2048 bits for the next question.

RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)

Requested keysize is 2048 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
Select an expiry date if you want to. And answer that the data is correct.

Real name:
Should be the real name associated with this key.

Email address:
Should be the email address associated with this key.

Comment:
May be a comment attached to the key if you want, or leave this empty.

You selected this USER-ID:
    "Foo Bar <foo@example.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit?
If you’re happy with this USER-ID answer O for okay.

We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: key 13AFCE85 marked as ultimately trusted
public and secret key created and signed.

gpg: checking the trustdb
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
gpg: depth: 0  valid:   4  signed:   8  trust: 0-, 0q, 0n, 0m, 0f, 4u
gpg: depth: 1  valid:   8  signed:   2  trust: 3-, 0q, 0n, 5m, 0f, 0u
gpg: next trustdb check due at 2014-03-23
pub   2048R/13AFCE85 2014-03-07 [expires: 2014-06-15]
      Key fingerprint = 743A 2D58 688A 9E9E B4FC  493F 70D1 D7A8 13AF CE85
uid                  Foo Bar <foo@example.com>
sub   2048R/D7421CDF 2014-03-07 [expires: 2014-06-15]
Take note of the id of the key, in this case 13AFCE85.

Add an authentication key
Here we will add an authentication key to the previously generated key.

gpg --expert --edit-key 13AFCE85

gpg (GnuPG) 2.0.22; Copyright (C) 2013 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/D7421CDF  created: 2014-03-07  expires: 2014-06-15  usage: E
[ultimate] (1). Foo Bar <foo@example.com>

gpg> addkey

2048-bit RSA key, ID 13AFCE85, created 2014-03-07

Please select what kind of key you want:
   (3) DSA (sign only)
   (4) RSA (sign only)
   (5) Elgamal (encrypt only)
   (6) RSA (encrypt only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
Your selection?
Here we select 8 to get another RSA key attached to our key.

Possible actions for a RSA key: Sign Encrypt Authenticate
Current allowed actions: Sign Encrypt

   (S) Toggle the sign capability
   (E) Toggle the encrypt capability
   (A) Toggle the authenticate capability
   (Q) Finished

Your selection?
Select A, then S, then E to get a pure authentication key. Then Q to continue.

RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)
Again we want a 2048 bit key.

Requested keysize is 2048 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0)
Select same expiry as for the rest of the key and then answer y.

Is this correct? (y/N) y
Really create? (y/N) y
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.

pub  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/D7421CDF  created: 2014-03-07  expires: 2014-06-15  usage: E
sub  2048R/B4000C55  created: 2014-03-07  expires: 2014-06-15  usage: A
[ultimate] (1). Foo Bar <foo@example.com>

gpg> Save changes? (y/N) y
Backup
This is a good point to create a backup of your key.

gpg --export-secret-key --armor 13AFCE85
Make sure to store the backup offline in a secure place.

Importing the key
Now it’s time to import the key into the YubiKey.

gpg --edit-key 13AFCE85

gpg (GnuPG) 2.0.22; Copyright (C) 2013 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Secret key is available.

pub  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15  usage: SC
                     trust: ultimate      validity: ultimate
sub  2048R/D7421CDF  created: 2014-03-07  expires: 2014-06-15  usage: E
sub  2048R/B4000C55  created: 2014-03-07  expires: 2014-06-15  usage: A
[ultimate] (1). Foo Bar <foo@example.com>

gpg> toggle

sec  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15
ssb  2048R/D7421CDF  created: 2014-03-07  expires: never
ssb  2048R/B4000C55  created: 2014-03-07  expires: never
(1)  Foo Bar <foo@example.com>

gpg> keytocard
Really move the primary key? (y/N) y
Signature key ....: [none]
Encryption key....: [none]
Authentication key: [none]

Please select where to store the key:
   (1) Signature key
   (3) Authentication key
Your selection? 1
Here we’ve just moved the primary key to the PGP Signature slot of the YubiKey.

gpg> key 1

sec  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15
                     card-no: 0000 00000001
ssb* 2048R/D7421CDF  created: 2014-03-07  expires: never
ssb  2048R/B4000C55  created: 2014-03-07  expires: never
(1)  Foo Bar <foo@example.com>

gpg> keytocard
Signature key ....: 743A 2D58 688A 9E9E B4FC  493F 70D1 D7A8 13AF CE85
Encryption key....: [none]
Authentication key: [none]

Please select where to store the key:
   (2) Encryption key
Your selection? 2
And here we’ve moved the Encryption key.

gpg> key 1

sec  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15
                     card-no: 0000 00000001
ssb  2048R/D7421CDF  created: 2014-03-07  expires: never
                     card-no: 0000 00000001
ssb  2048R/B4000C55  created: 2014-03-07  expires: never
(1)  Foo Bar <foo@example.com>

gpg> key 2

sec  2048R/13AFCE85  created: 2014-03-07  expires: 2014-06-15
                     card-no: 0000 00000001
ssb  2048R/D7421CDF  created: 2014-03-07  expires: never
                     card-no: 0000 00000001
ssb* 2048R/B4000C55  created: 2014-03-07  expires: never
(1)  Foo Bar <foo@example.com>

gpg> keytocard
Signature key ....: 743A 2D58 688A 9E9E B4FC  493F 70D1 D7A8 13AF CE85
Encryption key....: 8D17 89A0 5C2F B804 22E5  5C04 8A68 9CC0 D742 1CDF
Authentication key: [none]

Please select where to store the key:
   (3) Authentication key
Your selection? 3
And as a last step we’ve now moved the Authentication key to the YubiKey.

gpg> quit
Save changes? (y/N) y
After this the keyring is saved. And that point it no longer contains the real secret key, only a pointer indicating that it’s stored on a smart card.
```
