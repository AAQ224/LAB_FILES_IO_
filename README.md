# LAB_FILES_IO


## Using what you learned about Python File I/O , we want to make a progeram called To-Do List , this program should do the following:
- Ask the user do you want to add a new To-Do item? answer by "y" for yes and "n" for no.
- If the user answers yes , then ask the user to type in his new To-Do item . Then save that To-Do item inside the a file to_do.txt on a new line.
- If the user answers no, then ask the user : do you want to list your To-Do items ? answer "y" for yes and "n" for no. 
- If the user answers yes for reading his To-Do list , then print a list of the To-Do items one item per line.
- Then return again to ther first question and ask again, you coninue this untill the user types in "exit" , then you exit the program. and print to the user "thank you for using the To-Do program, come back again soon"

--------------

# Bonus
## studio Equipment Checkout System
Your task is to build a terminal-based Equipment Checkout System that replaces the notebook.
The system must store its information in a JSON file so that all records remain available even after the program is closed and restarted.

# Python Coding Challenge: The Equipment Checkout System

You have been hired by a small media production studio that lends cameras, microphones, lighting equipment, and other gear to its employees.

Currently, the studio tracks equipment using a notebook. This has caused several problems: equipment goes missing, employees borrow items that are already in use, and nobody knows exactly what is available.

Your task is to build a terminal-based Equipment Checkout System that replaces the notebook.

The system must store its information in a JSON file so that all records remain available even after the program is closed and restarted.

## 1. How the system should work

When the program starts, it displays:

```
=================================
    STUDIO EQUIPMENT MANAGER
=================================

1. Add Equipment
2. View All Equipment
3. Search Equipment
4. Update Equipment
5. Delete Equipment
6. Borrow Equipment
7. Return Equipment
8. View Borrowing History
9. Exit

Select an option:
```

The program continues running until the user selects Exit.

## 2. Equipment Management — CRUD

Implement the following operations:

| Operation | Requirements                                                                  |
| --------- | ----------------------------------------------------------------------------- |
| Create    | Add equipment with a unique ID, name, category, and total quantity.           |
| Read      | Display all equipment, including how many units are currently available.      |
| Update    | Allow changing the name, category, or total quantity.                         |
| Delete    | Remove equipment by ID, provided no units are currently borrowed.             |
| Search    | Find equipment by name or category, ignoring uppercase/lowercase differences. |

###### IMPORTANT: Equipment IDs must be generated automatically. Two different equipment records must never have the same ID.

## 3. Borrowing and Returning Equipment

This is where the real problem-solving begins.

When an employee borrows equipment, the system must ask for their name, the equipment ID, and the quantity they want to borrow.

Borrowing rules:

- An employee cannot borrow more units than are available.
- Every borrowing transaction receives a unique ID.
- A successful borrowing transaction reduces the available quantity.
- Each transaction must store the employee name, equipment ID, borrowed quantity, and borrowing date.
- The transaction must have a status of either `borrowed` or `returned`.

When equipment is returned, the user enters the borrowing transaction ID. The system must mark the transaction as returned and make the borrowed units available again. Returning the same transaction twice must not increase availability twice.

## 4. JSON File Storage

Use a file named `studio_data.json` to store the records.

You may organize the data however you prefer. One possible structure is:

```
{
  "equipment": [
    {
      "id": 1,
      "name": "Sony Camera",
      "category": "Cameras",
      "quantity": 5
    },
    {
      "id": 2,
      "name": "Wireless Microphone",
      "category": "Audio",
      "quantity": 3
    }
  ],
  "transactions": [
    {
      "id": 1,
      "equipment_id": 1,
      "employee": "Ahmed",
      "quantity": 2,
      "date": "2026-10-18",
      "status": "borrowed"
    }
  ]
}
```

The quantity stored for equipment represents the total number of units owned, not just the available units.

For example, if the studio owns five cameras and two are borrowed, the system should display:

```
Sony Camera
Total: 5
Borrowed: 2
Available: 3
```

#### Students must determine how to calculate availability using the information stored in the JSON file.

## 5. Required File Handling Behavior

The application must satisfy these conditions:

1. When started, it loads all existing records from `studio_data.json`.
2. If the file does not exist, the application creates it with the necessary empty data structure.
3. Every successful change must be saved to the JSON file.
4. When the application restarts, previously stored data must remain unchanged.
5. Invalid operations must not corrupt or erase existing records.
6. The application must use Python's built-in `json` module; databases are not allowed.

## 6. Example Test Scenario

Imagine the following sequence of operations.

Step 1 — Add Cameras

5 available

The studio adds five Sony cameras.

Step 2 — Ahmed Borrows Two

3 available

Ahmed successfully borrows two cameras.

Step 3 — Sara Requests Four

Rejected

Only three cameras are available. The system refuses the request.

Step 4 — Ahmed Returns Two

5 available

Ahmed returns his cameras using his transaction ID.

Step 5 — Delete Cameras

Deleted

Because no cameras are currently borrowed, the equipment can be deleted.


### Important Restrictions

- Do not use a database, external storage libraries, or prebuilt CRUD frameworks. Use Python's standard library.

- You  should write their own functions, organize the application into logical sections, and decide how to connect equipment records with borrowing transactions.

- Final requirement: Demonstrate the application working, close it completely, restart it, and prove that all equipment records and borrowing transactions have been preserved.
