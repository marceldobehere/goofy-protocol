# General Things that are important


## Signature Based Requests

Most requests to a service or idp should be secured using signature based requests.

This means that each request should be signed using the identity keypair.


The following headers should be added to authenticated requests:

```js
// body is a JSON Object or raw binary data, null should be turned into {}

let id = getRandomIntInclusive(10000000, 10000000000); // random ID
let validUntil = Date.now() + 1000 * 30; // Usually now + 30s
let signature = signObj({body, id, validUntil}); // More Details somewhere else

// TODO: signature should also include method, and path

// -> Headers to add: 

'X-Goofy-Signature': encodeURIComponent(signature),
'X-Goofy-Id': id,
'X-Goofy-Valid-Until': validUntil,
'X-Goofy-Public-Key': encodeURIComponent(publicKey), // PEM format
'X-Goofy-RAW': false, // set to true if the content is not json
'Content-Type': 'application/json', // set to something else if needed
```

The Body should either be the raw data or a stringified version of the JSON Object.


The server should then always check the validity of the signature + data before processing it. Ideally also checking if the userId/handle based on the public key is authorized to perform an activity.

