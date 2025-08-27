# Assignment 2: Interactive Web-Based Tic-Tac-Toe

## Overview
Now that your game logic and Flask app are set up, you’ll:  
- Make the game **interactive**  
- Add **Bootstrap styling**  
- Implement **win/draw checks** and a **reset button**  

---

## Step 5: Let Users Make Moves

1. Update `index.html` to add a **button for each cell**:  

```html
<table class="table table-bordered text-center">
  {% for row_index, row in enumerate(board) %}
  <tr>
    {% for col_index, cell in enumerate(row) %}
    <td>
      <form method="POST" action="/move">
        <input type="hidden" name="row" value="{{ row_index }}">
        <input type="hidden" name="col" value="{{ col_index }}">
        <button type="submit" class="btn btn-primary">
          {{ cell if cell != " " else "Play" }}
        </button>
      </form>
    </td>
    {% endfor %}
  </tr>
  {% endfor %}
</table>
```

2. Add a POST route in `app.py` to handle moves:  

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)
board = [[" " for _ in range(3)] for _ in range(3)]
current_player = "X"

@app.route('/', methods=["GET"])
def home():
    return render_template("index.html", board=board)

@app.route('/move', methods=["POST"])
def move():
    global current_player
    row = int(request.form["row"])
    col = int(request.form["col"])

    if board[row][col] == " ":
        board[row][col] = current_player
        current_player = "O" if current_player == "X" else "X"
    
    return redirect(url_for("home"))
```

---

## Step 6: Add Bootstrap Styling

1. Add Bootstrap to `index.html`:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
```

2. Wrap everything inside a container for layout:  

```html
<div class="container mt-4">
  <h1 class="text-center">Tic-Tac-Toe</h1>
  <!-- your table here -->
</div>
```

---

## Step 7: Check Wins and Draws

1. Use your `check_win` and `check_draw` functions after each move.  
2. Display a message in `index.html`, e.g.,  

```html
{% if message %}
<div class="alert alert-info text-center">{{ message }}</div>
{% endif %}
```

3. Update Flask routes to pass `message` when needed.

---

## Step 8: Add Reset Functionality

1. Add a “Reset Game” button in `index.html`:  

```html
<form method="POST" action="/reset">
  <button class="btn btn-danger mt-3">Reset Game</button>
</form>
```

2. Add a route in `app.py`:  

```python
@app.route('/reset', methods=["POST"])
def reset():
    global board, current_player
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"
    return redirect(url_for("home"))
```

---

## Optional Extensions
- Track scores across games  
- Prevent moves after the game ends  
- Add an AI opponent  

---

## Submission (Part 2)
1. Push all updates to GitHub (`app.py`, `templates/`).  
2. Confirm `python app.py` runs and the game plays in a browser.  
3. Submit your repository link.  

**Goal:** A fully functional web-based Tic-Tac-Toe with Flask + Bootstrap.  
