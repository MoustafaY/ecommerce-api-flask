# Ecommerce simulator

## Objective
The goal of this project is to keep track of products as they are moved from one table to another in an ecommerce environment. The project uses flask and sqlalchemy to create api calls that achieve that goal, the project also uses sqlite for its database, jwt tokens for authentication, and pytest for unit testing.

## Dependencies
All project libraries can be found in the requirements.txt file.

## Unit test instructions
The project uses pytest for its unit tests. When in root directory use the `pytest` command to run the unit tests. There are 31 unit tests that test each api call for its success and failure responses.

## API calls

### Create a customer
Creates and return new customers

* **URL** <br />
/Customers

* **Method** <br />
POST

* **URL Params** <br />
None

* **JWT required** <br />
None

* **Data Params** <br />
**Required:** <br />
```json
{
    "customers":[
        {
            "name": "Moustafa",
            "email": "email@gmail.com",
            "password": "pass"
        },
        {
            "name": "Lily",
            "email": "lil@gmail.com",
            "password": "lil"
        }
    ]
}
```

* **Success Response** <br />
  **Code:** 200 <br />
  **Content:** <br />
  ```json
  [
      {
          "balance": 0.0,
          "email": "email@gmail.com",
          "name": "Moustafa"
      },
      {
          "balance": 0.0,
          "email": "lil@gmail.com",
          "name": "Lily"
      }
  ]
  ```

* **Error response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid error"}` <br />
  OR
  * **Code:** 409 <br />
  **Content:** `{"message": "customer already exists"}`

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Customers' \
--header 'Content-Type: application/json' \
--data-raw '{
    "customers":[
        {
            "name": "Moustafa",
            "email": "email@gmail.com",
            "password": "pass"
        },
        {
            "name": "Lily",
            "email": "lil@gmail.com",
            "password": "lil"
        }
    ]
}'
```

### Get all customers
Returns all customers in database, for development use only

* **URL** <br />
/Customers

* **Method** <br />
GET

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
[
    {
        "balance": 0.0,
        "email": "email@gmail.com",
        "name": "Moustafa"
    },
    {
        "balance": 0.0,
        "email": "lil@gmail.com",
        "name": "Lily"
    }
]
```

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Customers'
```

### Update Customer information
Changes customer name

* **URL** <br />
/Customer

* **Method** <br />
PUT

* **URL Params** <br />
None

* **Data Params** <br />
**Required:** <br />
```json
{
    "name": "suality"
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:**
```json
{
"balance": 0.0,
"email": "email@gmail.com",
"name": "suality"
}
```

* **Error Response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`

* **Sample Call:** <br />
```json
curl --location --request PUT 'http://127.0.0.1:5000/Customer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0NjEyMiwianRpIjoiNDMyZGM4MGQtYzI5Mi00ZmNiLTkzNzUtMTU4NzM4YTBjZjlkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0NjEyMiwiY3NyZiI6ImQ5MDc4YzI5LWM0MmItNDE0ZS05YWRhLWRjNGYxNzNmOWI1ZSIsImV4cCI6MTcwOTU0NjcyMn0.hs1AMJ9TFjI23w9PT62_NB26xkM1tkV2vx-sRDMmETw' \
--data '{
    "name": "suality"
}'
```

### Delete a customer
Removes a customer from database

* **URL** <br />
/Customer

* **Method** <br />
DELETE

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** `{"message": "Customer deleted"}`

* **Error Response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "Customer not found"}`

### Add to shopping cart
A customer adds a product from inventory to shopping cart

* **URL** <br />
/Customer/ShoppingCart

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
**Required:** <br />
```json
{
    "products": [
        {
            "id": "aa4ff3d7-db92-4c84-a840-a70e7651df03",
            "quantity": 2
        },
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "quantity": 3
        }
    ]
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "id": "d78a2142-fc64-476d-b77c-61cf121f98b8",
    "products": [
        {
            "id": "aa4ff3d7-db92-4c84-a840-a70e7651df03",
            "name": "banana",
            "price": 1.1,
            "quantity": 2
        },
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "name": "apple",
            "price": 5.0,
            "quantity": 3
        }
    ],
    "sum": 17.2
}
```

* **Error Response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "invalid input"}`
  OR
  * **Code: 404** <br />
  **Content:** `{"message": "product not found"}`

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Customer/ShoppingCart' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0NzkzMiwianRpIjoiYzEyMWMxNzUtZWNkZS00MWY0LTg2MWUtZmMxNTIyODZiY2UxIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0NzkzMiwiY3NyZiI6IjUxZTA3ZmZjLTgyODQtNGI3NC05NWU5LWI0M2M3MzEzNWYxNyIsImV4cCI6MTcwOTU0ODUzMn0.bQcT0Z_ZxvdZNsZYMB5DdHmI3dUf2IQGfrbUJcq92oc' \
--data '{
    "products": [
        {
            "id": "aa4ff3d7-db92-4c84-a840-a70e7651df03",
            "quantity": 2
        },
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "quantity": 3
        }
    ]
}'
```

### View shopping cart
Returns shopping cart of customer

* **URL** <br />
/Customer/ShoppingCart

* **Method** <br />
GET

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "id": "d78a2142-fc64-476d-b77c-61cf121f98b8",
    "products": [
        {
            "id": "aa4ff3d7-db92-4c84-a840-a70e7651df03",
            "name": "banana",
            "price": 1.1,
            "quantity": 2
        },
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "name": "apple",
            "price": 5.0,
            "quantity": 3
        }
    ],
    "sum": 17.2
}
```

* **Error Response** <br />
  * **Code:** 404 <br />
  **Content** `{"message": "Customer not found"}`

* **Sample call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Customer/ShoppingCart' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0NzkzMiwianRpIjoiYzEyMWMxNzUtZWNkZS00MWY0LTg2MWUtZmMxNTIyODZiY2UxIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0NzkzMiwiY3NyZiI6IjUxZTA3ZmZjLTgyODQtNGI3NC05NWU5LWI0M2M3MzEzNWYxNyIsImV4cCI6MTcwOTU0ODUzMn0.bQcT0Z_ZxvdZNsZYMB5DdHmI3dUf2IQGfrbUJcq92oc'
```

### Remove from shopping cart
Customer removes product from shopping cart

* **URL** <br />
/Customer/ShoppingCart

* **Method** <br />
DELETE

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "productId": "aa4ff3d7-db92-4c84-a840-a70e7651df03"
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "id": "d78a2142-fc64-476d-b77c-61cf121f98b8",
    "products": [
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "name": "apple",
            "price": 5.0,
            "quantity": 3
        }
    ],
    "sum": 15.0
}
```

* **Error Response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`
  OR
  * **Code:** 404 <br />
  **Content:** `{"message": "Product not found"}`

* **Sample call:** <br />
```json
curl --location --request DELETE 'http://127.0.0.1:5000/Customer/ShoppingCart' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0ODc1NiwianRpIjoiYWUzNGI5NDEtY2M3Mi00ZTI1LTljYzAtYzJkOGUxZWI3YmM1IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0ODc1NiwiY3NyZiI6IjdhMDMwNjlhLWRhYzEtNDI1My05NWFhLTEwMDNjYzkyYTBkNyIsImV4cCI6MTcwOTU0OTM1Nn0.p_8Nm4RzwC1oaW5VawFScTWfb21OuJEcN_nDYvBw9ug' \
--data '{
    "productId": "aa4ff3d7-db92-4c84-a840-a70e7651df03"
}'
```

### Change product in shopping cart
Customer changes product quantity in shopping cart

* **URL** <br />
/Customer/ShoppingCart

* **Method** <br />
PUT

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "products": [
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "quantity": 5
        }
    ]
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
"id": "d78a2142-fc64-476d-b77c-61cf121f98b8",
"products": [
    {
        "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
        "name": "apple",
        "price": 5.0,
        "quantity": 5
    }
],
"sum": 25.0
}
```

* **Error Response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "product not found"}`
    OR
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`

* **Sample call:** <br />
```json
curl --location --request PUT 'http://127.0.0.1:5000/Customer/ShoppingCart' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0ODc1NiwianRpIjoiYWUzNGI5NDEtY2M3Mi00ZTI1LTljYzAtYzJkOGUxZWI3YmM1IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0ODc1NiwiY3NyZiI6IjdhMDMwNjlhLWRhYzEtNDI1My05NWFhLTEwMDNjYzkyYTBkNyIsImV4cCI6MTcwOTU0OTM1Nn0.p_8Nm4RzwC1oaW5VawFScTWfb21OuJEcN_nDYvBw9ug' \
--data '{
    "products": [
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "quantity": 5
        }
    ]
}'
```

### Customer create order
Customer creates order, products in shopping cart are deducted from inventory and added to transcripts

* **URL** <br />
/Customer/Transcripts

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "id": "30c0a1fa-705a-45a1-b287-5717144ec3e6",
    "products": [
        {
            "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
            "name": "apple",
            "price": 5.0,
            "quantity": 5
        }
    ],
    "sum": 25.0
}
```

* **Error Response** <br />
  * **Code:** 404 <br />
  * **Content:** `{"message": "Product not found"}`

* **Sample Call:** <br />
```json
curl --location --request POST 'http://127.0.0.1:5000/Customer/Transcripts' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0OTUwNSwianRpIjoiOGMwOTAyODEtYzFiNS00YmZjLTk3OWMtYzdjNGQwZmI4NzBiIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU0OTUwNSwiY3NyZiI6IjVlMjRjOTdjLTE5ZmUtNDJiZS1iMWMwLTJjY2UzMzFkYmQwMyIsImV4cCI6MTcwOTU1MDEwNX0.btLm8_ma6M88L5i_56IKJKYLT0J41EzylCNlZSupCAA'
```

### Customer view transcripts
Returns customer transcript history

* **URL** <br />
/Customer/Transcripts

* **Method** <br />
GET

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
[
    {
        "id": "30c0a1fa-705a-45a1-b287-5717144ec3e6",
        "products": [
            {
                "id": "9c37b607-75fe-460d-9aae-2f2275ca53f5",
                "name": "apple",
                "price": 5.0,
                "quantity": 5
            }
        ],
        "sum": 25.0
    }
]
```

* **Error Response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "Customer not found"}`

* **Sample call** <br />
```json
curl --location 'http://127.0.0.1:5000/Customer/Transcripts' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU1MDAxMCwianRpIjoiNzkxZDE0MTEtYzY5Zi00OGRjLWE0YzYtMWM2OGUwZWEwNzAwIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImZhNTI5ZTVhLTM2ZjAtNDA5YS1hZjUwLWFjZjFiZGUxOTdmYyIsIm5iZiI6MTcwOTU1MDAxMCwiY3NyZiI6ImVjYzE5MmM0LTIzOWMtNDcxMy1hODBkLTZjOTkzNjg4NTBhYiIsImV4cCI6MTcwOTU1MDYxMH0.ja-wuownTHFGkyD-rEGGk0bBoQBTCqOG5aCrwXpN8Kw'
```











    
