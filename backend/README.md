# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

REVIEW_COMMENT
```
This README is missing documentation of your endpoints. Below is an example for your endpoint to get all categories. Please use it as a reference for creating your documentation and resubmit your code. 

Endpoints
GET '/categories'
GET ...
POST ...
DELETE ...

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs. 
{'1' : "Science",
'2' : "Art",
'3' : "Geography",
'4' : "History",
'5' : "Entertainment",
'6' : "Sports"}

```
Endpoints

GET '/categories'
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, categories, that contains a object of id: category_string key:value pairs. 
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}

GET \questions?page=<page_number> Fetches a paginated dictionary of questions of all available categories

Request Arguments (optional): page:int
Example response:
 "categories": {
   "1": "Science", 
   "2": "Art", 
   "3": "Geography", 
   "4": "History", 
   "5": "Entertainment", 
   "6": "Sports"
 }, 
 "current_category": null, 
 "questions": [
   {
     "answer": "The ancient Egyptians", 
     "category": 4, 
     "difficulty": 2, 
     "id": 9, 
     "question": "Who started the pyramids?"
   },  
   {
     "answer": "Rungrado May Day Stadium", 
     "category": 6, 
     "difficulty": 1, 
     "id": 14, 
     "question": "What is the largest stadium in the world?"
   }
 ], 
 "success": true, 
 "total_questions": 2
}
DELETE /questions/<question_id> Delete an existing questions from the repository of available questions

Request arguments: question_id:int
Example response:
{
  "deleted": "28", 
  "success": true
}
POST /questions Add a new question to the repository of available questions

Request body: {question:string, answer:string, difficulty:int, category:string}
Example response:
{
  "created": 29, 
  "success": true
}
POST /questions/search Fetches all questions where a substring matches the search term (not case-sensitive)

Request body: {searchTerm:string}
Example response:
{
  "current_category": null, 
  "questions": [
    {
      "answer": "Rungrado May Day Stadium", 
      "category": 6, 
      "difficulty": 1, 
      "id": 14, 
      "What is the largest stadium in the world?"
    }
  ], 
  "success": true, 
  "total_questions": 1
}
GET /categories/<int:category_id>/questions Fetches a dictionary of questions for the specified category

Request argument: category_id:int
Example response:
{
  "current_category": 1, 
  "questions": [
    {
      "answer": "around 3 pounds", 
      "category": 1, 
      "difficulty": 4, 
      "id": 15, 
      "question": "What is the normal brain weight?"
    }, 
    {
      "answer": "Paul Ehrlich", 
      "category": 1, 
      "difficulty": 3, 
      "id": 16, 
      "question": "Who invented cancer treatments?"
    }, 
  ], 
  "success": true, 
  "total_questions": 2
}
POST /quizzes Fetches one random question within a specified category. Previously asked questions are not asked again.

Request body: {previous_questions: arr, quiz_category: {id:int, type:string}}
Example response:
{
  "question": {
    "answer": "around 3 pounds", 
    "category": 1, 
    "difficulty": 4, 
    "id": 15, 
    "question": "What is the normal brain weight??"
  }, 
  "success": true
}

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```