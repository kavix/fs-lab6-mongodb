Below is your complete MongoDB University Portal practical, cleaned up and organized into copy-paste-ready commands for GitHub.

I've corrected the syntax errors, fixed the `$set` and `$push` operations, and arranged everything in the correct execution order.

# MongoDB University Portal – Practical Commands

Database: `universityPortal` Collection: `students` Shell: MongoDB Mongosh

## 1. Start MongoDB and select database

javascript

```javascript
mongosh
```

javascript

```javascript
show dbs
```

javascript

```javascript
use universityPortal
```

javascript

```javascript
db
```

## 2. Create collection

javascript

```javascript
db.createCollection("students")
```

Check collections:

javascript

```javascript
show collections
```

## 3. Insert one student – insertOne()

javascript

```javascript
db.students.insertOne({
    name: "Anuradha",
    age: 22,
    major: "Computer Science",
    phone: "+94712345678",
    scholarship: true,
    address: {
        city: "Colombo",
        street: "Temple Road"
    },
    skills: [
        "Python",
        "Java",
        "MongoDB"
    ],
    semester: "Semester II",
    coursesTaken: [
        "COSC 32133",
        "BECS 32263"
    ]
})
```

## 4. Insert multiple students – insertMany()

javascript

```javascript
db.students.insertMany([
    {
        name: "Sithumini",
        age: 21,
        major: "Mathematics",
        phone: "+94723456789",
        scholarship: false,
        address: {
            city: "Kandy",
            street: "Peradeniya Rd"
        },
        skills: ["R", "Statistics", "Python"],
        semester: "Semester I",
        coursesTaken: ["MATH 3101", "STAT 3202"]
    },
    {
        name: "Nandana",
        age: 23,
        major: "Physics",
        phone: "+94773456780",
        scholarship: true,
        address: {
            city: "Galle",
            street: "Main Street"
        },
        skills: ["Matlab", "LaTeX"],
        semester: "Semester II",
        coursesTaken: ["PHYS 3102", "MATH 3101"]
    },
    {
        name: "Chamika",
        age: 20,
        major: "Biology",
        phone: "+94704567891",
        scholarship: false,
        address: {
            city: "Negombo",
            street: "Beach Road"
        },
        skills: ["Lab Research", "Data Analysis"],
        semester: "Semester II",
        coursesTaken: ["BIOL 3010", "CHEM 3020"]
    },
    {
        name: "Prasanna",
        age: 24,
        major: "Computer Science",
        phone: "+94711122233",
        scholarship: true,
        address: {
            city: "Matara",
            street: "Rahula Road"
        },
        skills: ["C++", "Docker", "Linux"],
        semester: "Semester I",
        coursesTaken: ["COSC 32133", "COSC 32253"]
    },
    {
        name: "Nisal",
        age: 21,
        major: "Mathematics",
        phone: "+94765544332",
        scholarship: false,
        address: {
            city: "Jaffna",
            street: "Station Road"
        },
        skills: ["Mathematics", "Python"],
        semester: "Semester II",
        coursesTaken: ["MATH 3101", "MATH 3103"]
    },
    {
        name: "Hiruni",
        age: 22,
        major: "Software Engineering",
        phone: "+94789988776",
        scholarship: true,
        address: {
            city: "Kurunegala",
            street: "Colombo Road"
        },
        skills: ["JavaScript", "React", "Node.js"],
        semester: "Semester II",
        coursesTaken: ["SE 3101", "COSC 32133"]
    }
])
```

## 5. Display databases and collections

javascript

```javascript
show dbs
```

javascript

```javascript
show collections
```

## 6. Display all student records – find()

javascript

```javascript
db.students.find()
```

javascript

```javascript
db.students.find({})
```

## 7. Display selected fields – Projection

Display only name and phone:

javascript

```javascript
db.students.find(
    {},
    {
        _id: 0,
        name: 1,
        phone: 1
    }
)
```

Display name, age and skills:

javascript

```javascript
db.students.find(
    {},
    {
        _id: 0,
        name: 1,
        age: 1,
        skills: 1
    }
)
```

Display name and major:

javascript

```javascript
db.students.find(
    {},
    {
        _id: 0,
        name: 1,
        major: 1
    }
)
```

## 8. Search students by skills

Find students whose skills contain Python:

javascript

```javascript
db.students.find({
    skills: "Python"
})
```

Find students whose skills array exactly matches `["Python"]`:

javascript

```javascript
db.students.find({
    skills: ["Python"]
})
```

Find students with Java:

javascript

```javascript
db.students.find({
    skills: "Java"
})
```

Find students with React:

javascript

```javascript
db.students.find({
    skills: "React"
})
```

Important: These two queries are different:

javascript

```javascript
db.students.find({ skills: "Python" })
```

Finds students where the skills array contains Python.

javascript

```javascript
db.students.find({ skills: ["Python"] })
```

Finds students whose entire skills array contains only Python.

## 9. Sort student records – sort()

Sort by age in descending order:

javascript

```javascript
db.students.find().sort({
    age: -1
})
```

Sort by age in ascending order:

javascript

```javascript
db.students.find().sort({
    age: 1
})
```

Sort by age descending and name ascending:

javascript

```javascript
db.students.find().sort({
    age: -1,
    name: 1
})
```

Display only name and age, sorted by age descending:

javascript

```javascript
db.students.find(
    {},
    {
        _id: 0,
        name: 1,
        age: 1
    }
).sort({
    age: -1,
    name: 1
})
```

## 10. Find a particular student

Find Anuradha:

javascript

```javascript
db.students.find({
    name: "Anuradha"
})
```

Find students from Mathematics:

javascript

```javascript
db.students.find({
    major: "Mathematics"
})
```

Find students aged 22:

javascript

```javascript
db.students.find({
    age: 22
})
```

Find students with scholarships:

javascript

```javascript
db.students.find({
    scholarship: true
})
```

Find students from Colombo:

javascript

```javascript
db.students.find({
    "address.city": "Colombo"
})
```

## 11. Update Anuradha's information – updateOne()

Question: Since information changes every semester, update Anuradha's phone number, set her scholarship status to false, and add a new course `"COSC 32253"` to her `coursesTaken` array using `$push`.

javascript

```javascript
db.students.updateOne(
    {
        name: "Anuradha"
    },
    {
        $set: {
            phone: "+94726677555",
            scholarship: false
        },
        $push: {
            coursesTaken: "COSC 32253"
        }
    }
)
```

Verify the update:

javascript

```javascript
db.students.find({
    name: "Anuradha"
})
```

Important correction- `$set` updates normal fields such as `phone` and `scholarship`.
- `$push` adds an item to an existing array such as `coursesTaken`.
- Do not use `$push` for `phone` or `scholarship` because they are not arrays.
- `updateOne()` uses a filter and an update document.

## 12. Update multiple students – updateMany()

Increase the age of all Mathematics students by 1:

javascript

```javascript
db.students.updateMany(
    {
        major: "Mathematics"
    },
    {
        $inc: {
            age: 1
        }
    }
)
```

Verify:

javascript

```javascript
db.students.find({
    major: "Mathematics"
})
```

## 13. Find students using data types – $type

Find students whose age is an integer:

javascript

```javascript
db.students.find({
    age: {
        $type: "int"
    }
})
```

Find students whose phone number is a string:

javascript

```javascript
db.students.find({
    phone: {
        $type: "string"
    }
})
```

## 14. More useful MongoDB commands

Find students older than 21:

javascript

```javascript
db.students.find({
    age: {
        $gt: 21
    }
})
```

Find students younger than 23:

javascript

```javascript
db.students.find({
    age: {
        $lt: 23
    }
})
```

Find students aged 21 or above:

javascript

```javascript
db.students.find({
    age: {
        $gte: 21
    }
})
```

Find students aged between 21 and 23:

javascript

```javascript
db.students.find({
    age: {
        $gte: 21,
        $lte: 23
    }
})
```

Find Computer Science students with scholarships:

javascript

```javascript
db.students.find({
    major: "Computer Science",
    scholarship: true
})
```

Find Mathematics or Physics students:

javascript

```javascript
db.students.find({
    major: {
        $in: ["Mathematics", "Physics"]
    }
})
```

Count all students:

javascript

```javascript
db.students.countDocuments()
```

Count Mathematics students:

javascript

```javascript
db.students.countDocuments({
    major: "Mathematics"
})
```

## 15. Delete commands

Delete one student:

javascript

```javascript
db.students.deleteOne({
    name: "Chamika"
})
```

Delete all students from Biology:

javascript

```javascript
db.students.deleteMany({
    major: "Biology"
})
```

Be careful Delete operations permanently remove matching documents.

## 16. Final verification

Display all student records:

javascript

```javascript
db.students.find().pretty()
```

Count student records:

javascript

```javascript
db.students.countDocuments()
```

Display collection names:

javascript

```javascript
show collections
```

Display databases:

javascript

```javascript
show dbs
```

Exit MongoDB:

javascript

```javascript
exit
```

# GitHub README.md version

If you want to upload this practical to GitHub, use the following structure:

text

```text
MongoDB-University-Portal/
│
├── README.md
│
└── commands/
    └── universityPortal.js
```

Save your MongoDB commands in `universityPortal.js` (without the `mongosh>` prompts).

To upload using Git Bash or VS Code terminal:

bash

```bash
git init
git add .
git commit -m "Add MongoDB University Portal practical"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/MongoDB-University-Portal.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username and create the repository on GitHub first.

One important note: Run the insert commands only once. If you run `insertOne()` and `insertMany()` repeatedly, you will create duplicate student records.
