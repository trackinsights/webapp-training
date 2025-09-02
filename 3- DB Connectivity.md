# Assignment 3: DB Connectivity  

---

The goal of this assignment is to create a web app that displays the school_name and school_type 
for all the schools in the Track.db database. 

## Project Layout

```
flask_bootstrap_db_demo/
│
├── app.py
├── Track.db
└── templates/
    └── index.html
```

The code for app.py and index.html is listed below. 

[Download Track.db](https://raw.githubusercontent.com/trackinsights/webapp-training/main/Track.db)


## `app.py`

```python
from flask import Flask, render_template
import sqlite3

app = Flask(__name__)

def get_data():
    conn = sqlite3.connect("Track.db")
    conn.row_factory = sqlite3.Row
    cur = conn.cursor()
    cur.execute("SELECT school_name, school_type FROM school")
    rows = cur.fetchall()
    conn.close()
    return rows

@app.route("/")
def index():
    data = get_data()
    return render_template("index.html", data=data)

if __name__ == "__main__":
    app.run(debug=True)
```

## `templates/index.html`

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Flask + Bootstrap + SQLite</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body class="bg-light">
    <div class="container py-5">
      <h1 class="mb-4">User List</h1>
      <table class="table table-striped table-bordered">
        <thead class="table-dark">
          <tr>
            <th>Name</th>
            <th>Email</th>
          </tr>
        </thead>
        <tbody>
          {% for row in data %}
          <tr>
            <td>{{ row['name'] }}</td>
            <td>{{ row['email'] }}</td>
          </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
  </body>
</html>
```

---

## Run It

```bash
python app.py
```

Open [http://127.0.0.1:5000/](http://127.0.0.1:5000/) in your browser.
