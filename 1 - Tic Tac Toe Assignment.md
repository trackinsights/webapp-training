
# Flask + Bootstrap Tic-Tac-Toe Project

## Overview
In this project, you will build a **Tic-Tac-Toe game** that runs in a web browser using:

- **Python** for game logic  
- **Flask** for the web application  
- **Bootstrap** for styling  

The project is broken into **small, testable steps** so you can verify each part as you build.

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

---

## Step 1: Build the Game Logic

In `app.py`:

1. Create a 3x3 board:

```python
board = [["-" for _ in range(3)] for _ in range(3)]
```

2. Add a print board function:
3. 
```python
def print_board():
    for row in board:
        print("|".join(row))
    print()
```
3. Call print_board():

  ```python
print_board():
```
4. Run your program to verify print_board() works.
   
5. Add these functions:
   - Place a move (`X` or `O`)  
   - Check for a win  
   - Check for a draw  

6. Test your functions.

> **Tip:** Test each function separately before moving on. 

---

## Step 2: Create a Basic Flask App

In `app.py`:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Tic-Tac-Toe!"

if __name__ == '__main__':
    app.run(debug=True)
```

Run the app:

```bash
python app.py
```

Visit `http://127.0.0.1:5000/` to verify it works.

---

## Step 3: Add HTML Templates

1. Create a folder called `templates`.  
2. Add `index.html`:

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

3. Update `app.py` to render the template:

```python
from flask import Flask, render_template

app = Flask(__name__)
board = [[" " for _ in range(3)] for _ in range(3)]

@app.route('/')
def home():
    return render_template("index.html", board=board)
```

---

## Step 4: Display the Board

Update `index.html` to render the board dynamically:

```html
<table>
  {% for row in board %}
  <tr>
    {% for cell in row %}
    <td>{{ cell }}</td>
    {% endfor %}
  </tr>
  {% endfor %}
</table>
```

---

## Step 5: Let Users Make Moves

1. Add forms or buttons for each cell.  
2. Add a route in `app.py` to handle moves (POST requests).  
3. Update the `board` variable after each move.

> Test one move at a time.

---

## Step 6: Add Bootstrap Styling

1. Include Bootstrap in `<head>` of `index.html`:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
```

2. Style the board using Bootstrap:
   - `table table-bordered text-center` for the board  
   - `btn btn-primary` for move buttons  
   - Wrap the board in `<div class="container">` and use `row`/`col` classes as needed  

---

## Step 7: Check Wins and Draws

1. After each move, check if a player has won or if it’s a draw.  
2. Display a message on the page (e.g., “Player X wins!” or “Draw”).

---

## Step 8: Add Reset Functionality

1. Add a reset button.  
2. Create a route to clear the board and reload the page.

---

## Optional Extensions

- Keep track of scores across games  
- Add two-player online mode using sessions  
- Add an AI opponent (start with random moves)

---

## Submission

1. Push all files to GitHub (`app.py`, `templates/`, optionally `static/`).  
2. Make sure `python app.py` runs locally.  
3. Submit your repository link.

---

**Goal:** By the end, you will have a fully functional **web-based Tic-Tac-Toe game** built with Python, Flask, and Bootstrap.
