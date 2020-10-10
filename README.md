# Flask Todo

Experimenting with Flask and Python.

* `virtualenv env` Create a virtual environment
* `source env/bin/activate` Activate virtualenv 
* `pip3 install flask flask-sqlalchemy`

* `pip3 install gunicorn` a Python WSGI HTTP Server
* `pip3 freeze -> requirements.txt` at the end, just re-export the dependencies.
  * `pip install -r requirements.txt` to reinstall requirements

* 
## Database

USing SQLite for simplicity sake

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

* Run this script (ad-hoc) `create_db.py`

## Glossary

* [Flask](https://palletsprojects.com/p/flask/)  a lightweight WSGI web application framework.
  * Flask depends on the [Jinja](https://www.palletsprojects.com/p/jinja/) template engine and the [Werkzeug](https://www.palletsprojects.com/p/werkzeug/) WSGI toolkit.

* [WSGI](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface)
* [Green Unicorn - gunicorn](https://gunicorn.org/) a Python WSGI HTTP Server for UNIX

## Uploading the app to Heroku

* Install [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli)
  * on WSL `$ curl https://cli-assets.heroku.com/install.sh | sh`
* Create `Procfile` into the app root folder with the content `web: gunicorn app:app`
* with the git repository at least initialized and heroku logged in
* `$ heroku create <my-app-name>`
* `$ git remote -v` check remotes
* `$git push heroku <branch_to_push>`

## Credits

Based on [Learn Flask for Python](https://www.youtube.com/watch?v=Z1RJmh_OqeA&t=386s)