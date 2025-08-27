# Assignment 1: Tic-Tac-Toe Game Logic + Flask Basics

## Overview
In this assignment, you will:  
- Write the **game logic** for Tic-Tac-Toe in Python  
- Set up a **Flask web app**  
- Display a simple board in the browser  

This builds your foundation before adding styling and advanced features in Assignment 2.

---

## Project Setup

1. Create a folder for your project, e.g., `tic-tac-toe-flask`.  
2. Create a Python virtual environment:  
   ```bash
   python -m venv venv
   ```
3. Activate your environment:  
   - Windows:  
     ```bash
     venv\Scripts\activate
     ```
   - Mac/Linux:  
     ```bash
     source venv/bin/activate
     ```
4. Install Flask:  
   ```bash
   pip install flask
   ```
5. Create a Python file: `app.py`.  
---

## Build the Game Logic

In `app.py`:

1. Create a 3x3 board:
   ```python
   board = [[" " for _ in range(3)] for _ in range(3)]
   ```

2. Add a function to print the board:
   ```python
   def print_board():
       for row in board:
           print("|".join(row))
       print()
   ```

3. Call it to test:
   ```python
   print_board()
   ```

   **Expected Output:**  
   ```
   | | 
   | | 
   | | 
   ```

4. Add these functions (and test them one by one in the terminal):  

   ```python
   def place_move(player, row, col):
       # If the cell is NOT empty, return False. Otherwise, move the player there and return True. 

   def check_win(player):
       # Check rows, columns, columns. Return True if player wins, or False otherwise

   def check_draw():
       # Return True if draw, or False otherwise
   ```

5. Test your functions in the terminal:  

   ```python
   place_move("X", 0, 0)
   print_board()

   # Expected:
   # X| | 
   #  | | 
   #  | | 

   print(check_win("X"))   # False
   print(check_draw())     # False
   ```

👉 **Test each function separately before continuing.**

---

## Create a Basic Flask App

Replace your file contents with:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Tic-Tac-Toe!"

if __name__ == '__main__':
    app.run(debug=True)
```

Run:
```bash
python app.py
```

Visit: [http://127.0.0.1:5000/](http://127.0.0.1:5000/) → you should see **Hello, Tic-Tac-Toe!**

---

## Add an HTML Template

1. Create a folder called `templates`.  
2. Inside, make a file `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tic-Tac-Toe</title>
</head>
<body>
    <h1>Welcome to Tic-Tac-Toe!</h1>
</body>
</html>
```

3. Update `app.py`:

```python
from flask import Flask, render_template

app = Flask(__name__)
board = [[" " for _ in range(3)] for _ in range(3)]

@app.route('/')
def home():
    # We will display the board in the next step
    return render_template("index.html", board=board)
```

4. Restart and refresh — you should now see your HTML.  
   *(Note: we’re already passing the board to the template, even though we’re not using it yet.)*

---

## Display the Board

Update `index.html`:

```html
<table border="1">
  {% for row in board %}
  <tr>
    {% for cell in row %}
    <td>{{ cell }}</td>
    {% endfor %}
  </tr>
  {% endfor %}
</table>
```

**Expected Result in Browser:**  
A simple 3x3 grid showing blank spaces.

---

## Submission (Part 1)
1. Push all files to GitHub (`app.py`, `templates/`, and `.gitignore`).  
2. Make sure `python app.py` runs locally.  
3. Submit your repository link.  

**Goal:** A working Flask app that shows a Tic-Tac-Toe board in the browser.  
