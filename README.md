KeyBits v0.01b

- This software uses bitcoinj, json-simple, commons-cli, slf4j, bcpg, bcprov

- For further questions contact keybits@gmx.de using the gpg keyring fixed at address 1Pmbtsb5Wm2ivE1KTnRXtpkR5oRprUAccz

- Please DO NOT SEND COINS to this address

- Fixation of arbitrary information in the blockchain ALWAYS DESTROYS a fraction of bitcoins!!!

- Usage of KeyBits AT YOUR OWN RISK

- Usage:

(i) Getting help

```
john@skynet$ java -jar KeyBits.jar
This is KeyBits v0.01b

usage: java -jar KeyBits.jar [options]
 -a <string>      bitcoin address
 -b <file name>   return balance of wallet
 -c <file name>   create wallet
 -d <file name>   monitor transaction depths of wallet
 -e               export public key to blockchain
 -h               print this message
 -i <string>      import public key from blockchain
 -n <integer>     in combination with -c, -d, -r or -s
 -p <file name>   monitor pending transactions of wallet
 -r <file name>   reset wallet
 -s <file name>   send satoshis
 -u <file name>   update wallet
 -v               verbose
 -w <file name>   show content of wallet
```

(ii) Reading gpg keyring

```
john@skynet$ java -jar KeyBits.jar -i 1Pmbtsb5Wm2ivE1KTnRXtpkR5oRprUAccz
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: BCPG v1.51

mQINBFQ057MBEACycElHMjqjJeVVUFvnb8SA+Hc5SfLDNkPa0wNEMYU8WDpzAelH
GDZFDiEnEt/3DPN9OrQ8JCXw2AE7SX/I3IqrMnZnFlwbjmhG4usP3Pzp7sgyPnJJ
                   <many lines not shown>
zTzRzlec+8vMCXBVpbfPpmdQEVxhHVzhrsHH3lkJvL8LylJiGKPTsYZBimIzMtUz
91YB6cqbRu66VmEs0zyA8B2tQZpZRgSdNiPInrXn3sDSNF+w5Pj3
=zXH3
-----END PGP PUBLIC KEY BLOCK-----
```

(iii) Importing gpg keyring

```
john@skynet$ java -jar KeyBits.jar -i 1Pmbtsb5Wm2ivE1KTnRXtpkR5oRprUAccz | gpg --armor --import
```

(iv) Exporting gpg keyring

```
john@skynet$ gpg --armor --export <email@provider.com> | java -jar KeyBits.jar -e
```

This will export the gpg keyring associated with  the email address <email@provider.com>.
therefore, KeyBits creates  and/or updates  a new wallet associated  with this key which
will contain exactly one address. This wallet  will be encrypted by default, so the user
must choose and remember a password. Also the corresponding chain file is created and/or
updated.  Not the  total blockchain  needs to be  downloaded if the  checkpoint  file is
available. It  is then  checked, if the address  contains  enough  funds  to fix the gpg
keyring  into the  blockchain. If not, the user is asked to send the corrsponding amount
of  XBT to the single  address and the  program exits exists  immediately. Otherwise, if
there are enough founds, KeyBits will fix the keyring into the blockchain and wait until
the transaction is fixed in the blockchain with depth 1.

VERY IMPORTANT: YOU MUST KEEP THE WALLET FILE WHICH IS CREATED  DURING EXPORT AS WELL AS
THE CORRESPONDING PASSWORD!

This is  important, since a second  outgoing transaction marks the gpg keyring  as being
not trustworthy anymore.

(v) Sending coins

```
john@skynet$ java -jar KeyBits.jar -s <wallet file> -a <address> -n <# of satoshis>
```

The wallet files are named ```<something>.wallet``` and the chain files are named
```<something>.wallet.chain```. If you use the bitcoinj functionality, you might want to
suppress the error stream via

```
john@skynet$ java -jar KeyBits.jar -s <wallet file> -a <address> -n <# of satoshis> 2> error.stream
```

You then should check file ```error.stream``` for helpful information if something goes wrong.
