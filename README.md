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
* **Sample call** <br />
```json
curl --location --request DELETE 'http://127.0.0.1:5000/Customer' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTE0MTM1NywianRpIjoiMDgzYjAxNjMtYzZiZC00MDY0LThmOGQtMmIyMDc1OGQzMDJkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUwMWRiZmJjLTZmNjUtNDA1ZC1hZWI4LTFhNjc4YTBmOTYwNSIsIm5iZiI6MTcwOTE0MTM1NywiY3NyZiI6ImIzMWVmYTllLTE3NGYtNGYyMC1iODQzLWJjMjE2NmU0Y2RhNyIsImV4cCI6MTcwOTE0MTk1N30.69CyBjkZ1f8EKZf8IqSIBrwu-Ixmlvcm5BQ4qWKHYMc'
```

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

### Make payments
Customer pays their balance

* **URL** <br />
/Customer

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "payment": 1
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "balance": 5.1,
    "email": "email@gmail.com",
    "name": "Moustafa"
}
```

* **Error response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`

* **Sample call** <br />
```json
curl --location 'http://127.0.0.1:5000/Customer' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3NTQ2OCwianRpIjoiNTczMWU1OWEtZDlhNS00NGFmLThhZmUtYWJhZTkwMDc4ZDE5IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImUzZDYwMzQwLTJhMjItNDYzYS1hMzQyLWU1YzQxNmFiNGRhMiIsIm5iZiI6MTcwOTU3NTQ2OCwiY3NyZiI6IjkwMDgxMDFlLTQwZjEtNDIxNC1iYzkxLTgyNDRjNjVjMTJlYiIsImV4cCI6MTcwOTU3NjA2OH0.-YIrTDn3iYrtl1p-9_WcbtelLvhe6qiLkdUNPEQ1Ay0' \
--data '{
    "payment": 1
}'
```

### Create a supplier
Creates and return new suppliers

* **URL** <br />
/Suppliers

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
    "suppliers":[
        {
            "name": "Yousef",
            "email": "joe@gmail.com",
            "password": "joe"
        },
        {
            "name": "Mohamed",
            "email": "kebz@gmail.com",
            "password": "kebz"
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
        "email": "joe@gmail.com",
        "name": "Yousef"
    },
    {
        "email": "kebz@gmail.com",
        "name": "Mohamed"
    }
]
```

* **Error response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}` <br />
  OR
  * **Code:** 409 <br />
  **Content:** `{"message": "supplier already exists"}`

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Suppliers' \
--header 'Content-Type: application/json' \
--data-raw '{
    "suppliers":[
        {
            "name": "Yousef",
            "email": "joe@gmail.com",
            "password": "joe"
        },
        {
            "name": "Mohamed",
            "email": "kebz@gmail.com",
            "password": "kebz"
        }
    ]
}'
```

### Get all suppliers
Returns all suppliers in database, for development use only

* **URL** <br />
/Suppliers

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
        "email": "joe@gmail.com",
        "name": "Yousef"
    },
    {
        "email": "kebz@gmail.com",
        "name": "Mohamed"
    }
]
```

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Suppliers'
```

### Update Supplier information
Changes supplier name

* **URL** <br />
/Supplier

* **Method** <br />
PUT

* **URL Params** <br />
None

* **Data Params** <br />
**Required:** <br />
```json
{
    "name": "Moustafa"
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:**
```json
{
"balance": 0.0,
"email": "joe@gmail.com",
"name": "Moustafa"
}
```

* **Error Response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`

* **Sample Call:** <br />
```json
curl --location --request PUT 'http://127.0.0.1:5000/Supplier' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTE0MTM1NywianRpIjoiMDgzYjAxNjMtYzZiZC00MDY0LThmOGQtMmIyMDc1OGQzMDJkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUwMWRiZmJjLTZmNjUtNDA1ZC1hZWI4LTFhNjc4YTBmOTYwNSIsIm5iZiI6MTcwOTE0MTM1NywiY3NyZiI6ImIzMWVmYTllLTE3NGYtNGYyMC1iODQzLWJjMjE2NmU0Y2RhNyIsImV4cCI6MTcwOTE0MTk1N30.69CyBjkZ1f8EKZf8IqSIBrwu-Ixmlvcm5BQ4qWKHYMc' \
--data '{
    "name": "Moustafa"
}'
```

### Delete a supplier
Removes a supplier from database

* **URL** <br />
/Supplier

* **Method** <br />
DELETE

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** `{"message": "Supplier deleted"}`

* **Error Response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "Supplier not found"}`

* **Sample call** <br />
```json
curl --location --request DELETE 'http://127.0.0.1:5000/Supplier' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTE0MTM1NywianRpIjoiMDgzYjAxNjMtYzZiZC00MDY0LThmOGQtMmIyMDc1OGQzMDJkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUwMWRiZmJjLTZmNjUtNDA1ZC1hZWI4LTFhNjc4YTBmOTYwNSIsIm5iZiI6MTcwOTE0MTM1NywiY3NyZiI6ImIzMWVmYTllLTE3NGYtNGYyMC1iODQzLWJjMjE2NmU0Y2RhNyIsImV4cCI6MTcwOTE0MTk1N30.69CyBjkZ1f8EKZf8IqSIBrwu-Ixmlvcm5BQ4qWKHYMc'
```

### Create a product
Create and return products

* **URL** <br />
/Supplier/Products

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "products": [
        {
            "name": "banana",
            "quantity": 10,
            "price": 1.1
        },
        {
            "name": "apple",
            "quantity":10,
            "price": 5
        }
    ]
}
```

* **Success response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
[
    {
        "id": "f3791325-c73e-46f9-ab84-140417310cc2",
        "name": "banana",
        "price": 1.1,
        "quantity": 10
    },
    {
        "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
        "name": "apple",
        "price": 5.0,
        "quantity": 10
    }
]
```

* **Error response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "Supplier not found"}` <br />
    OR
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}` <br />
    OR
  * **Code:** 409 <br />
  **Content:** `{"message": "product already exists"}` <br />

* **Sample call:** <br />
```json
curl --location 'http://127.0.0.1:5000/Supplier/Products' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3NTMxMCwianRpIjoiMjBmYWRhNmMtYTU0OC00Yjc2LWEwZTgtNzM0N2YxM2U1NzNkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTU3NTMxMCwiY3NyZiI6ImZjYjI0N2JhLWFjOTItNGIxMi05N2UyLTZlZTBhY2I2MGE3MSIsImV4cCI6MTcwOTU3NTkxMH0.dYu5qZJeuq8U4mLVaV7V7_uF5dZ8w-BbTJhRlX9sVLg' \
--data '{
    "products": [
        {
            "name": "banana",
            "quantity": 10,
            "price": 1.1
        },
        {
            "name": "apple",
            "quantity":10,
            "price": 5
        }
    ]
}'
```

### Get Products
Returns all products of supplier

* **URL** <br />
/Supplier/Products

* **Method** <br />
GET

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
[
    {
        "id": "f3791325-c73e-46f9-ab84-140417310cc2",
        "name": "banana",
        "price": 1.1,
        "quantity": 2
    },
    {
        "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
        "name": "apple",
        "price": 5.0,
        "quantity": 1
    }
]
```

* **Error response** <br />
  * **Code:** 404 <br />
    **Content:** `{"message": "Supplier not found"}`

### Update product
Change a product's name, quantity, and price

* **URL** <br />
/Customer/Product

* **Method** <br />
PUT

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
    "name": "apple",
    "quantity": 10,
    "price": 0.9
}
```

* **Success response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
    "name": "apple",
    "price": 0.9,
    "quantity": 10
}
```

* **Error response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "product not found"}`
    OR
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`
    OR
  * **Code:** 403 <br />
  **Content:** `{"message": "You do not have permission for this function"}`

* **Sample call** <br />
```json
curl --location --request PUT 'http://127.0.0.1:5000/Supplier/Product' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3Njg2OSwianRpIjoiYjExOGM0NjYtMjZmYS00MDY0LTlkYzUtNWFmOTU2NGNhMGRkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTU3Njg2OSwiY3NyZiI6ImI5ZDUzZGRiLTI0YTgtNDI2Zi04ZTZmLWEzMGI1NmUxY2MxYSIsImV4cCI6MTcwOTU3NzQ2OX0.KafVXCVHaqxQRgcfrszEgFhwr32p2lAfM1RE3UOHI3c' \
--data '{
    "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
    "name": "apple",
    "quantity": 10,
    "price": 0.9
}'
```

### Delete a product
Delete a product of a supplier

* **URL** <br />
/Supplier/Product

* **Method** <br />
DELETE

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f"
}
```

* **Success response** <br />
**Code:** 200 <br />
**Content:** `{"message": "product deleted"}`

* **Error response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "product not found"}`

* **Sample call** <br />
```json
curl --location --request DELETE 'http://127.0.0.1:5000/Supplier/Product' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3Njg2OSwianRpIjoiYjExOGM0NjYtMjZmYS00MDY0LTlkYzUtNWFmOTU2NGNhMGRkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTU3Njg2OSwiY3NyZiI6ImI5ZDUzZGRiLTI0YTgtNDI2Zi04ZTZmLWEzMGI1NmUxY2MxYSIsImV4cCI6MTcwOTU3NzQ2OX0.KafVXCVHaqxQRgcfrszEgFhwr32p2lAfM1RE3UOHI3c' \
--data '{
    "id": "0d5878db-8064-47b7-84ec-f6ba9d35169f"
}'
```

### Supplier make shipment
Supplier ships products to inventory table

* **URL** <br />
/Supplier/Shipments

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "products":[
        {
            "productId": "f3791325-c73e-46f9-ab84-140417310cc2",
            "name": "banana",
            "quantity": 8
        },
        {
            "productId": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
            "name": "apple",
            "quantity": 9
        }
    ]
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "date": "Mon, 04 Mar 2024 12:03:08 GMT",
    "id": "3202c03b-fe92-489f-a96e-d51585399ac9",
    "products": [
        {
            "name": "banana",
            "quantity": 8
        },
        {
            "name": "apple",
            "quantity": 9
        }
    ]
}
```

* **Error response** <br />
  * **Code:** 404 <br />
  **Content:** `{"message": "product not found"}`
    OR
  * **Code:** 400 <br />
  **Content:** `{"message": "invalid input}`

* **Sample call** <br />
```json
curl --location 'http://127.0.0.1:5000/Supplier/Shipments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3NTMxMCwianRpIjoiMjBmYWRhNmMtYTU0OC00Yjc2LWEwZTgtNzM0N2YxM2U1NzNkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTU3NTMxMCwiY3NyZiI6ImZjYjI0N2JhLWFjOTItNGIxMi05N2UyLTZlZTBhY2I2MGE3MSIsImV4cCI6MTcwOTU3NTkxMH0.dYu5qZJeuq8U4mLVaV7V7_uF5dZ8w-BbTJhRlX9sVLg' \
--data '{
    "products":[
        {
            "productId": "f3791325-c73e-46f9-ab84-140417310cc2",
            "name": "banana",
            "quantity": 8
        },
        {
            "productId": "0d5878db-8064-47b7-84ec-f6ba9d35169f",
            "name": "apple",
            "quantity": 9
        }
    ]
}'
```

### View shipment
view shipment of supplier

* **URL** <br />
/Supplier/Shipment

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
        "date": "Mon, 04 Mar 2024 12:03:08 GMT",
        "id": "3202c03b-fe92-489f-a96e-d51585399ac9",
        "products": [
            {
                "name": "banana",
                "quantity": 8
            },
            {
                "name": "apple",
                "quantity": 9
            }
        ]
    }
]
```

* **Error Response** <br />
  **Code:** 400 <br />
  **Content:** `{"message": "supplier not found"}`

* **Sample Call** <br />
```json
curl --location 'http://127.0.0.1:5000/Supplier/Shipments' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU3OTA3MiwianRpIjoiYTcyZDJkNGQtZWNmYy00N2Y1LTllOWYtOTA0OWQ4YmQ5NGQ1IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTU3OTA3MiwiY3NyZiI6IjZiYzE0MWM1LTExNzUtNDRiYi1iOTY0LTIzYmZiYzRlNmY5NSIsImV4cCI6MTcwOTU3OTY3Mn0.brceUiMNhoE4X-vSWKXHT16WB7d6hEqTeh2HknABrXU'
```

### Login
A supplier or customer logs in to their account

* **URL** <br />
/login

* **Method** <br />
POST

* **URL Params** <br />
None

* **Data Params** <br />
**Required** <br />
```json
{
    "email": "joe@gmail.com",
    "password": "joe",
    "user": "supplier"
}
```

* **Success Response** <br />
**Code:** 200 <br />
**Content:** <br />
```json
{
    "message": "Hello Yousef, you are logged in!",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTY0NjUxMywianRpIjoiZDBkZmRlN2YtYThjMy00NDlhLWI0ODktN2Q4OTJmNzI2Y2VhIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM0ZDM0NzFlLTI5ZjEtNGZlMS05YWM1LThkOTZiNzU2MjU0MCIsIm5iZiI6MTcwOTY0NjUxMywiY3NyZiI6ImY0NTQxMjJmLTNhMzItNDBmNC05OGUxLTRhNDc5MzRhZjRjMCIsImV4cCI6MTcwOTY0NzExM30.qUGsrj-F1Z296tBjf5GBNv2xTBipPit9xM7dznYAAcs"
}
```

* **Error Response** <br />
  * **Code:** 400 <br />
  **Content:** `{"message": "Invalid input"}`
    OR
  * **Code:** 404 <br />
  **Content:** `{"message": "Incorrect password or email"}`

* **Sample Call:** <br />
```json
curl --location 'http://127.0.0.1:5000/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email": "joe@gmail.com",
    "password": "joe",
    "user": "supplier"
}'
```

### Logout
Supplier or customer logs out of their account

* **URL** <br />
/logout

* **Method** <br />
DELETE

* **URL Params** <br />
None

* **Data Params** <br />
None

* **Success Response** <br />
**Code:** 200 <br />
**Content:** `{"message": "logged out!"}`

* **Sample Call:** <br />
```json
curl --location --request DELETE 'http://127.0.0.1:5000/logout' \
--header 'Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTcwOTU0NzgxNSwianRpIjoiMjM1NmViYTUtMDFhOS00Y2M2LWE3ZmItZTMwMzFkNjMxN2FkIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6ImM3MTcwYmZkLWJlZjYtNDgxOC04ODliLWI1MTU0NmI2NmZlYSIsIm5iZiI6MTcwOTU0NzgxNSwiY3NyZiI6IjYyOTM1ODJlLTRmNzgtNGM4Ny05ZGNmLWY3YzIwYTVmMTMwNiIsImV4cCI6MTcwOTU0ODQxNX0.kyHabv-MOZSbmGu_iIhz7rLuuEedjB-Ztoa_UWYf4k4'
```
