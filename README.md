# Goofy Protocol (WIP)
A silly protocol / architecure spec to make goofy decentralized and federated systems kinda.

## Notes
This is still very WIP.

Currently I am working on this outline and the IDP Specs.

I will then write the basic specs for services and also work on the code examples (which are all empty rn)

Once all that is done ill try to write somewhat detailed specs for Goofy Chat 3 and Goofy Media 2.

And once I got some actual code I will link the repositories and host some instances with the stuff so its actually usable!

But this all will take quite a while. (Writing the specs and outline alone takes ages)

# Table of Contents
- [Goofy Protocol (WIP)](#goofy-protocol-wip)
  - [Notes](#notes)
- [Table of Contents](#table-of-contents)
  - [Basic Outline](#basic-outline)
  - [Components](#components)
    - [Users](#users)
    - [IDP](#idp)
    - [Services](#services)
  - [Simplified Example Processes](#simplified-example-processes)
    - [Registering a Base identity](#registering-a-base-identity)
    - [Creating a Service Identity](#creating-a-service-identity)
    - [Joining a Service](#joining-a-service)
    - [Login to a Service](#login-to-a-service)
  - [Definitions](#definitions)
    - [IDP](#idp-1)
    - [Base Identity](#base-identity)
    - [Service Identity](#service-identity)
    - [Account](#account)
    - [Handle](#handle)
  - [Structures](#structures)
    - [Handle](#handle-1)
    - [Identity](#identity)
  - [Other things](#other-things)
    - [Handle generation](#handle-generation)
    - [Crypto Details](#crypto-details)
    - [Migrating an IDP](#migrating-an-idp)
  - [Component Specs](#component-specs)
  - [Example Service Specs](#example-service-specs)
  - [Implementation Examples](#implementation-examples)
- [Notes from Phone (copied)](#notes-from-phone-copied)



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

Services can store data in their own places, but they can also store user data at the IDP Servers of the respective users. When storing data on the IDP it should be encrypted to avoid tampering by the user or IDP administrator, unless the data is not important. Please consider that data can be viewed modified or deleted by the user / admins, so the service should always check the validity!

Services have a handle and cryptographic keypair for authentication with the IDP.

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
A string that is tied to a publickey / keypair of an identity.

The handle can be used to identify a user and to retrieve the public key of from one, to verify signatures.

Handles have the following format:

`[word]_[word]_[word]_[word][value between 0 and 999]`

There can be 2-4 words in a handle separated by underscores.

An example would be `holts_plesh_boaty798`


Normally handles do/should not require a domain (with certain exceptions like newly registering, migrating, etc.). If they do have a domain tied it will have this format:

`handle@domain.tld` / `[word]_[word]_[word]_[word][value between 0 and 999]@[domain]`


Handles are tied to a public key and unique, which means that a handle (basically) always points to a singular identity which is nice, because that means the identity isnt really tied to an IDP / domain. 


## Structures
A

### Handle
A

### Identity
A





## Other things

### Handle generation
More Info [here](./details/handles.md).

### Crypto Details


### Migrating an IDP


## Component Specs

* [IDP Specs](./specs/idp.md)
* [Minimum Service Specs](./specs/min_services.md)
* [User related Specs](./specs/user_stuff.md)



## Example Service Specs

* [Goofy Chat (v3)](./services/goofy_chat.md) A decentralized E2EE Chat App
* [Goofy Media (v2)](./services/goofy_media.md) A decentralized & secure text-based Social Media


## Implementation Examples
Examples for important parts can be found [here](./code_examples/java/). They will mainly be in Java for now, later also Javascript with corresponding Libraries/APIs.







# Notes from Phone (copied)

IDPs should have some default endpoint
* `/info` that shows the version and that it is infact an IDP server
* `/contact` which has information to contact the administrators of the thing
* `/report` to report any kind of problematic content or issues


IDP allow checking if a handle belongs to the IDP


Services should have some default endpoint
* `/info` that shows the version and that it is infact a service and what kind
* `/identity` which shows the public key / handle of the service
* `/contact` which has information to contact the administrators of the thing
* `/report` to report any kind of problematic content

Size Constraints.

Open question about what requirements there are regarding DSGVO


Make Services able to automatically allow all accounts from an IDP?


25.3 screenshots 


Idp per handle public dictionary of services and domains "goofy media: "https://...", mqybe api to edit this so u can add ut easily 


API for idp storage ahve warmings and errors whwn storage quota high/exceeded 

Global api for idp, services to update information for handle (eg when mpving)
post /uödate-handle-info -> new domain, etc, 

Idpmstorage several maps with string keys and string results, ideally AES encrypted
Maybe a signature field for each entry or for the global table state? (Or maybe not, idk)
Simple queries but what about fields?
Think abt what would be useful for goofy media and chat and ordering/sorting 


global registry where u can enter a handle and u get the public key and most recent server location + maybe services? 

Moderation so admins can deletr media that is not supposed to be there and delete users and change quotas etc 