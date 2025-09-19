# MongoDB Aggregation and Logical Operation Notes

This repository contains notes and examples on **MongoDB Aggregation Framework** and **Logical Operators**.  
All queries can be executed in **MongoDB Shell (mongosh)** or in **MongoDB Compass**.

---

## 📌 Aggregation Pipeline

The **aggregation pipeline** is a framework for data aggregation modeled on the concept of data processing pipelines.  
Documents enter a multi-stage pipeline that transforms them into aggregated results.

### Basic Syntax
```js
db.collection.aggregate([
  { stage1 },
  { stage2 },
  ...
]);
