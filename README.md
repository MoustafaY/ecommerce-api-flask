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




