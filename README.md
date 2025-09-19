# MongoDB Aggregation and Logical Operation Notes

This repository contains notes and examples on **MongoDB Aggregation Framework** and **Logical Operators**.  
All queries can be executed in **MongoDB Shell (mongosh)** or in **MongoDB Compass**.

---

Perfect 🚀 I’ll rewrite your **README.md** so it clearly explains the **step-by-step flow** (from database creation → inserting → aggregation → logical queries).

Here’s the updated content for your README:

````markdown
# MongoDB Aggregation and Logical Operation Notes

This repository contains step-by-step notes and examples on **MongoDB Database Creation**, **Data Insertion**, **Aggregation Framework**, and **Logical Operators**.  
All queries can be executed in **MongoDB Shell (mongosh)** or in **MongoDB Compass**.

---

## 📌 Step 1: Create Database and Collection
Switch to a new database and create a collection:
```js
use collegeDB;

db.createCollection("students");
````

---

## 📌 Step 2: Insert Documents

Insert sample student data:

```js
db.students.insertMany([
  { name: "Rahul", age: 20, city: "Hyderabad", department: "CSE", marks: 85 },
  { name: "Anjali", age: 19, city: "Bangalore", department: "ECE", marks: 72 },
  { name: "Ravi", age: 21, city: "Hyderabad", department: "IT", marks: 60 },
  { name: "Meena", age: 18, city: "Chennai", department: "CSE", marks: 45 },
  { name: "Arjun", age: 22, city: "Bangalore", department: "ECE", marks: 30 }
]);
```

---

## 📌 Step 3: Aggregation Pipeline

The **aggregation pipeline** is a framework for data aggregation modeled on the concept of data processing pipelines.
Documents enter a multi-stage pipeline that transforms them into aggregated results.

### Basic Syntax

```js
db.collection.aggregate([
  { stage1 },
  { stage2 },
  ...
]);
```

### Examples

#### Match students with marks ≥ 50

```js
db.students.aggregate([
  { $match: { marks: { $gte: 50 } } }
]);
```

#### Group students by department

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

#### Project name, marks, and pass/fail

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

---

## 📌 Step 4: Logical Operators

### `$and`

```js
db.students.find({
  $and: [
    { city: "Hyderabad" },
    { age: { $gte: 20 } }
  ]
});
```

### `$or`

```js
db.students.find({
  $or: [
    { city: "Hyderabad" },
    { city: "Bangalore" }
  ]
});
```

### `$not`

```js
db.students.find({
  marks: { $not: { $gte: 35 } }
});
```

---




---


