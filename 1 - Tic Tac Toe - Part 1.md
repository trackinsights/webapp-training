# Assignment 1: Tic-Tac-Toe Game Logic + Flask Basics 

## Overview
In this assignment, you will:  
- Write the **game logic** for Tic-Tac-Toe in Python  
- Set up a **Flask web app**  
- Display a simple board in the browser  

This builds your foundation before adding styling and advanced features in Assignment 2.

---

## Step 0: Project Setup

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
6. (Optional) Add a `.gitignore` file to ignore your virtual environment:  

```
venv/
__pycache__/
```

---

## Step 1: Build the Game Logic

In `app.py`, add:

```python
# Create a 3x3 board
board = [[" " for _ in range(3)] for _ in range(3)]

# Function to print the board in the terminal
def print_board():
    for row in board:
        print("|".join(row))
    print()

# Place a move
def place_move(player, row, col):
    if board[row][col] != " ":
        return False
    board[row][col] = player
    return True

# Check for a win
def check_win(player):
    # Rows
    for row in board:
        if all(cell == player for cell in row):
            return True
    # Columns
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    # Diagonals
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

# Check for a draw
def check_draw():
    return all(cell != " " for row in board for cell in row)
```

Test your functions in the terminal:

```python
place_move("X", 0, 0)
print_board()
print(check_win("X"))   # False
print(check_draw())     # False
```

---

## Step 2: Add Flask Basics

Add Flask code below your game logic:

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route('/')
def home():
    # Display the board in an HTML template
    return render_template("index.html", board=board)

if __name__ == '__main__':
    app.run(debug=True)
```

---

## Step 3: Create the Template

1. Create a folder called `templates` **next to `app.py`**:

```
tic-tac-toe-flask/
├─ app.py
├─ templates/
```

2. Inside `templates/`, create a file called `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tic-Tac-Toe</title>
</head>
<body>
    <h1>Welcome to Tic-Tac-Toe!</h1>
    <table border="1">
      {% for row in board %}
      <tr>
        {% for cell in row %}
        <td>{{ cell }}</td>
        {% endfor %}
      </tr>
      {% endfor %}
    </table>
</body>
</html>
```

3. Run your Flask app:

```bash
python app.py
```

4. Open [http://127.0.0.1:5000/](http://127.0.0.1:5000/) in a browser. You should now see a small 3x3 grid showing your board. We will apply styling in the next part to get the board looking better!

---

## Submission (Part 1)

1. Push all files to GitHub (`app.py`, `templates/`, `.gitignore`).  
2. Make sure `python app.py` runs locally.  
3. Submit your repository link.

**Goal:** A working Flask app that displays your Tic-Tac-Toe board **while keeping your Python functions intact**.
