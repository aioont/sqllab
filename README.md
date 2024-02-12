Db.collectionName.find({Query},{Project})

Query=>equivalent to where clause in sql
Projection=>equivalent to selection in sql

user@user-IdeaPad-Gaming-3-15ARH7:~$ mongosh 
Current Mongosh Log ID:	65c5afeb2210e2d16c82e0ef
Connecting to:		mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.1.3
Using MongoDB:		7.0.5
Using Mongosh:		2.1.3

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2024-02-09T10:24:00.444+05:30: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2024-02-09T10:24:01.243+05:30: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2024-02-09T10:24:01.243+05:30: vm.max_map_count is too low
------

test> show dbs
admin   40.00 KiB
config  72.00 KiB
local   40.00 KiB
test> use students
switched to db students
students> show dbs
admin   40.00 KiB
config  72.00 KiB
local   72.00 KiB
students> db.createCollection("student")
{ ok: 1 }
students> use students
already on db students
students> show dbs
admin     40.00 KiB
config    72.00 KiB
local     72.00 KiB
students   8.00 KiB
students> db.dropDatabase()
{ ok: 1, dropped: 'students' }
students> db.createCollection("student")
{ ok: 1 }
students> db.student.insertOne({name: 'Sachin', rollno: 10, cgpa: 8.8})
{
  acknowledged: true,
  insertedId: ObjectId('65c5b1cf2210e2d16c82e0f0')
}
students> db.student.find().sort()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  }
]
students> db.student.find().sort(cgpa)
ReferenceError: cgpa is not defined
students> db.student.find().sort('cgpa')
[
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  }
]
students> db.student.find().limit(2)
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]

students> db.student.find().sort({cgpa:-1})
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  }
]
students> db.student.find().sort({cgpa:-1}).limit(2)
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]
students> db.student.find().sort({cgpa:1}).limit(2)
[
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]

students> db.student.find().sort({cgpa:1}).limit(2)
[
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]
students> db.student.find({rollno:11})
[
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]
students> db.student.find({rollno:11},{_id:false, name:true, cgpa:true})
[ { name: 'Nina', cgpa: 8 } ]
students> 


students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  }
]
students> db.student.find.limit(2)
TypeError: db.student.find.limit is not a function
students> db.student.find().limit(2)
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  }
]
students> db.students.updateOne({name:abhi},{$set:{name:sachin}})
ReferenceError: abhi is not defined
students> db.students.updateOne({name:sachin},{$set:{name:abhi}})
ReferenceError: sachin is not defined
students> db.students.updateOne({name:Sachin},{$set:{name:abhi}})
ReferenceError: Sachin is not defined
students> db.students.updateOne({name:'Sachin'},{$set:{name:'abhi'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
students> db.students.updateOne({name:'abhi'},{$set:{name:'Sachin'}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
students> db.students.find()

students> db.students.find()

students> 

students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  }
]
students> db.student.insertOne({name: 'Test', rollno: 15, cgpa: 8.2, fulltime:false})
{
  acknowledged: true,
  insertedId: ObjectId('65c9c5cd351399b58b2e6d9c')
}
students> db.student.updateOne({name: 'Test'}, {$set: {fulltime: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true
  }
]
students> db.student.updateMany({}, {$set: {fulltime: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 3,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    fulltime: true
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    fulltime: true
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    fulltime: true
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true
  }
]
students> db.student.updateOne({}, {$set: {fulltime: false}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    fulltime: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    fulltime: true
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    fulltime: true
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true
  }
]
students> db.student.find({name: 'Test'})
[
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true
  }
]
students> db.student.updateOne({name: 'Test'}, {$unset: {fulltime: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find({name: 'Test'})
[
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2
  }
]
students> db.student.updateMany({}, {$unset: {fulltime: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 3,
  upsertedCount: 0
}
students> db.student.find({name: 'Test'})
[
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2
  }
]
students> db.student.insertMany({}, {$set: {placed: false}})
MongoInvalidArgumentError: Argument "docs" must be an array of documents
students> db.student.updateMany({}, {$set: {placed: false}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 4,
  modifiedCount: 4,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    placed: false
  }
]
students> db.student.updateMany({name: 'Test'}, {$set: {fulltime: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    placed: false,
    fulltime: true
  }
]
students> db.student.updateMany({fulltime: {$exist: true}, {$unset: {placed: ""}})
Uncaught:
SyntaxError: Unexpected token (1:49)

> 1 | db.student.updateMany({fulltime: {$exist: true}, {$unset: {placed: ""}})
    |                                                  ^
  2 |

students> db.student.updateMany({fulltime: {$exist: true}},{$unset: {placed: ""}})
MongoServerError: unknown operator: $exist
students> db.student.updateMany({fulltime: {$exists: true}},{$unset: {placed: ""}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true
  }
]
students> db.student.updateMany({name: 'Test'}, {$set: {placed: true}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  },
  {
    _id: ObjectId('65c9c5cd351399b58b2e6d9c'),
    name: 'Test',
    rollno: 15,
    cgpa: 8.2,
    fulltime: true,
    placed: true
  }
]
students> db.student.updateMany({fulltime: $exists: true}}, {})
Uncaught:
SyntaxError: Unexpected token, expected "," (1:40)

> 1 | db.student.updateMany({fulltime: $exists: true}}, {})
    |                                         ^
  2 |

students> db.student.updateMany({fulltime: {$exists: true}}, {})
MongoInvalidArgumentError: Update document requires atomic operators
students> db.student.deleteOne({fulltime: {$exists: true}})
{ acknowledged: true, deletedCount: 1 }
students> db.student.find()
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  }
]
students> db.student.find(name: 'Sachin')
Uncaught:
SyntaxError: Unexpected token, expected "," (1:20)

> 1 | db.student.find(name: 'Sachin')
    |                     ^
  2 |

students> db.student.find({name: 'Sachin'})
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  }
]
students> db.student.find({name: {$ne: 'Sachin'}})
[
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f1'),
    name: 'Nina',
    rollno: 11,
    cgpa: 8,
    placed: false
  },
  {
    _id: ObjectId('65c5b29e2210e2d16c82e0f2'),
    name: 'Cia',
    rollno: 12,
    cgpa: 7.4,
    placed: false
  }
]
students> db.student.find({cgpa: {$gte: 8.5}})
[
  {
    _id: ObjectId('65c5b1cf2210e2d16c82e0f0'),
    name: 'Sachin',
    rollno: 10,
    cgpa: 8.8,
    placed: false
  }
]





