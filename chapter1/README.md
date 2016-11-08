# Welcome to MongoDB Security

## Which topics are we going to cover in this course?
	CRUD
X	Encryption
X	Authorization
X	Auditing
	Aggregation


## Authentication vs Authorisation
Authentication is...
Choose the best answer:
	How we know what a user can do on a system.
X	How we know who a user is on a system.

## Authentication Mechanisms Overview
Which authentication mechanisms are supported by MongoDB?
Check all that apply:
X	LDAP
	RSA Tokens
X	SCRAM-SHA-1
	LTPA
X	Kerberos

## Authentication Mechanisms
Which of the following statements are true?
Check all that apply:
	Kerberos is an authentication and authorization protocol
X	X.509 can be used to authentivcate members of a sharded cluster
	SCRAM-SHA-1 is a certificate based authentication mechanism
X	MONGODB-CR is deprecated as of MongoDB 3.0
	A copy of a user's LDAP cerdentials are stored in MongoDB

The false statements are:

Kerberos is an authentication and authorization protocol.
	Kerberos is an *authentication* protocol.

SCRAM-SHA-1 is a certificate based authentication mechanism.
	SCRAM-SHA-1 is a *challenge/response* authentication mechanism. X.509 is the only certificate based authenticate mechanism supported by MongoDB.

A copy of a user's LDAP credentials are stored in MongoDB.
	LDAP is an *external* authentication mechanism. By definition an external authentication mechanism does *not* store user credentials inside MongoDB.



# The Localhost Exception
Which of the following statements are false concerning the localhost exception?
Check all that apply:
X	The localhost execption allows you to create one user per database
	The localhost exception is only applicable when connected to MongoDB via the localhost network interface
X	The localhost exceptio allows you to run `show dbs`
X	The localhost exception is not applicable to members in a sharded cluster


Answer

The false statements are:

The localhost exception allows you to create one user per database.
	The localhost exception only allows you to create one user. After the first user is created any other attempt to create a user (even on another database) will fail.

The localhost exception allows you to run show dbs.
	The localhost exception only allows you to create a user. Any other command that requires authorization will fail.

The localhost exception is not applicable to members in a sharded cluster.
	The localhost exception still applies to members of a sharded cluster (or a replica set).

The true statement is:

The localhost exception is only applicable when connected to MongoDB via the localhost network interface.




