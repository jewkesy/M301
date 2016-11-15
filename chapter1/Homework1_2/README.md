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


# Answer
`
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31120/test { "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:40:19.565Z"), "myState" : 1, "term" : NumberLong(9), "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 1, "stateStr" : "PRIMARY", "uptime" : 12, "optime" : { "ts" : Timestamp(1479195618, 2), "t" : NumberLong(9) }, "optimeDate" : ISODate("2016-11-15T07:40:18Z"), "infoMessage" : "could not find member to sync from", "electionTime" : Timestamp(1479195618, 1), "electionDate" : ISODate("2016-11-15T07:40:18Z"), "configVersion" : 1, "self" : true }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 6, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:18.208Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:17.867Z"), "pingMs" : NumberLong(0), "configVersion" : 1 }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 6, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:18.208Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:18.068Z"), "pingMs" : NumberLong(0), "configVersion" : 1 } ], "ok" : 1 }
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31120/test {"members":["database:31120","database:31121","database:31122"],"statuses":["PRIMARY","SECONDARY","SECONDARY"]}
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31121/test { "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:40:19.687Z"), "myState" : 2, "term" : NumberLong(9), "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 11, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:17.867Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:18.208Z"), "pingMs" : NumberLong(0), "configVersion" : 1 }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 12, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "infoMessage" : "could not find member to sync from", "configVersion" : 1, "self" : true }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 6, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:17.867Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:18.068Z"), "pingMs" : NumberLong(0), "configVersion" : 1 } ], "ok" : 1 }
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31121/test {"members":["database:31120","database:31121","database:31122"],"statuses":["SECONDARY","SECONDARY","SECONDARY"]}
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31122/test { "set" : "TO_BE_SECURED", "date" : ISODate("2016-11-15T07:40:19.810Z"), "myState" : 2, "term" : NumberLong(9), "heartbeatIntervalMillis" : NumberLong(2000), "members" : [ { "_id" : 1, "name" : "database:31120", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 11, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:18.068Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:18.208Z"), "pingMs" : NumberLong(0), "configVersion" : 1 }, { "_id" : 2, "name" : "database:31121", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 11, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "lastHeartbeat" : ISODate("2016-11-15T07:40:18.068Z"), "lastHeartbeatRecv" : ISODate("2016-11-15T07:40:17.867Z"), "pingMs" : NumberLong(0), "configVersion" : 1 }, { "_id" : 3, "name" : "database:31122", "health" : 1, "state" : 2, "stateStr" : "SECONDARY", "uptime" : 12, "optime" : { "ts" : Timestamp(1479195573, 1), "t" : NumberLong(8) }, "optimeDate" : ISODate("2016-11-15T07:39:33Z"), "infoMessage" : "could not find member to sync from", "configVersion" : 1, "self" : true } ], "ok" : 1 }
MongoDB shell version: 3.2.10 connecting to: 127.0.0.1:31122/test {"members":["database:31120","database:31121","database:31122"],"statuses":["SECONDARY","SECONDARY","SECONDARY"]}
`