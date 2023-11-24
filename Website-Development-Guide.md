Follow this guide to create quality and well organized website apps using Frappe Framework and and other frappe apps 

## Create a new App

Create a new frappe app using `bench new-app` and enter relevant information when prompted.

* Keep the name short and relevant to the project / client
* Best to go with company name in snake case for ex: `fusion_media`
* If using just the company name is too vague then use a suffix like `paralogic_website` or `paralogic_web`
* Set publisher as ParaLogic (info@paralogic.io) if you are working on any ParaLogic's website project
* Update relevant information in your app's `hooks.py` file: dependent apps if any, ...
* Create a git repository (on GitHub) and push to the repository
* For this guide we will assume we are creating an app called `paralogic_web`

## Create a Bootstrap SCSS Theme

See [Bootstrap SCSS Theme Guide](https://github.com/ParaLogicTech/frappe/wiki/Bootstrap-SCSS-Theme-Guide) for details on how to create and implement a Bootstrap Theme Stylesheet

## Assets

Keep your assets organized in your app's `public/` directory. You can access your assets using the directory: `/assets/paralogic_home/...` Always use absolute URLs for linking your assets or web pages starting with `/`. For example `/assets/paralogic_home/logo/logo.png` instead of `assets/paralogic_home/logo/logo.png`

* public/images/
* public/images/logo/
* public/images/background/
* public/images/illustrations/
* public/images/icons/
* public/images/icons/
* public/videos/...
* public/css/
* public/css/fonts/
* public/css/fonts/roboto/...
* public/scss/
* public/js/
* public/js/fullpage/...
* public/js/aos/...

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

## Favicon
...

## Images
...
