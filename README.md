# Flask Todo

Experimenting with Flask and Python.

* `virtualenv env` // Create a virtual environment
* activate virtualenv `source env/bin/activate`
* `pip3 freeze -> requirements.txt` // note that this file is empty (you must run it from the virtual env)
  * Other devs in their virtual environment can do `pip install -r requirements.txt`
* `pip3 install flask flask-sqlalchemy`
* `pip3 freeze -> requirements.txt` // now we see the dependencies.

## Database

Configuring a SQLite for simplicity sake

```python
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime

#setting DB

# sqlite:/// - relative path
# sqlite://// - absolute path
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///test.db'
db = SQLAlchemy(app)
```

Defining a class model

```python
class Todo(db.Model):
    id = db.Column(db.Integer, primary_key = True)
    content = db.Column(db.String(255), nullable = False)
    completed = db.Column(db.Integer, default = 0)
    date = db.Column(db.DateTime, default = datetime.utcnow)

    def __repr__(self):
        return '<Task %r>' % self.id;
```

Creating a SQLite DB

On the Python REPL, with the virtual environment set

```python
from app import db
db.create_all()
exit()
```


## Credits

Based on 
[Learn Flask for Python](https://www.youtube.com/watch?v=Z1RJmh_OqeA&t=386s)