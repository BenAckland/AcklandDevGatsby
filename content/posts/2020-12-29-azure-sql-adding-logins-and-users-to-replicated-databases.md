---
template: post
title: Azure SQL - Adding Logins and Users to Replicated Databases
slug: azure-sql-adding-logins-users-replicated-databases
socialImage: /media/ian-battaglia-9drs5e_rguc-unsplash.jpg
draft: false
date: 2020-12-29T18:01:47.091Z
description: Avoiding the error "The server principal "****" is not able to
  access the database "****" under the current security context." in replicated
  Azure SQL databases.
category: AzureSQL
tags:
  - Azure SQL
  - Quick Fix
---
Adding logins and users for replicated Azure SQL databases can be a bit fiddly. If, like me, you do it the wrong way you can end up unable to log in to your secondary DB using your new user hitting the error:

```
The server principal "****" is not able to access the database "****" under the current security context.
```

## Adding New Users

### Create a login

When adding new users you'll first create a login:

```
CREATE LOGIN imanewlogin WITH password='abcd1234';
```

Logins are server level username and password combos where the combo is the same for every database that the login is associated with. They must be created by admin users while connected to the master database.

### Create a user

Next you create a user. The user associates a single database with a login. Run the SQL against the DB you want to give access to:

```
CREATE USER imanewuser FROM LOGIN imanewlogin;
```

### Add Permissions

Finally, the newly added user must be given the correct permissions for the database in question.

```
EXEC sp_addrolemember 'db_datareader', 'imanewuser';
```

## Azure SQL Geo Replication

When adding new users following the steps to an Azure SQL DB that is using geo replication you might expect to that the new users that you have added to the primary DB will be replicated over to the secondary DB and that you will be able to log into the secondary using the same credentials. Unfortunately that's not quite the case and this is where I was tripped up.

### Users replicated but not logins

What you will find if you take a look at your secondary DB is that the replication has replicated the database users but not the new login. In hindsight that makes sense as it's the database that is being replicated and not the server.

Upon noticing that the login you need does not exist you might be tempted to simply create a login using the same SQL and credentials from the first step. **Don't do that.** This is what I did and what caused the error message up top when I attempted to log in to the secondary.

If you do run the SQL above you will create a new login with the same credentials but the underlying security identifier (SID) will be different to the original login you created in the primary and it will not match the SID of the user that has been replicated into the secondary DB.

What you need to do is create a new login in the secondary DB with the same SID as the new login you created in the primary server.

### Find the login you need to replicate

Run the following on the primary server to get the SID of the new created login:

```
SELECT [name], [sid]
FROM [sys].[sql_logins]
WHERE [type_desc] = 'SQL_Login'
```

Ensure it matched the SID of the user you created in the primary database:

```
SELECT [name], [sid]
FROM [sys].[database_principals]
WHERE [type_desc] = 'SQL_USER'
```

Finally, create a new login in the secondary server by running the following against the master DB:

```
CREATE LOGIN imanewlogin WITH password='abcd1234',
SID = <your SID>
```

The SID of the new login in the secondary server will now match that of the user you created in the beginning allowing you to connect to the database.