# (Service) Identity Handles


### Generation
Handles will be generated based on the public key.

Similar to how its done in https://github.com/marceldobehere/goofy-media-front/blob/master/src/lib/cryptoUtils.js


Some Basic Example Code for now (using CryptoJS) (stolen and slightly modified from Goofy Media)

This code will be optimized and available for to be done async in JS, using the window.crypto API, but thats not too important rn
```javascript
// publicKey in PEM Format with all \n \r and spaces removed
function userHashInternal(publicKey) {
    let words = getWordList();

    // The big root hash, based on the Public Key, takes long to compute
    let hash = newPbkdf2(str, "GoofyUserHash123", {keySize: 8, iterations: 1000000}).toString(enc.Base64);

    // The Word Count Hash -> Will be a number from 2 to 4 words
    let c = PBKDF2(hash, "GoofyUserLenHash123", {keySize: 16, iterations: 1234}).words[0];
    if (c < 0) c *= -1;
    c = 2 + c % 3;

    // Strength of handles
    // c = 2 -> ~44 bit (134611^2 * 1000)
    // c = 3 -> ~61 bit (134611^3 * 1000)
    // c = 4 -> ~78 bit (134611^4 * 1000)

    // The Last 1-3 digits 
    let n = PBKDF2(hash, "GoofyUserValHash123", {keySize: 16, iterations: 1234}).words[0];
    if (n < 0) n *= -1;
    n = n % 1000;
    let out = "";

    // The actual Words of the Handle
    for (let i = 0; i < c; i++) {
        let tHash = PBKDF2(hash, "GoofyWordHash123", {keySize: 16, iterations: 1234}).words[0];
        if (tHash < 0) tHash *= -1;
        tHash = tHash % words.length;
        out += words[tHash];
        if (i < c - 1)
            out += "_";

        // Modify the Hash every time to create a random chain
        hash = PBKDF2(hash, "GoofyNewUserHash123", {
            keySize: 16,
            iterations: 1234
        }).toString(CryptoJS.enc.Base64);
    }

    // Append the Numbers
    return out + n.toString(); // Example -> holts_plesh_boaty798
}
```

