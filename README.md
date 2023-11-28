Vaultzy
==========

![vaultzy_icon](https://github.com/AzzyB/Vaultzy/blob/main/favicon.png)

## What is Vaultzy?

* Vaultzy is client-side file encryption web app forked from Hypervault.
* Vaultzy is entirely contained in a single, static `.html` file.
    - As such, you can save the Vaultzy page, and you will have a complete working copy of Vaultzy which you can run offline.
    - Vaultzy has no server-side components.
* Vaultzy outputs another single `.html` file which contains both the encrypted file data, and a copy of itself.

## Features

* Vaultzy uses the `HTML5 File API` to read file data into the browser client-side.
* It then stores all the filenames, file types, file sizes, and file data (as `base64`) in a `JSON` object.
* The user enters a Vault password and clicks `Lock vault`; Vaultzy builds a locked vault like this:
    - Vaultzy serializes the `JSON` blob containing all the file data, and encrypts it using the [triplesec](https://github.com/keybase/triplesec) encryption library. The output of this is a single string.
    - Vaultzy then grabs it's own source code (without making any web requests), and treats it as a template with which it interpolates the encrypted file data by replacing the `REPLACE_WITH_ENCRYPTED_DATA_`.
    - Vaultzy also sets a variable in the new vault to indicate that this is a locked vault: `_decryptionMode = true;`.
    - Vaultzy then initiates a download of the new `locked_vault.html`.

* Secure
    - Vaultzy uses the Triplesec library, which uses 3 strong encryption algorithms ([AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), [Salsa20](https://en.wikipedia.org/wiki/Salsa20), and [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher))).
    - Since Vaultzy runs sandboxed in a browser, you never have to worry that it doing anything on your computer outside of what it's designed to do.
    - Zero-knowledge: Vaultzy encryption is all client-side only.
* Easy
    - No installations necessary, just run in the browser.
* Offline
    - Since Vaultzy is a self-contained `.html` file, you save it to your desktop and run it offline.
* Always usable
    - Since Vaultzy packages itself with your encrypted data (in the form of a `locked_vault.html` file, you can always decrypt your data, even if Vaultzy goes away.

