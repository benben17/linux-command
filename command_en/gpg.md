gpg
===

A tool for signing, checking, encrypting, or decrypting data.

### Supported Algorithms:

Pubkey: `RSA`, `ELG`, `DSA`, `ECDH`, `ECDSA`, `EDDSA`
Cipher: `IDEA`, `3DES`, `CAST5`, `BLOWFISH`, `AES`, `AES192`, `AES256`, `TWOFISH`,
        `CAMELLIA128`, `CAMELLIA192`, `CAMELLIA256`
Hash: `SHA1`, `RIPEMD160`, `SHA256`, `SHA384`, `SHA512`, `SHA224`
Compression: `Uncompressed`, `ZIP`, `ZLIB`, `BZIP2`

### Syntax
```shell
gpg [options] [files...]
```

### Parameters:

```shell
 -s, --sign                  Sign
     --clear-sign            Make a clear text signature
 -b, --detach-sign           Make a detached signature
 -e, --encrypt               Encrypt data
 -c, --symmetric             Encrypt only with symmetric cipher
 -d, --decrypt               Decrypt data (default)
     --verify                Verify a signature
 -k, --list-keys             List keys
     --list-signatures       List keys and signatures
     --check-signatures      List and check key signatures
     --fingerprint           List keys and fingerprints
 -K, --list-secret-keys      List secret keys
     --generate-key          Generate a new key pair
     --quick-generate-key    Quickly generate a new key pair
     --quick-add-uid         Quickly add a new user ID
     --quick-revoke-uid      Quickly revoke a user ID
     --quick-set-expire      Quickly set a new expiration date
     --full-generate-key     Full featured key pair generation
     --generate-revocation   Generate a revocation certificate
     --delete-keys           Remove keys from the public keyring
     --delete-secret-keys    Remove keys from the secret keyring
     --quick-sign-key        Quickly sign a key
     --quick-lsign-key       Quickly sign a key locally
     --quick-revoke-sig      Quickly revoke a key signature
     --sign-key              Sign a key
     --lsign-key             Sign a key locally
     --edit-key              Sign or edit a key
     --change-passphrase     Change a passphrase
     --export                Export keys
     --send-keys             Export keys to a keyserver
     --receive-keys          Import keys from a keyserver
     --search-keys           Search for keys on a keyserver
     --refresh-keys          Update all keys from a keyserver
     --import                Import/merge keys
     --card-status           Print card status
     --edit-card             Change data on a card
     --change-pin            Change a card's PIN
     --update-trustdb        Update the trust database
     --print-md              Print message digests
     --server                Run in server mode
     --tofu-policy VALUE     Set the TOFU policy for a key
```

### Options:

```shell
 -a, --armor                 Create ASCII armored output
 -r, --recipient USER-ID     Encrypt for USER-ID
 -u, --local-user USER-ID    Use USER-ID to sign or decrypt
 -z N                        Set compression level to N (0 disables)
     --textmode              Use canonical text mode
 -o, --output FILE           Write output to FILE
 -v, --verbose               Verbose mode
 -n, --dry-run               Do not make any changes
 -i, --interactive           Prompt before overwriting
     --openpgp               Use strict OpenPGP behavior
```

### Examples:

```shell
 -se -r Bob [file]          Sign and encrypt for user Bob
 --clear-sign [file]        Make a clear text signature
 --detach-sign [file]       Make a detached signature
 --list-keys [names]        List keys
 --fingerprint [names]      Show fingerprints
```
