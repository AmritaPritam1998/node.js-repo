********Selecting From a Table*****
To select data from a table in MySQL, use the "SELECT" statement.

ExampleGet your own Node.js Server
Select all records from the "customers" table, and display the result object:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT * FROM customers", function (err, result, fields) {
    if (err) throw err;
    console.log(result);
  });
});
SELECT * will return all columns

Save the code above in a file called "demo_db_select.js" and run the file:

Run "demo_db_select.js"

C:\Users\Your Name>node demo_db_select.js
Which will give you this result:

[
  { id: 1, name: 'John', address: 'Highway 71'},
  { id: 2, name: 'Peter', address: 'Lowstreet 4'},
  { id: 3, name: 'Amy', address: 'Apple st 652'},
  { id: 4, name: 'Hannah', address: 'Mountain 21'},
  { id: 5, name: 'Michael', address: 'Valley 345'},
  { id: 6, name: 'Sandy', address: 'Ocean blvd 2'},
  { id: 7, name: 'Betty', address: 'Green Grass 1'},
  { id: 8, name: 'Richard', address: 'Sky st 331'},
  { id: 9, name: 'Susan', address: 'One way 98'},
  { id: 10, name: 'Vicky', address: 'Yellow Garden 2'},
  { id: 11, name: 'Ben', address: 'Park Lane 38'},
  { id: 12, name: 'William', address: 'Central st 954'},
  { id: 13, name: 'Chuck', address: 'Main Road 989'},
  { id: 14, name: 'Viola', address: 'Sideway 1633'}
]

***********selecting Columns*********
To select only some of the columns in a table, use the "SELECT" statement followed by the column name.

Example
Select name and address from the "customers" table, and display the return object:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT name, address FROM customers", function (err, result, fields) {
    if (err) throw err;
    console.log(result);
  });
});

Save the code above in a file called "demo_db_select2.js" and run the file:

Run "demo_db_select2.js"

C:\Users\Your Name>node demo_db_select2.js
Which will give you this result:

[
  { name: 'John', address: 'Highway 71'},
  { name: 'Peter', address: 'Lowstreet 4'},
  { name: 'Amy', address: 'Apple st 652'},
  { name: 'Hannah', address: 'Mountain 21'},
  { name: 'Michael', address: 'Valley 345'},
  { name: 'Sandy', address: 'Ocean blvd 2'},
  { name: 'Betty', address: 'Green Grass 1'},
  { name: 'Richard', address: 'Sky st 331'},
  { name: 'Susan', address: 'One way 98'},
  { name: 'Vicky', address: 'Yellow Garden 2'},
  { name: 'Ben', address: 'Park Lane 38'},
  { name: 'William', address: 'Central st 954'},
  { name: 'Chuck', address: 'Main Road 989'},
  { name: 'Viola', address: 'Sideway 1633'}
]
***********The Result Object*********
As you can see from the result of the example above, the result object is an array containing each row as an object.

To return e.g. the address of the third record, just refer to the third array object's address property:

Example
Return the address of the third record:

console.log(result[2].address);
Which will produce this result:

Apple st 652
The Fields Object
The third parameter of the callback function is an array containing information about each field in the result.

Example
Select all records from the "customers" table, and display the fields object:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT name, address FROM customers", function (err, result, fields) {
    if (err) throw err;
    console.log(fields);
  });
});
Save the code above in a file called "demo_db_select_fields.js" and run the file:

Run "demo_db_select_fields.js"

C:\Users\Your Name>node demo_db_select_fields.js
Which will give you this result:

[
  {
    catalog: 'def',
    db: 'mydb',
    table: 'customers',
    orgTable: 'customers',
    name: 'name',
    orgName: 'name',
    charsetNr: 33,
    length: 765,
    type: 253,
    flags: 0,
    decimals: 0,
    default: undefined,
    zeroFill: false,
    protocol41: true
  },
  {
    catalog: 'def',
    db: 'mydb',
    table: 'customers',
    orgTable: 'customers',
    name: 'address',
    orgName: 'address',
    charsetNr: 33,
    length: 765,
    type: 253,
    flags: 0,
    decimals: 0,
    default: undefined,
    zeroFill: false,
    protocol41: true
  }
]
As you can see from the result of the example above, the fields object is an array containing information about each field as an object.

To return e.g. the name of the second field, just refer to the second array item's name property:

Example
Return the name of the second field:

console.log(fields[1].name);
Which will produce this result:

address

*************mySql where********
Select With a Filter
When selecting records from a table, you can filter the selection by using the "WHERE" statement:

ExampleGet your own Node.js Server
Select record(s) with the address "Park Lane 38":

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT * FROM customers WHERE address = 'Park Lane 38'", function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
Save the code above in a file called "demo_db_where.js" and run the file:

Run "demo_db_where.js"

C:\Users\Your Name>node demo_db_where.js
*****Which will give you this result:

[
  { id: 11, name: 'Ben', address: 'Park Lane 38'}
]

*****Wildcard Characters
You can also select the records that starts, includes, or ends with a given letter or phrase.

Use the '%' wildcard to represent zero, one or multiple characters:

Example
Select records where the address starts with the letter 'S':

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT * FROM customers WHERE address LIKE 'S%'", function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
Save the code above in a file called "demo_db_where_s.js" and run the file:

Run "demo_db_where_s.js"

C:\Users\Your Name>node demo_db_where_s.js
Which will give you this result:

[
  { id: 8, name: 'Richard', address: 'Sky st 331'},
  { id: 14, name: 'Viola', address: 'Sideway 1633'}
]
Escaping Query Values
When query values are variables provided by the user, you should escape the values.

This is to prevent SQL injections, which is a common web hacking technique to destroy or misuse your database.

The MySQL module has methods to escape query values:

Example
Escape query values by using the mysql.escape() method:

var adr = 'Mountain 21';
var sql = 'SELECT * FROM customers WHERE address = ' + mysql.escape(adr);
con.query(sql, function (err, result) {
  if (err) throw err;
  console.log(result);
});
You can also use a ? as a placeholder for the values you want to escape.

In this case, the variable is sent as the second parameter in the query() method:

Example
Escape query values by using the placeholder ? method:

var adr = 'Mountain 21';
var sql = 'SELECT * FROM customers WHERE address = ?';
con.query(sql, [adr], function (err, result) {
  if (err) throw err;
  console.log(result);
});
If you have multiple placeholders, the array contains multiple values, in that order:

Example
Multiple placeholders:

var name = 'Amy';
var adr = 'Mountain 21';
var sql = 'SELECT * FROM customers WHERE name = ? OR address = ?';
con.query(sql, [name, adr], function (err, result) {
  if (err) throw err;
  console.log(result);
});
****************node.js mysql orderby*****
Sort the Result
Use the ORDER BY statement to sort the result in ascending or descending order.

The ORDER BY keyword sorts the result ascending by default. To sort the result in descending order, use the DESC keyword.

ExampleGet your own Node.js Server
Sort the result alphabetically by name:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT * FROM customers ORDER BY name", function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
Save the code above in a file called "demo_db_orderby.js" and run the file:

Run "demo_db_orderby.js"

C:\Users\Your Name>node demo_db_orderby.js
Which will give you this result:

[
  { id: 3, name: 'Amy', address: 'Apple st 652'},
  { id: 11, name: 'Ben', address: 'Park Lane 38'},
  { id: 7, name: 'Betty', address: 'Green Grass 1'},
  { id: 13, name: 'Chuck', address: 'Main Road 989'},
  { id: 4, name: 'Hannah', address: 'Mountain 21'},
  { id: 1, name: 'John', address: 'Higheay 71'},
  { id: 5, name: 'Michael', address: 'Valley 345'},
  { id: 2, name: 'Peter', address: 'Lowstreet 4'},
  { id: 8, name: 'Richard', address: 'Sky st 331'},
  { id: 6, name: 'Sandy', address: 'Ocean blvd 2'},
  { id: 9, name: 'Susan', address: 'One way 98'},
  { id: 10, name: 'Vicky', address: 'Yellow Garden 2'},
  { id: 14, name: 'Viola', address: 'Sideway 1633'},
  { id: 12, name: 'William', address: 'Central st 954'}
]

********ORDER BY DESC*****
Use the DESC keyword to sort the result in a descending order.

Example
Sort the result reverse alphabetically by name:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  con.query("SELECT * FROM customers ORDER BY name DESC", function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
Save the code above in a file called "demo_db_orderby_desc.js" and run the file:

Run "demo_db_orderby_desc.js"

C:\Users\Your Name>node demo_db_orderby_desc.js
Which will give you this result:

[
  { id: 12, name: 'William', address: 'Central st 954'},
  { id: 14, name: 'Viola', address: 'Sideway 1633'},
  { id: 10, name: 'Vicky', address: 'Yellow Garden 2'},
  { id: 9, name: 'Susan', address: 'One way 98'},
  { id: 6, name: 'Sandy', address: 'Ocean blvd 2'},
  { id: 8, name: 'Richard', address: 'Sky st 331'},
  { id: 2, name: 'Peter', address: 'Lowstreet 4'},
  { id: 5, name: 'Michael', address: 'Valley 345'},
  { id: 1, name: 'John', address: 'Higheay 71'},
  { id: 4, name: 'Hannah', address: 'Mountain 21'},
  { id: 13, name: 'Chuck', address: 'Main Road 989'},
  { id: 7, name: 'Betty', address: 'Green Grass 1'},
  { id: 11, name: 'Ben', address: 'Park Lane 38'},
  { id: 3, name: 'Amy', address: 'Apple st 652'}
]

*****************mysql Delete***********
Delete Record
You can delete records from an existing table by using the "DELETE FROM" statement:

ExampleGet your own Node.js Server
Delete any record with the address "Mountain 21":

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "DELETE FROM customers WHERE address = 'Mountain 21'";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log("Number of records deleted: " + result.affectedRows);
  });
});
Notice the WHERE clause in the DELETE syntax: The WHERE clause specifies which record or records that should be deleted. If you omit the WHERE clause, all records will be deleted!

Save the code above in a file called "demo_db_delete.js" and run the file:

Run "demo_db_delete.js"

C:\Users\Your Name>node demo_db_delete.js
Which will give you this result:

Number of records deleted: 1

**************The Result Object ***************
When executing a query, a result object is returned.

The result object contains information about how the query affected the table.

The result object returned from the example above looks like this:

{
  fieldCount: 0,
  affectedRows: 1,
  insertId: 0,
  serverStatus: 34,
  warningCount: 0,
  message: '',
  protocol41: true,
  changedRows: 0
}
The values of the properties can be displayed like this:

Example
Return the number of affected rows:

console.log(result.affectedRows)
Which will produce this result:

1


******************My 
Sql Drop Table************
Delete a Table
You can delete an existing table by using the "DROP TABLE" statement:

ExampleGet your own Node.js Server
Delete the table "customers":

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "DROP TABLE customers";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log("Table deleted");
  });
});
Save the code above in a file called "demo_db_drop_table.js" and run the file:

Run "demo_db_drop_table.js"

C:\Users\Your Name>node demo_db_drop_table.js
Which will give you this result:

Table deleted.

Drop Only if Exist
If the the table you want to delete is already deleted, or for any other reason does not exist, you can use the IF EXISTS keyword to avoid getting an error.

Example
Delete the table "customers" if it exists:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "DROP TABLE IF EXISTS customers";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});

Drop Only if Exist
If the the table you want to delete is already deleted, or for any other reason does not exist, you can use the IF EXISTS keyword to avoid getting an error.

Example
Delete the table "customers" if it exists:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "DROP TABLE IF EXISTS customers";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
*****************My sql Update************
Update Table
You can update existing records in a table by using the "UPDATE" statement:

ExampleGet your own Node.js Server
Overwrite the address column from "Valley 345" to "Canyon 123":

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log(result.affectedRows + " record(s) updated");
  });
});
Notice the WHERE clause in the UPDATE syntax: The WHERE clause specifies which record or records that should be updated. If you omit the WHERE clause, all records will be updated!

Save the code above in a file called "demo_db_update.js" and run the file:

Run "demo_db_update.js"

C:\Users\Your Name>node demo_db_update.js
Which will give you this result:

1 record(s) updated

The Result Object
When executing a query, a result object is returned.

The result object contains information about how the query affected the table.

The result object returned from the example above looks like this:

{
  fieldCount: 0,
  affectedRows: 1,
  insertId: 0,
  serverStatus: 34,
  warningCount: 0,
  message: '(Rows matched: 1 Changed: 1 Warnings: 0',
  protocol41: true,
  changedRows: 1
}
The values of the properties can be displayed like this:

Example
Return the number of affected rows:

console.log(result.affectedRows)
Which will produce this result:

1

**************my sql limit**********
Limit the Result
You can limit the number of records returned from the query, by using the "LIMIT" statement:

ExampleGet your own Node.js Server
Select the 5 first records in the "customers" table:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "SELECT * FROM customers LIMIT 5";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});

Save the code above in a file called "demo_db_limit.js" and run the file:

Run "demo_db_limit.js"

C:\Users\Your Name>node demo_db_limit.js
Which will give you this result:

[
  { id: 1, name: 'John', address: 'Highway 71'},
  { id: 2, name: 'Peter', address: 'Lowstreet 4'},
  { id: 3, name: 'Amy', address: 'Apple st 652'},
  { id: 4, name: 'Hannah', address: 'Mountain 21'},
  { id: 5, name: 'Michael', address: 'Valley 345'}
]

Save the code above in a file called "demo_db_limit.js" and run the file:

Run "demo_db_limit.js"

C:\Users\Your Name>node demo_db_limit.js
Which will give you this result:

[
  { id: 1, name: 'John', address: 'Highway 71'},
  { id: 2, name: 'Peter', address: 'Lowstreet 4'},
  { id: 3, name: 'Amy', address: 'Apple st 652'},
  { id: 4, name: 'Hannah', address: 'Mountain 21'},
  { id: 5, name: 'Michael', address: 'Valley 345'}
]
********************Mysql Join***********
Join Two or More Tables
You can combine rows from two or more tables, based on a related column between them, by using a JOIN statement.

Consider you have a "users" table and a "products" table:

usersGet your own Node.js Server
[
  { id: 1, name: 'John', favorite_product: 154},
  { id: 2, name: 'Peter', favorite_product: 154},
  { id: 3, name: 'Amy', favorite_product: 155},
  { id: 4, name: 'Hannah', favorite_product:},
  { id: 5, name: 'Michael', favorite_product:}
]
products
[
  { id: 154, name: 'Chocolate Heaven' },
  { id: 155, name: 'Tasty Lemons' },
  { id: 156, name: 'Vanilla Dreams' }
]
These two tables can be combined by using users' favorite_product field and products' id field.

Example
Select records with a match in both tables:

var mysql = require('mysql');

var con = mysql.createConnection({
  host: "localhost",
  user: "yourusername",
  password: "yourpassword",
  database: "mydb"
});

con.connect(function(err) {
  if (err) throw err;
  var sql = "SELECT users.name AS user, products.name AS favorite FROM users JOIN products ON users.favorite_product = products.id";
  con.query(sql, function (err, result) {
    if (err) throw err;
    console.log(result);
  });
});
Note: You can use INNER JOIN instead of JOIN. They will both give you the same result.

Save the code above in a file called "demo_db_join.js" and run the file:

Run "demo_db_join.js"

C:\Users\Your Name>node demo_db_join.js
Which will give you this result:

[
  { user: 'John', favorite: 'Chocolate Heaven' },
  { user: 'Peter', favorite: 'Chocolate Heaven' },
  { user: 'Amy', favorite: 'Tasty Lemons' }
]
As you can see from the result above, only the records with a match in both tables are returned.

**************left join*********
If you want to return all users, no matter if they have a favorite product or not, use the LEFT JOIN statement:

Example
Select all users and their favorite product:

SELECT users.name AS user,
products.name AS favorite
FROM users
LEFT JOIN products ON users.favorite_product = products.id
Which will give you this result:

[
  { user: 'John', favorite: 'Chocolate Heaven' },
  { user: 'Peter', favorite: 'Chocolate Heaven' },
  { user: 'Amy', favorite: 'Tasty Lemons' },
  { user: 'Hannah', favorite: null },
  { user: 'Michael', favorite: null }
]
Right Join
If you want to return all products, and the users who have them as their favorite, even if no user have them as their favorite, use the RIGHT JOIN statement:

Example
Select all products and the user who have them as their favorite:

SELECT users.name AS user,
products.name AS favorite
FROM users
RIGHT JOIN products ON users.favorite_product = products.id
Which will give you this result:

[
  { user: 'John', favorite: 'Chocolate Heaven' },
  { user: 'Peter', favorite: 'Chocolate Heaven' },
  { user: 'Amy', favorite: 'Tasty Lemons' },
  { user: null, favorite: 'Vanilla Dreams' }
]
Note: Hannah and Michael, who have no favorite product, are not included in the result.