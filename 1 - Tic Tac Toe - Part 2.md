# Assignment 2: Tic-Tac-Toe with Bootstrap + Interactivity  

---

## Step 1: Update Flask App for Moves  

Replace your code in `app.py` withe below:  

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# --- Game Logic ---
board = [[" " for _ in range(3)] for _ in range(3)]
current_player = "X"

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

# --- Flask Routes ---
@app.route('/')
def home():
    return render_template("index.html", board=board)

@app.route('/move/<int:row>/<int:col>')
def move(row, col):
    global current_player
    if board[row][col] == " " and not (check_win("X") or check_win("O") or check_draw()):
        place_move(current_player, row, col)
        current_player = "O" if current_player == "X" else "X"
    return redirect(url_for("home"))

if __name__ == '__main__':
    app.run(debug=True)

```

---

## Step 2: Style the Board with Bootstrap  

Replace your `templates/index.html` with the below:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tic-Tac-Toe</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="text-center">

<h1>Tic-Tac-Toe</h1>

<table class="table table-bordered mx-auto">
    {% for i in range(3) %}
    <tr>
        {% for j in range(3) %}
        <td style="width:100px; height:100px; text-align:center;">
            {% if board[i][j] == " " %}
            <a href="{{ url_for('move', row=i, col=j) }}" style="display:block; width:100%; height:100%;">&nbsp;</a>
            {% else %}
            {{ board[i][j] }}
            {% endif %}
        </td>
        {% endfor %}
    </tr>
    {% endfor %}
</table>

</body>
</html>

```

---

## Step 3: Run and Play  

1. Start your Flask app:  

```bash
python app.py
```

2. Open in your browser:  
[http://127.0.0.1:5000/](http://127.0.0.1:5000/)  


---

## Step 4: Update the game
1. Study the existing code to get familar with it. Ask AI about code sections you don't understand.
2. Update the styling to make the game look better. Go to Bootstrap's documenation to learn about how you can style the table, links, etc.
3. Add a message that shows the winner or draw when the game ends.
4. Add a reset button that resets the game.  

## 📌 Submission (Part 2)  

1. Push your updated project to GitHub (`app.py`, `templates/index.html`).  
2. Submit your **GitHub repo link**.  

---
