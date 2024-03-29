# Description
Using NodeJS Framework and MySQL BackEnd language,\
We can create our Local Databse..

Some simple steps for working \
We will be doing the __CRUD__ operations in NodeJS with MySql Query..



#### Let's Begain ...

# Step 1 :

Create a folder and open terminal from vscode in that folder . Then type : 

```
npm init
```

After that keep pressing enter button to keep the default config .. 


# Step 2 :


in terminal now type : 

```
npm install express mysql body-parser
```

It’ll install the necessary packages tempurary in Project..



# Step 3 :

install Dev-dependences : 

```
npm install --save-dev nodemon
```


# Step 4 : 

Edit the package.json file ..
in the 

__"scripts": {__\
__"test": "echo \"Error: no test specified\" && exit 1"__\
__},__

add this line above the __“test”__ ..

__“ start ” : “nodemon app.js”__

_app.js is only the file name  !!_




# Step 5 : 

back to app.js file .. 


add this code  :
```
const express = required(‘express’) ;
const mysql = required(‘mysql’);
const bodyParser = required(‘body-parser’);
const port = 5000; {as you wish}
const app = express();
app.use(bodyParser.urlencoded({extended : false}));
app.use(bodyParser.json());

// Listen to the necessary port ..
app.listen(port,( ) => {
console.log(`App is running on the port ${port});
}
```



# Step 6 : 

Now create a DB in using XAMPP with MySQL .. 


a sample DB will be like : 




# Step 7 : 
back to the App.Js …
 
We have to make a pool to create a bridge between our environment and DB ..

Add this code to create a pool …..

```
const pool = mysql.createPool ( {
connectionLimit	: 10,
host			: ‘localhost’,
user			: ‘root’,
password		: ‘ ’,
database		: ‘google’
} );
```


# Step 8 :

All the pre-requirement is now ready for implementing the SQL queries from NodeJS..


## Can do 8.1 


*Get all the elements from database …*


method : __GET__\
purpose : fetch all the data from the database …\
query : __SELECT * FROM products__

code : 
```
app.get( ‘ ’ ,( req ,res ) => {
	
	pool.getConnection((err,connection) => {
	if(err) throw err;
		
connection.query( ‘ SELECT * FROM products ’ , (err , rows) => {
	connection.release();

	if(!err) res.send(rows);
else console.log(err);
});
});
});
```

__OutPut :__\
<img width="337" alt="image" src="https://user-images.githubusercontent.com/91305837/197471298-551f1fdc-8c8c-48b0-9aeb-ecdb6a7a4c39.png">




## Can do 8.2


Get a specific element from the database …


method : __GET__\
purpose : fetch only a object from the database …\
query : __SELECT FROM products WHERE id = ?__

Note: here in get : 
 
/:id -> is the id that we are searching and it send from url …

code : 
```
app.get( ‘/:id ’ ,( req ,res ) => {
	
	pool.getConnection((err,connection) => {
	if(err) throw err;
		
connection.query( ‘ SELECT * FROM products WHERE id = ? ’ , [req.params.id], (err , rows) => {
	connection.release();

	if(!err) res.send(rows);
else console.log(err);
});
});
});
```

__OutPut :__\
<img width="337" alt="image" src="https://user-images.githubusercontent.com/91305837/197472044-9790fa3d-b3ae-434f-9674-dca2ce257ab7.png">



## Can do 8.3


Delete a specific element from the database …


method : __DELETE__\
purpose : delete only an object from the database …\
query : __DELETE FROM products WHERE id = ?__

code : 
```
app.delete( ‘/:id ’ ,( req ,res ) => {
	
	pool.getConnection((err,connection) => {
	if(err) throw err;
		
connection.query( ‘ DELETE FROM products WHERE id = ? ’ , [req.params.id], (err , rows) => {
	connection.release();

	if(!err) res.send(`record id ${[req.params.id]} has been deleted`);
else console.log(err);
});
});
});
```

__Output :__\
<img width="435" alt="image" src="https://user-images.githubusercontent.com/91305837/197472595-42875f1d-0e3c-413d-84b7-11bf6e4abcc0.png">



## Can do 8.4

Add an element to the database …


method : __POST__\
purpose : add an object to the database at the end…\
query : __INSERT FROM products SET ?__

code : 
```
app.post('',(req,res)=> {
   pool.getConnection((err,connection) => {
       if (err) throw err;
 
       const params = req.body;
 
       connection.query('INSERT INTO products SET ?',params,(err,rows) => {
           connection.release();
          
           if(!err) res.send(`new object added to the database !`);
           else console.log(err);
       });
   });
});
```

__Output :__\
<img width="435" alt="image" src="https://user-images.githubusercontent.com/91305837/197473191-446ab9a1-40ab-4f06-83d6-7597280ceac0.png">



## Can do 8.5

Update an existing elements property to the database …


method : __PUT__\
purpose : update an object's property in DB.\
query : __UPDATE products SET drive = ?, contacts = ?, map = ? WHERE id = ?__

code : 
```
app.put('',(req,res)=> {
   pool.getConnection((err,connection) => {
       if (err) throw err;
 
       const {id,drive,contacts,map} = req.body;
       connection.query('UPDATE products SET drive = ?, contacts = ?, map = ? WHERE id = ?',[id,drive,contacts,map],(err,rows) => {
           connection.release();
          
           if(!err) res.send(`Block with drive ${drive} is updated`);
           else console.log(err);
       });
   });
});
```

__Output :__\

<img width="435" alt="image" src="https://user-images.githubusercontent.com/91305837/197473761-402fc726-8559-43d6-8e29-5e5c3d120c1c.png">
