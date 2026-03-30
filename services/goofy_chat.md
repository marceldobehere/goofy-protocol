# Goofy Chat (v3) (WIP)
A spec / architecture on how Goofy Chat will work using the Goofy Protocol














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