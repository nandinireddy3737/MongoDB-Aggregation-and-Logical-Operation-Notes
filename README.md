# MongoDB Aggregation and Logical Operation Notes

This repository contains step-by-step notes and examples on **MongoDB Database Creation**, **Data Insertion**, **Aggregation Framework**, and **Logical Operators**, along with **sample outputs**.

---

## 📌 Step 1: Create Database and Collection
```js
use collegeDB;

db.createCollection("students");
````

---

## 📌 Step 2: Insert Documents

```js
db.students.insertMany([
  { name: "Rahul", age: 20, city: "Hyderabad", department: "CSE", marks: 85 },
  { name: "Anjali", age: 19, city: "Bangalore", department: "ECE", marks: 72 },
  { name: "Ravi", age: 21, city: "Hyderabad", department: "IT", marks: 60 },
  { name: "Meena", age: 18, city: "Chennai", department: "CSE", marks: 45 },
  { name: "Arjun", age: 22, city: "Bangalore", department: "ECE", marks: 30 }
]);
```

```json
[
  { "name": "Rahul", "age": 20, "city": "Hyderabad", "department": "CSE", "marks": 85 },
  { "name": "Anjali", "age": 19, "city": "Bangalore", "department": "ECE", "marks": 72 },
  { "name": "Ravi", "age": 21, "city": "Hyderabad", "department": "IT", "marks": 60 },
  { "name": "Meena", "age": 18, "city": "Chennai", "department": "CSE", "marks": 45 },
  { "name": "Arjun", "age": 22, "city": "Bangalore", "department": "ECE", "marks": 30 }
]
```

---

## 📌 Step 3: Aggregation Queries with Outputs

### 1. Match students with marks ≥ 50

```js
db.students.aggregate([
  { $match: { marks: { $gte: 50 } } }
]);
```

**Output:**

```json
[
  { "name": "Rahul", "age": 20, "city": "Hyderabad", "department": "CSE", "marks": 85 },
  { "name": "Anjali", "age": 19, "city": "Bangalore", "department": "ECE", "marks": 72 },
  { "name": "Ravi", "age": 21, "city": "Hyderabad", "department": "IT", "marks": 60 }
]
```

---

### 2. Group students by department (average marks & total count)

```js
db.students.aggregate([
  {
    $group: {
      _id: "$department",
      avgMarks: { $avg: "$marks" },
      totalStudents: { $sum: 1 }
    }
  }
]);
```

**Output:**

```json
[
  { "_id": "CSE", "avgMarks": 65, "totalStudents": 2 },
  { "_id": "ECE", "avgMarks": 51, "totalStudents": 2 },
  { "_id": "IT",  "avgMarks": 60, "totalStudents": 1 }
]
```

---

### 3. Project name, marks, and pass/fail status

```js
db.students.aggregate([
  {
    $project: {
      name: 1,
      marks: 1,
      isPassed: { $cond: [ { $gte: ["$marks", 35] }, true, false ] }
    }
  }
]);
```

**Output:**

```json
[
  { "name": "Rahul", "marks": 85, "isPassed": true },
  { "name": "Anjali", "marks": 72, "isPassed": true },
  { "name": "Ravi",  "marks": 60, "isPassed": true },
  { "name": "Meena", "marks": 45, "isPassed": true },
  { "name": "Arjun", "marks": 30, "isPassed": false }
]
```

---

## 📌 Step 4: Logical Operators with Outputs

### 1. `$and` → Students from Hyderabad AND age ≥ 20

```js
db.students.find({
  $and: [
    { city: "Hyderabad" },
    { age: { $gte: 20 } }
  ]
});
```

**Output:**

```json
[
  { "name": "Rahul", "age": 20, "city": "Hyderabad", "department": "CSE", "marks": 85 },
  { "name": "Ravi",  "age": 21, "city": "Hyderabad", "department": "IT", "marks": 60 }
]
```

---

### 2. `$or` → Students from Hyderabad OR Bangalore

```js
db.students.find({
  $or: [
    { city: "Hyderabad" },
    { city: "Bangalore" }
  ]
});
```

**Output:**

```json
[
  { "name": "Rahul", "age": 20, "city": "Hyderabad", "department": "CSE", "marks": 85 },
  { "name": "Ravi",  "age": 21, "city": "Hyderabad", "department": "IT", "marks": 60 },
  { "name": "Anjali", "age": 19, "city": "Bangalore", "department": "ECE", "marks": 72 },
  { "name": "Arjun",  "age": 22, "city": "Bangalore", "department": "ECE", "marks": 30 }
]
```

---

### 3. `$not` → Students who did **not** pass (marks < 35)

```js
db.students.find({
  marks: { $not: { $gte: 35 } }
});
```

**Output:**

```json
[
  { "name": "Arjun", "age": 22, "city": "Bangalore", "department": "ECE", "marks": 30 }
]

