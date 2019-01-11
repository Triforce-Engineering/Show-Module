# Project Name

> SDC Amazon Project

## Related Projects

  - https://github.com/ChampsOfTheSun/reviews-service
  - https://github.com/ChampsOfTheSun/vrtobar-service
  - https://github.com/ChampsOfTheSun/jhods16-service

## Table of Contents

1. [Usage](#Usage)
1. [Requirements](#requirements)
1. [Development](#development)

## SetUp Instructions

> Navigate to db/db.js to configure the mySql username and password to match your local machine
> From the root of the directory run the following commands:
  > 'npm run start' (starts a nodemon server on port 3004)
  > 'npm run schema' 
    >Enter your own mySql password when prompted
  > 'npm run seed-products' (seeds the products table)
  > 'npm run seed-photos' (seeds the photos table)

## Requirements

An `nvmrc` file is included if using [nvm](https://github.com/creationix/nvm).

- Node 6.13.0
- etc

## Development

### Installing Dependencies

From within the root directory:

```sh
npm install
```

### CRUD API's
Create: 
> app.post(/photos/:productId)

> app.post(/products/:productId)

> --> Sample Create Helper Function

> const addProduct = (obj) => {
>   return new Promise((resolve, reject) => {
>     const queryString = `INSERT INTO products (product_title, vendor_name, review_average, review_count, answered_questions, list_price, price, prime, description) VALUES ('${obj.product_title}', '${obj.vendor_name}', ${obj.review_average}, ${obj.review_count}, ${obj.answered_questions}, '${obj.list_price}', '${obj.price}', ${obj.prime}, '${obj.description}')`;
>     db.query(queryString, (err, res) => {
>       if (err) {
>         console.log(queryString);
>         console.log(err);
>         reject(err);
>       } else {
>         resolve(res);
>       }
>     });
>   });
> };

Read: 
 > app.get(/photos/:productId)

 > app.get(/products/:productId)

> --> Sample Read Helper Function

> const getProducts = (productID) => {
>   return new Promise((resolve, reject) => {
>     const queryString = 'SELECT * FROM products WHERE productID = ?';
>     const params = [productID];
>     db.client.query(queryString, params, (err, res) => {
>       if (err) {
>         reject(err);
>       } else {
>         resolve(res);
>       }
>     });
>   });
> };

Update: 
 > app.put(/photos/:productId)

 > app.put(/products/:productId)

> --> Sample Update Helper Function

 > const updateProduct = (product, productID) => {
>   return new Promise((resolve, reject) => {
>     db.query(`UPDATE products SET product_title=${product.product_title}, vendor_name=${product.vendor_name}, review_average=${product.review_average}, review_count = ${product.review_count}, answered_questions = ${product.answered_questions}, list_price = ${product.list_price}, price = ${product.price}, description = ${product.description} WHERE productID=${productID}`, (err, res) => {
>       if (err) {
>         reject(err);
>       } else {
>         resolve(res);
>       }
>     });
>   });
> };

Delete:
 > app.delete(/photos/:productId)

 > app.delete(/products/:productId)

> --> Sample Delete Helper Function

 > const deleteProducts = (productID) => {
 >   return new Promise((resolve, reject) => {
 >     db.query(`DELETE FROM products WHERE productID = ${productID}`, (err, res) => {
 >       if (err) {
 >         reject(err);
 >       } else {
 >         resolve(res);
 >       }
 >     });
 >   });
 > };