Launch initial process: -
`
vagrant@database:~$ mongod --dbpath ~/data/db/
`


New Tab: -
`
$ vagrant ssh database
$ mongo
MongoDB Enterprise > db.createUser({user: 'alice', pwd: 'secret', roles: [ { role: 'root', db: 'admin' } ]})

Successfully added user: {
	"user" : "alice",
	"roles" : [
		{
			"role" : "root",
			"db" : "admin"
		}
	]
}

MongoDB Enterprise > db.auth('alice', 'secret')
1
MongoDB Enterprise > db.runCommand({getParameter: 1, authenticationMechanisms: 1})
{
	"authenticationMechanisms" : [
		"MONGODB-CR",
		"MONGODB-X509",
		"SCRAM-SHA-1"
	],
	"ok" : 1
}
MongoDB Enterprise > exit

`

Restart mongod process with auth: -
`
vagrant@database:~$ mongod --auth  --dbpath ~/data/db/
`




Which of the following statements will successfully run the above command on the standalone server that you've set up?

Check all that apply:
X	mongo admin -u alice -p secret --eval "db.runCommand({getParameter: 1, authenticationMechanisms: 1})"
	mongo --eval "db.runCommand({getParameter: 1, authenticationMechanisms: 1})"
	mongo -u alice -p secret --eval "db.runCommand({getParameter: 1, authenticationMechanisms: 1})"
	mongo -u alice -p secret --eval "db.runCommand({getParameter: 1, authenticationMechanisms: 1})" --authenticationDatabase admin
X	mongo admin --eval "db.auth('alice', 'secret');db.runCommand({getParameter: 1, authenticationMechanisms: 1})"
X	mongo -u alice -p secret --eval "db=db.getSisterDB('admin');db.runCommand({getParameter: 1, authenticationMechanisms: 1})" --authenticationDatabase admin

