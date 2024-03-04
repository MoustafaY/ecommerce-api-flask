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
