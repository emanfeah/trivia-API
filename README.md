# Full Stack API Final Project

## Trivia app :

 trivia is a web application to play trivia game with multiple categories .

## API Reference

### Getting Started

* Base URL: Currently this application is only hosted locally. The backend is hosted at `http://localhost:5000/`
* Authentication: No Authentication Needed.

### Error Handling

Errors are returned as JSON in the following format:<br>

    {
        "success": False,
        "error": 404,
        "message": "resource not found "
    }

The API will return three types of errors:

* 400 – bad request
* 404 – resource not found
* 422 – unprocessable
* 405 - method not allowed

### Endpoints

#### GET /categories

* General: Returns a list categories.
* Sample: `curl localhost:5000/categories`<br>

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


#### GET /questions

* General:
  * Returns a list questions.
  * Results are paginated in groups of 10.
  * Also returns list of categories and total number of questions.
* Sample: `curl localhost:5000/questions`<br>

        {
        "categories": {
            "1": "Science", 
            "2": "Art", 
            "3": "Geography", 
            "4": "History", 
            "5": "Entertainment", 
            "6": "Sports"
        }, 
        "current_catagory": null, 
        "questions": [
            {
            "answer": "Maya Angelou", 
            "category": 4, 
            "difficulty": 2, 
            "id": 1, 
            "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
            }, 
            {
            "answer": "Muhammad Ali", 
            "category": 4, 
            "difficulty": 1, 
            "id": 2, 
            "question": "What boxer's original name is Cassius Clay?"
            }, 
            {
            "answer": "Apollo 13", 
            "category": 5, 
            "difficulty": 4, 
            "id": 3, 
            "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
            }, 
            {
            "answer": "Tom Cruise", 
            "category": 5, 
            "difficulty": 4, 
            "id": 4, 
            "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
            }, 
            {
            "answer": "Edward Scissorhands", 
            "category": 5, 
            "difficulty": 3, 
            "id": 5, 
            "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
            }, 
            {
            "answer": "Brazil", 
            "category": 6, 
            "difficulty": 3, 
            "id": 6, 
            "question": "Which is the only team to play in every soccer World Cup tournament?"
            }, 
            {
            "answer": "Uruguay", 
            "category": 6, 
            "difficulty": 4, 
            "id": 7, 
            "question": "Which country won the first ever soccer World Cup in 1930?"
            }, 
            {
            "answer": "George Washington Carver", 
            "category": 4, 
            "difficulty": 2, 
            "id": 8, 
            "question": "Who invented Peanut Butter?"
            }, 
            {
            "answer": "Lake Victoria", 
            "category": 3, 
            "difficulty": 2, 
            "id": 9, 
            "question": "What is the largest lake in Africa?"
            }, 
            {
            "answer": "The Palace of Versailles", 
            "category": 3, 
            "difficulty": 3, 
            "id": 10, 
            "question": "In which royal palace would you find the Hall of Mirrors?"
            }
        ], 
        "success": true, 
        "total_questions": 19
        }

#### DELETE /questions/<question_id>

* General:
  * Deletes a question by id using url parameters.
  * Returns id of deleted question upon success.
* Sample: `curl -X DELETE localhost:5000/questions/4`<br>
        {
  
         "deleted": 4,
        "success": true,
    
        }


#### POST /questions

* General:
  * Creates a new question using JSON request parameters.
  * Returns JSON object with newly created question id.
* Sample: `curl -X POST localhost:5000/questions/create -H 'Content-Type: application/json' -d '{"question":"how old you ?","answer":"22","category":1,"difficulty":1}'`<br>
        {
        "question_id": 25,
        "success": true
        }


#### POST /questions/search

* General:
  * Searches for questions using search term in JSON request parameters.
  * Returns JSON object with matching questions.
* Sample: `curl -X POST localhost:5000/questions/search -H "Content-Type: application/json" -d '{"search": "which"}'`<br>

                {
  

            "questions": [
                {
                    "answer": "Brazil",
                    "category": 6,
                    "difficulty": 3,
                    "id": 10,
                    "question": "Which is the only team to play in every soccer World Cup tournament?"
                },
                {
                    "answer": "Uruguay",
                    "category": 6,
                    "difficulty": 4,
                    "id": 11,
                    "question": "Which country won the first ever soccer World Cup in 1930?"
                },
                {
                    "answer": "The Palace of Versailles",
                    "category": 3,
                    "difficulty": 3,
                    "id": 14,
                    "question": "In which royal palace would you find the Hall of Mirrors?"
                },
                {
                    "answer": "Escher",
                    "category": 2,
                    "difficulty": 1,
                    "id": 16,
                    "question": "Which Dutch graphic artist–initials M C was a creator of optical illusions?"
                },
                {
                    "answer": "Scarab",
                    "category": 4,
                    "difficulty": 4,
                    "id": 23,
                    "question": "Which dung beetle was worshipped by the ancient Egyptians?"
                }
            ],
            "success": true,
            "total_questions": 5
        }

#### GET /categories/<category_id>/questions

* General:
  * Gets questions by category id using url parameters.
  * Returns JSON object with paginated matching questions.
* Sample: `curl localhost:5000/categories/1/questions`<br>

            {
        "current_category": 1,
        "questions": [
            {
                "answer": "The Liver",
                "category": 1,
                "difficulty": 4,
                "id": 20,
                "question": "What is the heaviest organ in the human body?"
            },
            {
                "answer": "Alexander Fleming",
                "category": 1,
                "difficulty": 3,
                "id": 21,
                "question": "Who discovered penicillin?"
            },
            {
                "answer": "Blood",
                "category": 1,
                "difficulty": 4,
                "id": 22,
                "question": "Hematology is a branch of medicine involving the study of what?"
            }
        ],
        "success": true,
        "total_questions": 13
    }

#### POST /quizzes

* General:
  * Allows users to play the quiz game.
  * Uses JSON request parameters of category and previous questions.
  * Returns JSON object with random question not among previous questions.
* Sample: `curl -X POST localhost:5000/quizzes -H "Content-Type: application/json" -d '{"previous_questions": [20, 21],"quiz_category": {"type": "Science", "id": 1}}'`<br>

            {
        "question": {
            "answer": "Blood",
            "category": 1,
            "difficulty": 4,
            "id": 22,
            "question": "Hematology is a branch of medicine involving the study of what?"
        },
        "success": true
    }

## how install  the project : 
Fork the project repository and Clone your forked repository to your machine. 



## About the project 

the project contain 2 folder :

### Backend

The `./backend` directory contains completed Flask and SQLAlchemy server. 

### Frontend

The `./frontend` directory contains a complete React frontend to consume the data from the Flask server. 


##start project  server :
 set up a psql database 
1. fork and clone the project
2. go in frontend folder and run :  [`.npm i`]  and [`.npm start `]
3. go in backend folder and run : [`.export FLASK_APP=flaskr `] and [`.export FLASK_ENV=development `] and 
[`.flask run `]





