# Goofy Chat (v3) (WIP)
A spec / architecture on how Goofy Chat will work using the Goofy Protocol















## Concept for simplified Forward Secure Key Agreement / X3DH / Double Ratchet

This is a simplified concept that removes the need for pre signed keys or limited one time presigned keys but in turn flips the encryption order / blocks sending messages until both parties are online at least once. (Which for a chat app should be fine, a user would need to send something like a friend/chat request first before a chat is started and it needs to be accepted, which already satisfies the condition)

In a simple scenario we have two parties, Bob and Alice and Bob wants to start an encrypted conversation with Alice. Bob and Alice both know or can derive each others public key.

(**NOTE**: Beware of Out-of-order messages)

### Start

Before starting the new chat, Bob generates a random, short-lived Keypair. (This will be used exactly once to decrypt a future message and can then be deleted after)

### Bob requests a Chat

Bob can then send Alice a chat request message and include the temporary/random public key. This message will be encrypted using Alices (Identity) Public Key. It may also contain a request message text, which does not have forward secrecy guarantees.

At this point Bob cannot send Alice any more (secure) messages yet, and needs to await the response.

### Alice receives the Request

At some point Alice will find the message, decrypt it with the private key and then decide to accept or deny the request. In this example the request will be accepted.

Now Alice will generate a secret, which will be used to symmetrically encrypt messages from Alice to Bob. (This should be used as the base for a symmetric ratchet and it is only one-way = Alice -> Bob)

Additionally, Alice will generate a random, short-lived Keypair (Just like Bob did, this will be used for the other way)

This symmetric secret and Alices random/temporary public key will then be encrypted with the temporary public key of Bob and sent to Bob in a "accept request" / "set secret" message.

At this point Alice can now freely send Bob messages.

### Bob receives the Accepted Request

At some point Bob will receive this "set secret" / "accept request" message and store the secret / use it for the symmetric ratchet (Alice -> Bob). Bob can now receive messages from Alice securely.

Now Bob will generate a secret, which will be used to symmetrically encrypt messages from Bob to Alice. (This should be used as the base for the other way symmetric ratchet).

This symmetric secret will then be encrypted using the temporary public key from Alice and send to Alice in a "set secret" message.

At this point Bob can now freely send Alice messages.

### Alice receives the "set secret" message

At some point Alice will receive this "set secret" message and store the secret / use it for the symmetric ratchet (Bob -> Alice)

Now Alice can decrypt messages sent by Bob and both parties can securely communicate with each other.

### Ensuring Forward Secrecy

To ensure forward secrecy, both parties should regularly request the other party to update their symmetric secret / ratchet, by sending some kind of "request new secret" message in regular intervals. 

The process will be identical to the method described above and ensures that if a private identity key gets compromised, all past messages using previous ratchets / secrets are unaffected.

Do note that the sender "cannot" not update their own sending ratchet (unless the agreement is changed) but only request the other party to update theirs. 

This also means that the sender does not need to worry about using outdated secrets or waiting for confirmations or needing a pool of presigned one time keys constantly available.

This key exchange / ratchet can be implemented easily using existing code / public key infrastructure provided by the goofy protocol and already is quantum resistant due to the support of ML-KEM / ML-DSA.


# Notes from Phone (copied)
If the Goofy Chat 3 Server doesnt need to manage users and groups and messages it can get quite simple.

It will still need to store messages on the IDP, or rather it would be good because the server wouldnt really need a message queue then (unless the IDP is down ig but idk if the server will keep it), the server can just have a table in the idp that stores the new messages which have not been processed by the client yet

look into message processing with several clients at once, either some form of locking for the tables or clients or assigning a client to be the primary to actually write data and the others just to read and get events using websockets?



Dont just write server specs but also client specs for
* messages / types
* media handling
* user info
* group chats
* example for how to store messages (maybe using IDP)
* more


User - goofy chat service - idp ? Or user access idp directly so no need to rely on service? Would be goofy thoigh bc clients for idp dataset so idk 


dgsvo zeugs? 

When u send afike in goofy vhst it gets uplpaded to ur idp and u bascially send s link to an unlisted fownload of it + kexs

API for idp storage ahve warmings and errors whwn storage quota high/exceeded 





Moderation so admins can deletr media that is not supposed to be there and delete users and change quotas etc 

Report api endpoibts for idp + services 

Treat file uploads differently?
Store chat messages?


Look into Backwards and Forwards Secrecy

Maybe look into signal sealed-sender messages? Not sure if i can do that easily with my architecture without allowing spam 


Maybe mitm chwck by standardizes OTP emojis (mix of matrix emojo verification and otp codes which u can always see/check and yes) 
