# MongoDB-Exercise

## Task

**Q: Find all the information about each products**

```javascript
db.products.find();
```

**Q: Find the product price which are between 400 to 800**

```javascript
db.products.find({ product_price: { $gte: 400, $lte: 800 } });
```

**Q: Find the product price which are not between 400 to 600**

```javascript
db.products.find({ product_price: { $not: { $gte: 400, $lte: 800 } } });
```

**Q: List the four product which are greater than 500 in price**

```javascript
db.products.find({ product_price: { $gte: 500 } }).limit(4);
```

**Q: Find the product name and product material of each product**

```javascript
db.products.find({}, { product_name: 1, product_material: 1 });
```

**Q: Find the product with a row id of 10**

```javascript
db.products.find({ id: "10" });
```

**Q: Find all products which contain the value of soft in product material**

```javascript
db.products.find({ product_material: { $regex: /soft/, $options: "i" } });
```

**Q: Find products which contain product color indigo and product price 492.00**

```javascript
db.products.find({
  $and: [{ product_color: "indigo" }, { product_price: 492.0 }]
});
```

**Q: Delete the products which product price value are same**

```javascript
// First get list of product_price which are repeated. Result is [36, 47]

db.products.aggregate([
  { $group: { _id: "$product_price", count: { $count: {} } } },
  { $match: { _id: { $ne: null }, count: { $gt: 1 } } }
]);

db.products.deleteMany({ product_price: { $in: [36, 47] } });
```
