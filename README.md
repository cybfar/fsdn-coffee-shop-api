# COFFEE SHOP API : Final Project

## Coffee Shop

Coffee Shop is a cafe where students can order drinks, socialize, and study.


## Getting Started
### Pre-requisites and Local Development

The project is divided into two parts.
A backend part made in Flask and a frontend part made in Ionic.
Developers using this project should already have Python, pip, node and Ionic installed on their local machines.
### Frontend

The [frontend](./frontend/) directory contains a complete Ionic frontend to consume the data from the Flask server.
To start the frontend, run the following commands from the frontend folder:
    
    npm install //To install dependencies
    ionic serve //To run the frontend
The frontend will run on localhost:8100


### Backend

The [backend](./backend) directory contains a Flask and SQLAlchemy server.
To setup the Trivia API, install the required dependencies by navigating to the `/backend` directory and run:

```bash
pip install -r requirements.txt
```

#### Set up the Database

To initialize the database, uncomment the following line in `backend/src/api.py`

```bash
#db_drop_and_create_all()
```
This must be uncommented only for the first run


#### Run the application
To run the application run the following commands from `backend/src/`:

```bash
export FLASK_APP=api.py
export FLASK_DEBUG=On
flask run
```
The `FLASK_DEBUG=On` will detect file changes and restart the server automatically.
The application is run on http://127.0.0.1:5000/ by default.


## API Reference
### Getting Started

- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://127.0.0.1:5000/.

- Authentication: This version of the application require authentication and authorization for some endpoints.

### Error Handling

Errors are returned as JSON objects in the following format:

```json
{
  "success": False,
  "error": 422,
  "message": "unprocessable",
}
```

The API will return three error types when requests fail (The message is sent with a specific description of the error):

  - 400: Bad Request
  - 401: Authentication Error
  - 403: Forbiden
  - 404: Resource Not Found
  - 405: Method not allowed
  - 422: Not Processable
  - 422: Not Processable

### Endpoints

#### Get all drinks

```http
GET /drinks
```

- General :
    - Fetch all drinks
    - Return the drink.short() data representation and success value
- Sample : `curl http://127.0.0.1:5000/drinks`
- This endpoint does not require authentication 

```json
{
  "drinks": [
    {
      "id": 1,
      "recipe": [
        {
          "color": "blue",
          "parts": 1
        }
      ],
      "title": "water"
    }
  ],
  "success": true
}
```

#### Get all drinks with details

```http
GET /drinks-detail
```

- General :
    - Fetch all drinks
    - Return the drink.long() data representation and success value
    - This endpoint require authentication 
    - Require the ``'get:drinks-detail'`` permission
- Sample : `curl http://127.0.0.1:5000/drinks-detail -H "Authorization: Bearer {AUTH_TOKEN}" `

```json
{
  "drinks": [
    {
      "id": 1,
      "recipe": [
        {
          "color": "blue",
          "name": "water",
          "parts": 1
        }
      ],
      "title": "water"
    }
  ],
  "success": true
}
```

#### Post a drink

```http
POST /drinks
```

- General :
    - Create a new Drink in the drinks table
    - Return the newly created drink and success value
    - This endpoint require authentication 
    - Require the ``'post:drinks'`` permission
- Sample : `curl -X POST "http://127.0.0.1:5000/drinks" -H "Content-Type: application/json" -d '{"title": "Water 2","recipe": {"name": "Water","color": "blue","parts": 1}}' -H "Authorization: Bearer {AUTH_TOKEN}" `

```json
{
    "drinks": [
        {
            "id": 2,
            "recipe": [
                {
                    "color": "blue",
                    "name": "Water",
                    "parts": 1
                }
            ],
            "title": "Water 2"
        }
    ],
    "success": true
}
```


#### Update an existing drink

```http
PATCH /drinks/{id}
```

- General :
    - Update the corresponding drink for <id>
    - This endpoint require authentication
    - Require the 'patch:drinks' permission
    - Return the updated drink and success value
- Sample : `curl -X PATCH "http://127.0.0.1:5000/drinks/3" -H "Content-Type: application/json" -d '{"title": "Water 10","recipe": {"name": "Lemon","color": "green","parts": 1}}' -H "Authorization: Bearer {AUTH_TOKEN}"`

```json
{
  "drinks": [
    {
      "id": 3,
      "recipe": {
        "color": "green",
        "name": "Lemon",
        "parts": 1
      },
      "title": "Water 10"
    }
  ],
  "success": true
}
```

#### Delete drink
```http
DELETE /drinks/{id}
```
- General :
    - Delete the corresponding drink for <id>
    - This endpoint require authentication
    - Require the 'delete:drinks' permission
    - Return the deleted drink id and success value
- Sample : `curl -X DELETE "http://127.0.0.1:5000/drinks/3" -H "Authorization: Bearer {AUTH_TOKEN}"`

```json
{
  "delete": 3,
  "success": true
}
```

## Authors

- [@cybfar](https://github.com/cybfar) for editing some files in the project
- All project files were created by [Udacity](https://github.com/udacity) as a template for the Coffee Shop project.
