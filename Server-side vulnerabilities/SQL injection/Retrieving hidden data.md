# Retrieving hidden data

Consider a shopping application that allows users to filter products by category. When a user clicks on the Gifts category, their browser requests the following URL:

```
https://insecure-website.com/products?category=Gifts
```

To fetch the matching products, the back-end application constructs and executes a SQL query like this:

```
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

## Breaking Down the Query

This query instructs the database to return:

- **All columns (`*`)**: Every detail associated with each matching product.

- **From the `products` table**: The table storing all store inventory.

- **Where `category = 'Gifts'`**: Filters results strictly to the user-requested category.

- **`And released = 1`**: An internal business-logic restriction used to ensure only publicly launched products are displayed. Unreleased or draft products are stored in the same table with `released = 0`, keeping them hidden from ordinary shoppers.

## Why This Query Structure Is Vulnerable

- **Direct String Concatenation**: The `category` parameter from the URL (`Gifts`) is inserted directly inside single quotes (`'...'`) in the WHERE clause without parameterisation.

- **Logic Bypass via SQL Comments**: Because the `AND released = 1` condition appears after the user-supplied `category` parameter, an attacker who breaks out of the single quotes can inject a SQL comment sequence (`--`) to strip away the `AND released = 1` check entirely forcing the database to return both released (`1`) and unreleased (`0`) products.
  
