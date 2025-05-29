# mongodb_medium

## steps to follow 
# step-1

  created a database sucessfully in mongodb atlas
code: use aggregationAssignmentDB
# step -2
intersion of samples data:

    db.products.insertMany([{ name: "Laptop Pro", category: "Electronics", price: 1200, quantity: 10, tags: ["computer", "portable", "work"], date_added: new Date("2023-01-15T10:00:00Z"), supplier: { name: "TechGlobe", location: "USA" } },.......]);

![image](https://github.com/user-attachments/assets/dab412b8-4f27-47b6-b076-b2949ab927f5)



##  Medium assignment

# 1. Total Quantity of Products by Supplier:
     
  
    db.products.aggregate([{$group: {_id: "$supplier.name",totalQuantity: { $sum: "$quantity" }}}]);

  # Description : 
  used  functions 
  $group: To aggregate data based on supplier.name.
  $sum: To total the quantity of all products grouped under each supplier.

  ![image](https://github.com/user-attachments/assets/e1f8d386-d001-4bbb-8bd6-24d703d3578e)
# 2. Average Price of Products per Tag:
 ## code:
    db.products.aggregate([{$unwind: "$tags"},{$group: {_id: "$tags", averagePrice: { $avg: "$price" }}},{$sort: {averagePrice: -1 }}]);
  # Description :
  $unwind: Breaks down each array element in tags into separate documents.

  $group: Groups documents by tag and calculates the average price.

  $avg: Computes the average of the price field.

  $sort: Orders results by average price in descending order.
  
  ![image](https://github.com/user-attachments/assets/90c4d2b5-bedc-4006-a678-021e9a76387f)


# 3. Products Added in February 2023:
   ## code 
    db.products.aggregate([{$match: {date_added: {$gte: new Date("2023-02-01T00:00:00Z"),$lt: new Date("2023-03-01T00:00:00Z")}}},{$project: {_id: 0,name: 1,category: 1,formattedDateAdded: {$dateToString: {format: "%Y-%m-%d",date: "$date_added"}}}}]);

# Description :
$match: Filters products whose date_added falls between "2023-02-01" and "2023-02-28".

$project: Selects specific fields for output.

$dateToString: Formats the date_added field to a user-friendly date string.

![image](https://github.com/user-attachments/assets/f8ab3a96-0e67-4c2f-a591-ff2323aa5c04)
