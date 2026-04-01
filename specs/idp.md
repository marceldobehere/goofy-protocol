# Minimal Specs for a valid IDP
These are the minimal specs for a valid IDP.

These are still very WIP.


# Table of Contents
- [Minimal Specs for a valid IDP](#minimal-specs-for-a-valid-idp)
- [Table of Contents](#table-of-contents)
- [Specs](#specs)
  - [API](#api)
    - [General](#general)
      - [Info](#info)
      - [Contact](#contact)
      - [Report](#report)
      - [A](#a)
    - [Verification / User Lookup](#verification--user-lookup)
      - [Handle Lookup](#handle-lookup)
      - [A](#a-1)
    - [Registration (Base Identity / Account)](#registration-base-identity--account)
      - [Check Registrations Allowed](#check-registrations-allowed)
      - [Contact](#contact-1)
      - [Create Registration](#create-registration)
    - [Login/Check (Base Identity / Account)](#logincheck-base-identity--account)
      - [Get User Info](#get-user-info)
    - [Encrypted Password/Keypair Storage (Base Identity / Account)](#encrypted-passwordkeypair-storage-base-identity--account)
      - [Get Storage Entry for Username](#get-storage-entry-for-username)
      - [Post Storage Entry for Username](#post-storage-entry-for-username)
    - [Encrypted (Service) Identity Storage](#encrypted-service-identity-storage)
      - [Get All Identities](#get-all-identities)
      - [Get Specific Identity](#get-specific-identity)
      - [Create/Store/Update Identity](#createstoreupdate-identity)
    - [Global Handle Information](#global-handle-information)
      - [Get Public Data](#get-public-data)
      - [Post Public Data](#post-public-data)
      - [Get Private Data](#get-private-data)
      - [Post Private Data](#post-private-data)
    - [Service Entry Configuration](#service-entry-configuration)
      - [Get Service Entries for Handle](#get-service-entries-for-handle)
      - [Get Service Entry Details](#get-service-entry-details)
      - [Create Service Entry](#create-service-entry)
      - [Update Service Entry](#update-service-entry)
      - [Delete Service Entry](#delete-service-entry)
    - [Service Storage Configuration](#service-storage-configuration)
      - [A](#a-2)
    - [Service Access](#service-access)
      - [(REDIRECT) Add Service Access to Handle](#redirect-add-service-access-to-handle)
      - [(REDIRECT) Get Service Login Credentials / Keypair](#redirect-get-service-login-credentials--keypair)
    - [Service Table Access](#service-table-access)
      - [Get Tables](#get-tables)
      - [Get Tables Quota](#get-tables-quota)
      - [Get Table](#get-table)
      - [Create Table](#create-table)
      - [Delete Table](#delete-table)
      - [Locking a Table](#locking-a-table)
      - [Unlocking a Table](#unlocking-a-table)
      - [Get Table Entries](#get-table-entries)
      - [Add Table Entry](#add-table-entry)
      - [Update Table Entry](#update-table-entry)
      - [Get Table Entry](#get-table-entry)
      - [Delete Table Entry](#delete-table-entry)
      - [Query Table Entries](#query-table-entries)
    - [Service Bucket Access](#service-bucket-access)
      - [Get Buckets](#get-buckets)
      - [Get Buckets Quota](#get-buckets-quota)
      - [Get Bucket](#get-bucket)
      - [Create Bucket](#create-bucket)
      - [Delete Bucket](#delete-bucket)
      - [Get Entries for Bucket](#get-entries-for-bucket)
      - [Add Entry to Bucket](#add-entry-to-bucket)
      - [Get Entry Info from Bucket](#get-entry-info-from-bucket)
      - [Get Entry from Bucket](#get-entry-from-bucket)
      - [Delete Entry from Bucket](#delete-entry-from-bucket)
    - [DSGVO and such](#dsgvo-and-such)
      - [Get Complete Account Export](#get-complete-account-export)
      - [Delete Account and all Data](#delete-account-and-all-data)
      - [Deactive Handle or so](#deactive-handle-or-so)
      - [Move Handle to different IDP or so](#move-handle-to-different-idp-or-so)
      - [Import Export of different IDP?](#import-export-of-different-idp)
    - [Account Information](#account-information)
      - [Get Storage Details](#get-storage-details)
      - [Get Storage Quotas](#get-storage-quotas)
      - [A](#a-3)
  - [Admin API](#admin-api)
    - [General](#general-1)
      - [Get Contact Requests](#get-contact-requests)
      - [Update Contact Request](#update-contact-request)
      - [Delete Contact Request](#delete-contact-request)
      - [Get Report Requests](#get-report-requests)
      - [Update Report Request](#update-report-request)
      - [Delete Report Request](#delete-report-request)
      - [Set Public IDP Instance Info Data](#set-public-idp-instance-info-data)
    - [Registration Management](#registration-management)
      - [View Registration Codes](#view-registration-codes)
      - [Create Registration Code](#create-registration-code)
      - [Delete Registration Code](#delete-registration-code)
      - [Set Registrations Allowed](#set-registrations-allowed)
      - [Get Registration Code Requests](#get-registration-code-requests)
      - [Update Registration Code Request](#update-registration-code-request)
      - [Delete Registration Code Request](#delete-registration-code-request)
    - [User Management](#user-management)
      - [A](#a-4)
    - [Encrypted Password/Keypair Storage Management](#encrypted-passwordkeypair-storage-management)
      - [A](#a-5)
    - [User Service Management](#user-service-management)
      - [A](#a-6)
    - [User Service Table Management](#user-service-table-management)
      - [A](#a-7)
    - [User Service Bucket Management](#user-service-bucket-management)
      - [A](#a-8)
    - [User Storage Quota Management](#user-storage-quota-management)
      - [B](#b)
    - [Service Management](#service-management)
      - [B](#b-1)
    - [Stats](#stats)
      - [B](#b-2)
    - [Backup](#backup)
      - [Export Full Backup](#export-full-backup)
      - [Import Full Backup](#import-full-backup)
  - [Potential for future improvement](#potential-for-future-improvement)



# Specs



## API

### General

#### Info

#### Contact
These can be used publically but can also be signed by a user.

#### Report
These can be used publically but can also be signed by a user.

#### A


### Verification / User Lookup

#### Handle Lookup
Looking up the base / service identity using the handle and getting some basic information back. (Handle, Public Key, which IDP server it is on, etc,)

#### A


### Registration (Base Identity / Account)

#### Check Registrations Allowed
Checks if the IDP even allows registrations currently

#### Contact
A way to contact if you want a register code. If register codes are automatically sent by email or something, this can be optional. 

#### Create Registration
This endpoint is used to create a new account. It should be a signed request using the generated keypair and include the public key and handle of the registering user. It should also include the registration code/token/key/etc.

### Login/Check (Base Identity / Account)

#### Get User Info
This signed request will return info about the user who sent it. This can be used to check whether the signing works, if the user is authenticated and if the user is an administrator.


### Encrypted Password/Keypair Storage (Base Identity / Account)
Endpoints for storing encrypted keypairs, which are used for password based login.

Each registered user can have one entry with a chosen username (if available) and can store text data in it. The entry can be looked up publically with the username as the key.

The username will never be sent in plaintext, it will be hashed beforehand so that the IDP does not know the username and only the user knows it. (As an additional layer of security)

It's intended for users to symmetrically encrypt their keypair with a password and store that in this storage. (If want to store it conveniently)

The Entry should have a normal size constraint, maybe max 100KB.

#### Get Storage Entry for Username

#### Post Storage Entry for Username


### Encrypted (Service) Identity Storage
Endpoints for storing and retrieving generated Identities. They will be stored encrypted

The Entries are symmetrically encrypted with a key.
This key is stored alongside the entry but it is asymmetrically encrypted with the public key of the base identity, meaning only the user can decrypt/use them. 

The identity entries should have the handle and a custom name added to them which doesnt need to be encrypted and a string for notes which should be encrypted. 

The Entries should have a normal size constraint, maybe max 100KB. There should also be a maximum number of encrypted identities, but that depends on the IDP, I would say at minimum 20 should be good.

#### Get All Identities

#### Get Specific Identity

#### Create/Store/Update Identity




### Global Handle Information
For each identity the user has, they can set global public and private data.
This data is basically just a JSON Object with keys and values.


Public Data for example should include a `services` key which has an object with service names and the urls of the service instance the handle is used on. This can be useful if you use the same handle for several services and want others to find the instances.


#### Get Public Data

#### Post Public Data


#### Get Private Data

#### Post Private Data


### Service Entry Configuration
Creating an entry which contains tables and buckets that can be accessed by a service using a handle. This should also support multiple handles having access to an entry. Should be differentiated between read-only and read/write.

#### Get Service Entries for Handle

#### Get Service Entry Details

#### Create Service Entry

#### Update Service Entry
Set Quotas for Storage and maybe Table count
Two distinct quotas, binary content and table data!
Also updating access levels per handle

#### Delete Service Entry






### Service Storage Configuration
Being able to list, view and modify the tables / data inside.
Two distinct quotas, binary content and table data!

How much storage can be used / is used, and how many tables can be created / have been created. Also how many columns/rows a table can have.

Also being able to set the visibility of data (either private or public or select services maybe?)

#### A





### Service Access
These Endpoints get used by services 

#### (REDIRECT) Add Service Access to Handle
This should be a URL that services can link users to which should redirect users to a (ideally) Frontend Page of the IDP where a logged in user can add the service (defined in the query parameter) to a handle.

This is there to make the userflow easier.


#### (REDIRECT) Get Service Login Credentials / Keypair
This should be a URL that services can link users to which should redirect users to a (ideally) Frontend Page of the IDP where a logged in user can get all handles associated with the service (defined in the query parameter) and can get the keypair which can be used to log in.

It could potentially add a link to the service which would get the credentials in the url (ideally encoded inside the fragment `#` portion for security reasons) so that the user can get signed in by just selecting the handle and getting redirected to the specific service url. 

This is there to make the userflow easier.


### Service Table Access
These Endpoints get used by services to access the tables.


#### Get Tables

#### Get Tables Quota
How much storage can be used / is used, and how many tables can be created / have been created. Also how many columns/rows a table can have.

#### Get Table
Column Definitions and stuff
How many entries, how much storage used, etc.

#### Create Table
Define Colums

#### Delete Table


#### Locking a Table
If several entities are trying to access a table at the same time, it could cause issues, that is why you can lock a table for everyone but you. 

You can set the lock to be write only or read write depending on your needs. You also will have to add a duration to lock the table for. 

Tables can and should of course be unlocked early but should have a timeout to avoid possible race conditions. The timeout should have an upper bound, of for example 15-30s which should be clearly documented.

Locking a table will return a lock token if successful and the other endpoints will be locked, unless you provide the lock token in the headers.


#### Unlocking a Table
Unlocking a table can only be done by having the lock token. Otherwise it will unlock automatically after the timeout.


#### Get Table Entries

#### Add Table Entry

#### Update Table Entry

#### Get Table Entry

#### Delete Table Entry


#### Query Table Entries
Some kind of way to query tables with specific column constraints and also define what data/columns you want. should be basic but make life easier and increase performance.



### Service Bucket Access
These Endpoints get used by services to access the buckets.

#### Get Buckets

#### Get Buckets Quota
How much storage buckets can use and have used and how many buckets can be created/have been created

#### Get Bucket
How many entries, how much storage used, etc.

#### Create Bucket

#### Delete Bucket



#### Get Entries for Bucket

#### Add Entry to Bucket
Upload File/Data to Bucket alongside metadata.
TODO: Decide if it should be a POST with raw data + custom JSON metadata header or a multipart form with metadata and file seperate

#### Get Entry Info from Bucket
Get Info about the entry but not the data itself.
Can be if it exists, size, maybe timestamp, filename with extension?

#### Get Entry from Bucket
Get Raw Data from an Entry

#### Delete Entry from Bucket




### DSGVO and such
These endpoints should be signed by the user. If someone without a signature wants something, they should use the public contact or report endpoint

#### Get Complete Account Export

#### Delete Account and all Data

#### Deactive Handle or so

#### Move Handle to different IDP or so

#### Import Export of different IDP?
If you want to move your data to a different IDP you can export it and register somewhere else and import it there hopefully.

Can also make the current IDP point to the new one

Need more details as to like how itll work and with the base identity


### Account Information

#### Get Storage Details

#### Get Storage Quotas

#### A







## Admin API
These API Endpoints should only be accessible by signed requests which are authorized to be an administrator of the IDP.

They do not need to 100% implement all the Endpoints by the spec but it would make sense to have these endpoints. (Especially if using a general (statically hosted/local) client)

### General
You can query between user signed and guest requests.
And also by status (open / done / flagged)

#### Get Contact Requests

#### Update Contact Request
Set it to Open/Done/Flagged and also allow for custom notes.

#### Delete Contact Request

#### Get Report Requests

#### Update Report Request
Set it to Open/Done/Flagged and also allow for custom notes.

#### Delete Report Request


#### Set Public IDP Instance Info Data



### Registration Management

#### View Registration Codes
View used and unused registration codes

#### Create Registration Code
Create a registration code for a user / admin

#### Delete Registration Code


#### Set Registrations Allowed


#### Get Registration Code Requests

#### Update Registration Code Request
Set it to Open/Done/Flagged

#### Delete Registration Code Request


### User Management
View User Details, Delete Users, send warnings, etc.

Also promote/demote Admin status

Also see all handles of a user and maybe manage the quotas?

#### A


### Encrypted Password/Keypair Storage Management
Manage the Encrypted Storage. (View all entries, delete entries)

See all entries for a user maybe, stats, idk yet.

#### A



### User Service Management
Managing Services for a handle

#### A


### User Service Table Management
Managing Tables from Services for a handle

#### A

### User Service Bucket Management
Managing Buckets from Services for a handle

#### A


### User Storage Quota Management

TODO: Define behaviour on what should happen if an admin shrinks the quota for a user. What should get shrunk and what if there already is too much data for the quota? Force Delete? Send the user a notice and give them a month to download their data or to fix their quota? 

Two distinct quotas, binary content and table data!

How much storage can be used / is used, and how many tables can be created / have been created. Also how many columns/rows a table can have.

#### B


### Service Management
View Services that are used, maybe some stats, have a blocklist of server.


#### B







### Stats
Stats for user and service access and storage quotas.

Setting the total IDP storage quota

#### B


### Backup
Backup related things


#### Export Full Backup


#### Import Full Backup







## Potential for future improvement

If IDPs get large there should be some moderation users with some kind of abilities but not quite administrators.

Maybe include rate limiting suggestions for the endpoints

Look into synchronised code blocks / locking table accesses to avoid weird issues

Look into locking Buckets maybe?