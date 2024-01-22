+------------------+        +----------------------+         +-----------------+                                                                                                                                              
|                  |        |                      |         |                 |                                                                                                                                              
|   User's         |        |    Flask Web App     |         |    SQLite DB    |                                                                                                                                              
|   Browser        |  --->  |                      |  <---   |                 |                                                                                                                                        
|                  |        |   - Routes           |         |   - Users        |                                                                                                                                          
|                  |        |   - Models           |         |   - Expenses     |                                                                                                                                     
|                  |        |   - Utils            |         |   - Balances     |                                                                                                                                         
|                  |        |                      |         |                 |                                                                                                                                           
+------------------+        +----------------------+         +-----------------+                                                                                                                                          


User's Browser: This represents the user interface where users interact with the application.

Flask Web App: The core of your application built using Flask. It handles HTTP requests, processes business logic, and communicates with the database.

Routes: Define the API endpoints and handle HTTP requests.
Models: Define the data structures using SQLAlchemy ORM.
Utils: Utility functions for calculations and simplification.
SQLite Database: A lightweight database engine used for simplicity in this example. It stores users, expenses, and balances.

Users: Store user information.
Expenses: Store information about each expense, including the paid user, amount, split type, and participants.
Balances: Store information about the balances between users.
Please note that this is a high-level overview, and you may want to consider additional details based on your specific needs (e.g., asynchronous task processing, security measures, and deployment considerations). Additionally, if your application scales, you might consider more complex architectures, such as separating the frontend and backend, introducing a message queue for asynchronous tasks, or using a dedicated database server.



About the code

User Management:
Users can be added to the system by making a POST request to the /add_user endpoint. User details such as user ID, name, email, and mobile number are provided in the request.

Expense Handling:
Expenses are added to the system by making a POST request to the /add_expense endpoint. The details of the expense include the user who paid (paid_by), the total amount, the split type (EQUAL, EXACT, PERCENT), and the participants.
The application calculates balances between users based on the split type and updates user balances accordingly.

Balances and Simplification:
Users can query their balances by making a GET request to the /get_balances endpoint, providing their user ID.
The /simplify_expenses endpoint simplifies expenses for a specific user by removing zero balances.

Email Notifications:
When a new expense is added, email notifications are sent asynchronously to participants, informing them of the amount they owe.

Flask App Execution:
The Flask application is executed and runs a development server if the script is run directly (if __name__ == '__main__': app.run()).

Data Storage:
User and expense information is stored in dictionaries (users and expenses). User and expense details are encapsulated in classes (User and Expense).


send_email(subject, body, recipients) function:
This function is responsible for sending email notifications.
It uses Flask-Mail to send an email with the specified subject, body, and recipients.
The with app.app_context() ensures that the Flask application context is available within the function.

calculate_balances() function:
This function iterates through all expenses and calculates balances between users based on the split type.
For each expense, it checks the split type (EQUAL, EXACT, PERCENT) and updates the balances accordingly.
The users dictionary stores user information, and the expenses list holds information about each expense.

simplify_expenses(user_id) function:
This function simplifies expenses for a specific user by removing zero balances.
It creates a new dictionary (simplified_balances) to store non-zero balances.
The balances for the specified user are updated with the simplified balances.
