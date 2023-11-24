## Web Page Structure

Web Pages can be created by creating files inside your app's `www` directory. HTML files are treated as Jinja templates. Python files are treated as backend scripts to update the context variables for HTML files.

For example to create an "About Us" page you can create the files `www/about.html` and `www/about.py` which can then be accessed by https://paralogic.io/about.

* HTML files should extend `{% extends "templates/web.html" %}`
* HTML files should have the following blocks: `{% block style %}`, `{% block hero %}`, `{% block page_content %}`, `{% block navbar %}`, `{% block script %}`
* Python files should contain a `def get_context(context)` method that will update the `context` dict variables used in the HTML file

## Create Home Page

* Create file `www/paralogic_home.html`
* Create file `www/paralogic_home.py`
* Add `home_page = "paralogic_home"` in `hooks.py` (user can also change the home page in Website Settings)

## Navbar
...