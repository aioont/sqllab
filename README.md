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







