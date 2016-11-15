Create keyfile on db

`
vagrant@database:~/shared$ openssl rand -base64 755 > mongodb-keyfile
vagrant@database:~/shared$ chmod 400 mongodb-keyfile
`

Shutdown each repl set member starting with secondaries
TODO
`
pkill mongo
`

Start the primary with keyfile, then the secondaries with keyfiles
`
$ mongod --replSet TO_BE_SECURED --dbpath ~/M310-HW-1.2/r0 --logpath ~/M310-HW-1.2/r0/mongodb.log --port 31120  --fork --keyFile ~/shared/mongodb-keyfile
$ mongod --replSet TO_BE_SECURED --dbpath ~/M310-HW-1.2/r1 --logpath ~/M310-HW-1.2/r1/mongodb.log --port 31121  --fork --keyFile ~/shared/mongodb-keyfile
$ mongod --replSet TO_BE_SECURED --dbpath ~/M310-HW-1.2/r2 --logpath ~/M310-HW-1.2/r2/mongodb.log --port 31122  --fork --keyFile ~/shared/mongodb-keyfile
`

Create root user
`
$ mongo --port 31120
MongoDB Enterprise TO_BE_SECURED:PRIMARY > use admin
switched to db admin
MongoDB Enterprise TO_BE_SECURED:PRIMARY > db.createUser({user: 'admin', pwd: 'webscale', roles: [ { role: 'root', db: 'admin' } ]})
 [ { role: 'root', db: 'admin' } ]})
Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "root",
			"db" : "admin"
		}
	]
}
`


# Answer  - this is incorrect though???!?!?!
`
{ "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:45:08.951Z"), "myState" : 1, "term" : NumberLong(9), "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 1, "stateStr" : "PRIMARY", "uptime" : 301, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "electionTime" : Timestamp(1479195618, 1), "electionDate" : ISODate("2016-11-15T07:40:18Z"), "configVersion" : 1, "self" : true }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 296, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.368Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.014Z"), "pingMs" : NumberLong(0), "syncingTo" : "database:31120", "configVersion" : 1 }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 296, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.368Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.210Z"), "pingMs" : NumberLong(0), "syncingTo" : "database:31121", "configVersion" : 1 } ], "ok" : 1 }
{"members":["database:31120","database:31121","database:31122"],"statuses":["PRIMARY","SECONDARY","SECONDARY"]}
{ "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:45:09.078Z"), "myState" : 2, "term" : NumberLong(9), "syncingTo" : "database:31120", "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 1, "stateStr" : "PRIMARY", "uptime" : 301, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.015Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.368Z"), "pingMs" : NumberLong(0), "electionTime" : Timestamp(1479195618, 1), "electionDate" : ISODate("2016-11-15T07:40:18Z"), "configVersion" : 1 }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 302, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "syncingTo" : "database:31120", "configVersion" : 1, "self" : true }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 296, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.031Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.211Z"), "pingMs" : NumberLong(0), "syncingTo" : "database:31121", "configVersion" : 1 } ], "ok" : 1 }
{"members":["database:31120","database:31121","database:31122"],"statuses":["PRIMARY","SECONDARY","SECONDARY"]}
{ "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:45:09.203Z"), "myState" : 2, "term" : NumberLong(9), "syncingTo" : "database:31121", "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 1, "stateStr" : "PRIMARY", "uptime" : 301, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.210Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.368Z"), "pingMs" : NumberLong(0), "electionTime" : Timestamp(1479195618, 1), "electionDate" : ISODate("2016-11-15T07:40:18Z"), "configVersion" : 1 }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 301, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "lastHeartbeat" : ISODate("2016-11-15T07:45:08.211Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:45:08.030Z"), "pingMs" : NumberLong(0), "syncingTo" : "database:31120", "configVersion" : 1 }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 302, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "syncingTo" : "database:31121", "configVersion" : 1, "self" : true } ], "ok" : 1 }
{"members":["database:31120","database:31121","database:31122"],"statuses":["PRIMARY","SECONDARY","SECONDARY"]}
`