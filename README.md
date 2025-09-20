
# MongoDB Aggregation and Logical Operation Notes



## 🗄 Create Database & Dataset

```
use schoolDB
```

```
db.students.insertMany([
  { name: "Alice", age: 20, marks: 85, city: "Delhi" },
  { name: "Bob", age: 22, marks: 67, city: "Mumbai" },
  { name: "Charlie", age: 21, marks: 92, city: "Delhi" },
  { name: "David", age: 23, marks: 58, city: "Chennai" },
  { name: "Eva", age: 20, marks: 74, city: "Mumbai" }
])
```

**Output (from shell):**

```
switched to db schoolDB
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("66f2e4b3a23f98d7a1c11111"),
    '1': ObjectId("66f2e4b3a23f98d7a1c11112"),
    '2': ObjectId("66f2e4b3a23f98d7a1c11113"),
    '3': ObjectId("66f2e4b3a23f98d7a1c11114"),
    '4': ObjectId("66f2e4b3a23f98d7a1c11115")
  }
}
```

---



### 1. Match Students with Marks ≥ 70

```
db.students.aggregate([
  { $match: { marks: { $gte: 70 } } }
])
```

**Output (from shell):**

```
[
  { _id: ObjectId("66f2e4b3a23f98d7a1c11111"), name: 'Alice', age: 20, marks: 85, city: 'Delhi' },
  { _id: ObjectId("66f2e4b3a23f98d7a1c11113"), name: 'Charlie', age: 21, marks: 92, city: 'Delhi' },
  { _id: ObjectId("66f2e4b3a23f98d7a1c11115"), name: 'Eva', age: 20, marks: 74, city: 'Mumbai' }
]
```

---

### 2. Group Students by City and Find Average Marks

```
db.students.aggregate([
  { $group: { _id: "$city", avgMarks: { $avg: "$marks" } } }
])
```

**Output (from shell):**

```
[
  { _id: 'Delhi', avgMarks: 88.5 },
  { _id: 'Mumbai', avgMarks: 70.5 },
  { _id: 'Chennai', avgMarks: 58 }
]
```

---

### 3. Sort Students by Marks (Descending)

```
db.students
```
