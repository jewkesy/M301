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



## The Localhost Exception
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


## Authentication Methods
Which of these authentication methods will fail if a server is started with the following options?
`
$ mongod --auth
$ mongo
use admin
db.createUser({user: 'kirby', pwd: 'password', roles: ['root']})
`
Check all that apply:

X	`$ mongo -u kirby -p password
	`$ mongo admin -u kirby -p password
X	`$ mongo 
	db.auth('kirby', 'password')`
	`$ mongo
	use admin
	db.auth('kirby', 'password')`


Answer

The authentication methods that will fail for the given server configuration are:
`
$ mongo -u kirby -p password
`
A user must authenticate to the database they were created on. This command will fail because kirby was created on the admin database, but mongo attempts to connect to the test database unless otherwise specified.
`
$ mongo
db.auth('kirby', 'password')
`
You are allowed to connect to a server that has authorization enabled without authenticating first. The seccond command will fail however because you'll be connected to the test database and kirby was created on the admin database.

The authentication methods that will succeed for the given server configuration are:
`
$ mongo admin -u kirby -p password
$ mongo
use admin
db.auth('kirby', 'password')
`

## Authentication on Sharded Clusters
Authentication on a sharded cluster is achieved by...
Check all that apply:

	passing a --auth option to mongos
	passing a --auth option to each mongod
	passing a --auth option to mongod and to mongos
X	enabling internal authentication between members using keyfiles
X	enabling internal authentication between members using X.509 certificates

Answer

Authentication on a sharded cluster is achieved by...

enabling internal authentication between members using keyfiles
enabling internal authentication between members using X.509 certificates
Authentication on a sharded cluster is enabled by enabling internal authentication. It doesn't matter if you use keyfiles or X.509 certificates.

Authentication on a sharded cluster is not achieved by...

passing a --auth option to mongos

There is no --auth option for mongos.

passing a --auth option to each mongod

This would enable client authentication on each mongod, which would not enable authentication on communication via the mongos.

passing a --auth option to each mongod and to ``mongos``

There is no --auth option for mongos.

## Enabling SCRAM-SHA-1
SCRAM-SHA-1 is the default password authentication mechanism on MongoDB.
Choose the best answer:

X	True
	False


Answer

SCRAM-SHA-1 is the default password authentication mechanism on MongoDB.


## Enabling X.509
How does the mongod know the identity of the client?
Check all that apply:

X	It obtains a certificate from the client when the TLS connection is established
X	The certificate must be signed by the certificate authority file passed to the mongod
X	The subject of the certifcate must match the names of the user in the $external database


Answer

All of the following are true:

It obtains a certificate from the client when the TLS connection is established.
The certificate must be signed by the certificate authority file passed to the mongod.
The subject of the certificate must match the name of the user in the $external database.


## Enabling LDAP
Which of the following are true regarding LDAP authentication?
Check all that apply:
	
X	MongoDB drivers authenticating to MongoDB with LDAP send LDAP credentials using SASL PLAIN which sends the username/password in clear text
X	LDAP Authentication support is a MongoDB Enterprise only feature
	LDAP is more secure than Kerberos
X	saslauthd is a proxy service used by mongod to talk to a LDAP server


Answer

The following are true regarding LDAP authentication:

MongoDB drivers authenticating to MongoDB with LDAP send LDAP credentials using SASL PLAIN which sends the username/password in clear text.
LDAP Authentication support is a MongoDB Enterprise only feature.
saslauthd is a proxy service used by mongod to talk to a LDAP server
LDAP is more secure than Kerberos

This is not true. LDAP was not designed for the purpose of external authentication. LDAP was designed to store user meta-data in a directory service. Kerberos was designed for the sole purpose of external authentication.






