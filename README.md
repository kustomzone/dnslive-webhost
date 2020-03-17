# dnslive webhosting
## Quick and simple web hosting for your Handshake Naming System Top Level Domain Zone
Simply provide a signature of the file you wish to upload signed by the address associated with the domain/tld.


### Install
```
git clone https://github.com/realrasengan/dnslive-webhost
cd dnslive-webhost
npm install request
```

### Use
```
node dnslive-webhost.js domain publichtml/path/to/file signature-of-file
```

### Example of full commands to get up and going (assumes [Bob Wallet by Kyokan](https://github.com/kyokan/bob-wallet))
1. Copy the address that owns the domain to a temporary textfile/notepad.
2. Get your API key from Bob Wallet  (Settings -> copy HSD API Key to a temporary textfile/notepad)
3. Download hs-client
```
git clone https://github.com/handshake-org/hs-client
```
4. Once downloaded, type
```
cd hs-client
npm install --production
```
5. Then, type:
```
cd bin
```
6. Type this in to select the proper wallet in Bob.
```
./hsw-rpc selectwallet allison --api-key=APIKEY_FROM_HSD
```
7. Type this command and save the signature result -- you'll need it for the final update, it is a signature.  Note: The below signmessage command is currently not working, but a PR has been submitted to hsd [PR 393, hsd](https://github.com/handshake-org/hsd/pull/393).  Advanced users can use the `hsd-rpc signmessagewithprivkey` function after getting the associated private key with `./hsw-cli dump`.  Everyone else, I apologize, but its best to wait until the fix is merged to avoid risking your private key.
```
./hsw-rpc signmessage ADDRESS_THAT_OWNS_DOMAIN `node /path/to/dnslive-webhost/dnslive-filetobase64.js publichtml/path/to/file` --api-key=<API KEY from step 2>
```
8. Go to the /path/to/dnslive-webhost directory
```
node dnslive-webhost.js <domain> <publichtml/path/to/file> <signature from step 7>
```
9. Done.

### A more straight forward example
#### Assumes you have 2 folders at the same level, hs-client and dnslive-webhost (i.e., installed them in same folder):
```
cd hs-client/bin
./hsw-rpc selectwallet allison --api-key=APIKEY_FROM_HSD
./hsw-rpc signmessage ADDRESS_THAT_OWNS_DOMAIN `node ../../dnslive-webhost/dnslive-filetobase64.js publichtml/path/to/file` --api-key=APIKEY_FROM_HSD
```
> SIGNATUREOUTPUT
```
cd ../../dnslive-webhost
node dnslive-webhost.js DOMAIN publichtml/PATH/TO/FILE SIGNATUREOUTPUT
```

### Copyright
Copyright (c) 2020 The Handshake Community

MIT Licensed.

