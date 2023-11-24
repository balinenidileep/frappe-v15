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

## Assets

Keep your assets organized in your app's `public/` directory. You can access your assets using the directory: `/assets/paralogic_home/...` Always use absolute URLs for linking your assets or web pages starting with `/`. For example `/assets/paralogic_home/logo/logo.png` instead of `assets/paralogic_home/logo/logo.png`

* public/images/
* public/images/logo/...
* public/images/background/...
* public/images/illustrations/...
* public/images/icons/...
* public/videos/...
* public/css/
* public/css/fonts/
* public/css/fonts/roboto/...
* public/scss/
* public/scss/paralogic_theme/...
* public/js/
* public/js/fullpage/...
* public/js/aos/...

## Bootstrap SCSS Theme Structure

Your main website stylesheet can be built by customizing, themeing and compiling Bootstrap v4.5+ using ESBuild to bundle and build SCSS files into a CSS file. We import Frappe's website SCSS files which in imports Bootstrap. Frappe provides additional variables and styling for its built in components and pages.

See [Bootstrap SCSS Theme Guide](https://github.com/ParaLogicTech/frappe/wiki/Bootstrap-SCSS-Theme-Guide) for details on how to create and implement a Bootstrap Theme Stylesheet

## Web Page HTML/Jinja Structure

HTML Web Pages can be created by creating files inside your app's `www` directory. HTML files are processed by [Jinja (template engine)](https://jinja.palletsprojects.com/). Python files are treated as backend scripts responsible for providing data to the HTML/Jinja files by updating context variables. Context variables can be to generate dynamic content for the web pages.

See [Web Page HTML Jinja Guide](https://github.com/ParaLogicTech/frappe/wiki/Web-Page-HTML-Jinja-Guide) for details on how to create web pages and integrate them with Frappe's Jinja base templates

## Favicon
...

## Images
...
