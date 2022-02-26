# mongo-lab

See the notion (https://www.notion.so/Mongo-Lab-4b92157ab9254162af08ead76d068735) for instructions on how to complete this lab. Remember to fork over this repo, make your changes to your version, then push up the changes and finally submit it with a pull request.
_________________________________________________________________________________
    To find all the documents in our collection that have a weight property greater than 700, we run:
_________________________________________________________________________________
    > db.employees.find( { weight : { $gt : 700 } } ).pretty();
_________________________________________________________________________________
        {
            "_id" : ObjectId("6219a3a5306077004e7032f8"),
            "name" : "Unicrom",
            "dob" : ISODate("1973-02-10T03:10:00Z"),
            "loves" : [
                "energon",
                "redbull"
            ],
            "weight" : 984,
            "gender" : "m",
            "salary" : 182
        }
    {
        "_id" : ObjectId("6219a3a5306077004e7032fb"),
        "name" : "Ayna",
        "dob" : ISODate("1998-03-07T13:30:00Z"),
        "loves" : [
            "strawberry",
            "lemon"
        ],
        "weight" : 733,
        "gender" : "f",
        "salary" : 40
    }
    {
        "_id" : ObjectId("6219a3a5306077004e703301"),
        "name" : "Dunx",
        "dob" : ISODate("1976-07-18T22:18:00Z"),
        "loves" : [
            "grape",
            "watermelon"
        ],
        "weight" : 704,
        "gender" : "m",
        "salary" : 165
    }
_________________________________________________________________________________
If the field is an array, you can search for a match within that array
_________________________________________________________________________________
> db.employees.find(
... {
... loves:'energon'
... }
... ).pretty();
_________________________________________________________________________________
    {
        "_id" : ObjectId("6219a3a5306077004e7032f8"),
        "name" : "Unicrom",
        "dob" : ISODate("1973-02-10T03:10:00Z"),
        "loves" : [
            "energon",
            "redbull"
        ],
        "weight" : 984,
        "gender" : "m",
        "salary" : 182
    }
_________________________________________________________________________________
>If the object you pass into find()has more than one attribute, it will return documents that match both criteria. This is called an AND statement (like &&)
_________________________________________________________________________________
    > db.employees.find({loves:'energon'} && {gender:'m',weight:{ $gt:700} }).pretty();
_________________________________________________________________________________
{
	"_id" : ObjectId("6219a3a5306077004e7032f8"),
	"name" : "Unicrom",
	"dob" : ISODate("1973-02-10T03:10:00Z"),
	"loves" : [
		"energon",
		"redbull"
	],
	"weight" : 984,
	"gender" : "m",
	"salary" : 182
}
{
	"_id" : ObjectId("6219a3a5306077004e703301"),
	"name" : "Dunx",
	"dob" : ISODate("1976-07-18T22:18:00Z"),
	"loves" : [
		"grape",
		"watermelon"
	],
	"weight" : 704,
	"gender" : "m",
	"salary" : 165
}
>_________________________________________________________________________________ 
To find all documents that match at least one of a set of criteria, use an OR statement (like ||)
_________________________________________________________________________________
db.employees.find( { $or: [ { loves: 'apple' }, { weight: { $lt: 500 } } ] } ).pretty()
    {
        "_id" : ObjectId("6219a3a5306077004e7032f7"),
        "name" : "Aurora",
        "dob" : ISODate("1991-01-24T18:00:00Z"),
        "loves" : [
            "carrot",
            "grape"
        ],
        "weight" : 450,
        "gender" : "f",
        "salary" : 43
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032f9"),
        "name" : "Roooooodles",
        "dob" : ISODate("1979-08-18T22:44:00Z"),
        "loves" : [
            "apple"
        ],
        "weight" : 575,
        "gender" : "m",
        "salary" : 99
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032fa"),
        "name" : "Solnara",
        "dob" : ISODate("1985-07-04T06:01:00Z"),
        "loves" : [
            "apple",
            "carrot",
            "chocolate"
        ],
        "weight" : 550,
        "gender" : "f",
        "salary" : 80
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032fd"),
        "name" : "Raleigh",
        "dob" : ISODate("2005-05-03T04:57:00Z"),
        "loves" : [
            "apple",
            "sugar"
        ],
        "weight" : 421,
        "gender" : "m",
        "salary" : 2
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032fe"),
        "name" : "Leia",
        "dob" : ISODate("2001-10-08T18:53:00Z"),
        "loves" : [
            "apple",
            "watermelon"
        ],
        "weight" : 601,
        "gender" : "f",
        "salary" : 33
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032ff"),
        "name" : "Pilot",
        "dob" : ISODate("1997-03-01T10:03:00Z"),
        "loves" : [
            "apple",
            "watermelon"
        ],
        "weight" : 650,
        "gender" : "m",
        "salary" : 54
    }
________________________________________________________________________________________
To find documents that have a value that matches multiple criteria, pass an object that contains both tests. This is similar to an AND (&&), but for one property. If you try to do a normal AND statement, but use the same property, twice it won't work.
________________________________________________________________________________________
> db.employees.find( { salary: { $gte : 80, $lte : 165 } } ).pretty()
    {
        "_id" : ObjectId("6219a3a5306077004e7032f9"),
        "name" : "Roooooodles",
        "dob" : ISODate("1979-08-18T22:44:00Z"),
        "loves" : [
            "apple"
        ],
        "weight" : 575,
        "gender" : "m",
        "salary" : 99
    }
    {
        "_id" : ObjectId("6219a3a5306077004e7032fa"),
        "name" : "Solnara",
        "dob" : ISODate("1985-07-04T06:01:00Z"),
        "loves" : [
            "apple",
            "carrot",
            "chocolate"
        ],
        "weight" : 550,
        "gender" : "f",
        "salary" : 80
    }
    {
        "_id" : ObjectId("6219a3a5306077004e703301"),
        "name" : "Dunx",
        "dob" : ISODate("1976-07-18T22:18:00Z"),
        "loves" : [
            "grape",
            "watermelon"
        ],
        "weight" : 704,
        "gender" : "m",
        "salary" : 165
    }
> ________________________________________________________________________
We can change a specific value  
db.employee.update({name:'Pilot'},{
    $inc:{salary:-2}})
__________________________________________________________________________
{
        name: "Pilot",
        dob: new Date(1997, 2, 1, 5, 3),
        loves: ["apple", "watermelon"],
        weight: 650,
        gender: "m",
        salary: 54,
    },

    {
            "_id" : ObjectId("6219a3a5306077004e7032ff"),
        "name" : "Pilot",
        "dob" : ISODate("1997-03-01T10:03:00Z"),
        "loves" : [
            "apple",
            "watermelon"
        ],
        "weight" : 650,
        "gender" : "m",
        "salary" : 52
    ___________________________________________________________________________
   Multiple or divide a value
    ___________________________________________________________________________
        "_id" : ObjectId("6219a3a5306077004e7032ff"),
        "name" : "Pilot",
        "dob" : ISODate("1997-03-01T10:03:00Z"),
        "loves" : [
            "apple",
            "watermelon"
        ],
        "weight" : 650,
        "gender" : "m",
        "salary" : 26
    ______________________________________
Push a value onto an array-- pushed sugar
__________________________________________________
        "_id" : ObjectId("6219a3a5306077004e7032f7"),
        "name" : "Aurora",
        "dob" : ISODate("1991-01-24T18:00:00Z"),
        "loves" : [
            "carrot",
            "grape",
            "sugar"
        ],
        "weight" : 450,
        "gender" : "f",
        "salary" : 43> 
    _____________________________________________________
Pop a value off an array - popped love.1 but it took 2 instead??
 _____________________________________________________
        "_id" : ObjectId("6219a3a5306077004e7032f7"),
        "name" : "Aurora",
        "dob" : ISODate("1991-01-24T18:00:00Z"),
        "loves" : [
            "carrot",
            "grape"
        ],
        "weight" : 450,
        "gender" : "f",
        "salary" : 43

 _____________________________________________________
Popped the property love
 _____________________________________________________

            "_id" : ObjectId("6219a3a5306077004e7032f7"),
        "name" : "Aurora",
        "dob" : ISODate("1991-01-24T18:00:00Z"),
        "weight" : 450,
        "gender" : "f",
        "salary" : 43
 _____________________________________________________
rename a field -renamed salary wage
 _____________________________________________________
        {
        "_id" : ObjectId("6219a3a5306077004e7032f7"),
        "name" : "Aurora",
        "dob" : ISODate("1991-01-24T18:00:00Z"),
        "weight" : 450,
        "gender" : "f",
        "wage" : 43
    }
______________________________________________________
Upserts will insert a value if it doesn't exist. If it does, it will update it.
–––––––––––––––––––––––––––––––––––––––––––––––––––––––
        "_id" : ObjectId("6219c0b6a70db9764ab7b79d"),
        "page" : "employees",
        "hits" : 2
    }
