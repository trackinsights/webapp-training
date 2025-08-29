# Assignment 2: Tic-Tac-Toe with Bootstrap + Interactivity  

## 🎯 Goal  
By the end of this assignment, you will:  
- Use **Bootstrap** to style your Tic-Tac-Toe board  
- Add **buttons for moves** (instead of plain text)  
- Update the board dynamically after each move  
- Detect and display **win/draw messages**  

---

## Step 0: Install Bootstrap  

You don’t need to install Bootstrap manually — just link it in your HTML.  
In your `templates/index.html` file, update the `<head>` section:  

```html
<head>
    <title>Tic-Tac-Toe</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
```

---

## Step 1: Update Flask App for Moves  

In `app.py`, expand your Flask app:  

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# --- Game Logic (reuse from Assignment 1) ---
board = [[" " for _ in range(3)] for _ in range(3)]
current_player = "X"

def reset_board():
    global board, current_player
    board = [[" " for _ in range(3)] for _ in range(3)]
    current_player = "X"

def place_move(player, row, col):
    if board[row][col] == " ":
        board[row][col] = player
        return True
    return False

def check_win(player):
    for row in board:
        if all(cell == player for cell in row):
            return True
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def check_draw():
    return all(cell != " " for row in board for cell in row)

# --- Flask Routes ---
@app.route('/')
def home():
    message = None
    if check_win("X"):
        message = "Player X wins!"
    elif check_win("O"):
        message = "Player O wins!"
    elif check_draw():
        message = "It's a draw!"
    return render_template("index.html", board=board, message=message)

@app.route('/move/<int:row>/<int:col>')
def move(row, col):
    global current_player
    if board[row][col] == " " and not (check_win("X") or check_win("O") or check_draw()):
        place_move(current_player, row, col)
        current_player = "O" if current_player == "X" else "X"
    return redirect(url_for("home"))

@app.route('/reset')
def reset():
    reset_board()
    return redirect(url_for("home"))

if __name__ == '__main__':
    app.run(debug=True)
```

---

## Step 2: Style the Board with Bootstrap  

Update your `templates/index.html` to add **Bootstrap styling + clickable buttons**:  

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tic-Tac-Toe</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light text-center">
    <div class="container py-5">
        <h1 class="mb-4">Tic-Tac-Toe</h1>

        {% if message %}
        <div class="alert alert-info">{{ message }}</div>
        {% endif %}

        <table class="table table-bordered mx-auto" style="width: 300px; height: 300px; text-align: center; font-size: 2em;">
          {% for row in range(3) %}
          <tr>
            {% for col in range(3) %}
            <td>
              {% if board[row][col] == " " and not message %}
                <a href="{{ url_for('move', row=row, col=col) }}" class="btn btn-outline-primary btn-lg w-100 h-100"></a>
              {% else %}
                {{ board[row][col] }}
              {% endif %}
            </td>
            {% endfor %}
          </tr>
          {% endfor %}
        </table>

        <a href="{{ url_for('reset') }}" class="btn btn-danger mt-3">Reset Game</a>
    </div>
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
👉 [http://127.0.0.1:5000/](http://127.0.0.1:5000/)  

✅ You can now:  
- Click cells to place `X` and `O`  
- Automatically alternate between players  
- See **win/draw messages**  
- Reset the game with a button  

---

## 📌 Submission (Part 2)  

1. Push your updated project to GitHub (`app.py`, `templates/index.html`).  
2. Verify that:  
   - The board shows clickable buttons for moves  
   - Win/draw/reset logic works correctly  
   - Bootstrap styling is applied  
3. Submit your **GitHub repo link**.  

---

💡 **Next (Assignment 3):** We’ll add **JavaScript for instant updates** (AJAX/Fetch), so the page doesn’t reload every time you click a cell.  
