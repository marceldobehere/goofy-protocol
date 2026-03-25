# Goofy Protocol
A silly protocol / architecure spec to make goofy decentralized and federated systems kinda.


## Basic Outline

```
         ######           
         #User#           
       / ###### \         
      /          \        
  #####          #########
  #IDP# ──────── #Service#
  #####          #########
```


## Components
There are 3 big parts in the Goofy Protocol:

### Users
Normal people like you and me. (Could include bots) Users want to interact with services.

Services require a service identity and (most times) an associated IDP to register an account and to be used.

### IDP
A server which manages/provides identities to users and offers some storage for services.

Users can register a base identity on an IDP and then create service identities for the services they want to use. Each service identity has a unique handle which is used.

Often times services need to read/store data for a user, which the user can configure. Each user gets a specific amount of storage (depending on the IDP and registration) which can then be split amongst the services. 

Each service gettings its own "Mini Database" which should be end to end encrypted. (Split into text data and binaries)

### Services

Services are the actual things that we use to do things. 

They can be anything, from simple chat apps, mailing systems, a shared canvas or even social media networks. All they do is allow users to interact with some kind of system (and usually with other users too).

Services can be singular centralized things or federalized and decentralized instances spread out through the whole internet.

Services can store data in their own places, but they can also store user data at the IDP Servers of the respective users.


Ideally, services have a open-source and statically hosted Frontend/Client application to use it. And that Frontend should be compatible with all instances of the service running.

This is important because to use services, you need to use your service identity keypair and malicious clients could steal it and compromise that service identity keypair, especially if used for multiple services. 


## Simplified Example Processes

### Registering a Base identity
You find a cool IDP Provider and you want to register there.

First you'll go to their page and follow the instructions. These can be different but for an example:
* You enter an email and get sent a registration code
* On the webpage (or elsewhere) you create a secret keypair
  * This keypair also "creates" a handle which is linked to it
  * You save a backup of your keypair locally
  * Do not share it with anywhere and dont use an IDP you dont trust!
* You register using some sort of credentials and the registration code
  * The credentials can be email/username & password
  * It could also be your public key / handle and private key
  * It could even be a token you need to sign locally
  * It depends on the webpage
* You're done, you have a base identity at an IDP now!

Now you can manage your identities and join services!


### Creating a Service Identity
In your IDP Website, you can create Service Identities. 

They basically just consist of a keypair and handle and offer you settings to configure for the services.

A Service Identity can be used for several services. This is useful if you want to have the same handle on several services. But only do this, if you trust the services and the pages/clients you use!

You can now configure access and size constraints for the services you will join/use.

### Joining a Service
When you want to register for a service you can visit their page (or a page of one of the instances you like / would like to join).

If you have not set up access for the service in your IDP, it might redirect you to your IDP or ask you to create an entry with some settings. Please read the settings carefully and only apply them if you understand what its doing and why.

Once you have set up access it will probably ask you to register with a code or something. Depending on the service, you might need to ask someone, enter some contact information, do a captcha or something else.

Once you have a register code you can register using your service identity. Either you get redirected to your IDP or you have to look up and enter your service identity keypair.

Now you successfully joined a service.


### Login to a Service

If you want to login to a service, you can visit it and it can either redirect you to your IDP and you can sign in from there or you might enter your service identity keypair manually and login that way.

Now you have logged in and can use the service!


## Definitions

### IDP
A

### Base Identity
A

### Service Identity
A

### Account
A

### Handle
A




## Structures
A

### Handle
A

### Identity
A





## Other things

### Handle generation
More Info [here](./handles.md).

### Crypto Details


### Migrating an IDP

