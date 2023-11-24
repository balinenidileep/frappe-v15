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

## Bootstrap Theme SCSS Structure

Our main website stylesheet is built by theming, customizing and compiling bootstrap v4.5+ using SCSS. Frappe provides ESBuild for bundling SCSS and JavaScript files that will compile our SCSS files. 

* Create a directory for SCSS files `public/paralogic_web/scss/paralogic_theme/`
* Keep the directory organized into multiple files: `type.scss`, `buttons.scss`, `forms.scss`, `utils.scss`, ...
* Create a bundle file `public/paralogic_web/scss/paralogic_theme.bundle.scss`

### Bundle File

* Override Bootstrap variables
* `@import "frappe/public/scss/website"` to import frappe's SCSS files along with Bootstrap SCSS files
* Set CSS `:root` variables
* Import all your SCSS files from `public/paralogic_web/scss/paralogic_theme/` in your bundle file
* Add `custom_theme_bundle` by defining/updating `website_context` in `hooks.py` 

```python
website_context = {
	"custom_theme_bundle": "paralogic_theme.bundle.css",
}
```

### Bootstrap Variables Reference

* Refer to https://github.com/twbs/bootstrap/blob/v4.5.0/scss/_variables.scss for a list of all bootstrap's SCSS variables
* Refer to https://github.com/twbs/bootstrap/blob/v4.5.0/scss/_root.scss for a list of all boostrap's *CSS* :root variables

### Common Option Variables

* `$enable-rounded` for border radius on common elements
* `$enable-shadows`
* `$enable-gradients`

### Colors Variables

Bootstrap have the following variables which also become part of your CSS :root variables. The important color list variables are `$colors`, `$theme-colors` and `$grays`. We strongly recommend to use color CSS variables instead of hard coding them. 

* Base Colors: always define your own `$white`, `$black`
* Grays: you may override `$gray-50`, `$gray-100`, `$gray-200`, ..., `$gray-900`
* Color Palette: you may override `$blue`, `$indigo`, `$purple`, `$pink`, `$red`, `$orange`, `$yellow`, `$green`, `$teal`, `$cyan`
* Color Palette: you may add additional colors by creating for example `$magenta` by adding it into the `$colors` variable
* Theme Colors: always define `$primary`, `$secondary`, `$success`, `$info`, `$warning`, `$danger`, `$light`, `$dark` preferably using your colors from the `$colors` palette
* Theme Colors: you may add additional theme colors by defining `$theme-colors`
* Body Colors: always define `$body-bg`, `$body-color` for default body background and font colors
* Link Color: you may override `$link-color` (defaults to $primary)
* Border Color: `$border-color` (defaults to $gray-900)
* Headings Color: `$headings-color`
* Muted/Disabled Text Color: `$text-muted`
* Placeholder Color: `$placeholder` (To be implemented)

### Fonts and Typography Variables

* You should create a separate font CSS directory and file for letting the browser down the fonts using [Transfonter](https://transfonter.org/)
* Make sure to include your font css in `hooks.py` `web_include_css`
* Font Family: always define `$font-family-sans-serif` along with fallback font similar to actual font
* Headings Size: `$h1-font-size`, ..., `$h6-font-size`
* Headings Margin Bottom: `$headings-margin-bottom`
* Headings Font: you may define `$headings-font-family` (for example `$font-family-serif` for headings)
* Always define font sizes in rem

### Navbar Variables

* Padding: `$navbar-padding-x`, `$navbar-padding-y`
* `$navbar-light-color`, `$navbar-light-hover-color`, `$navbar-light-active-color`, `$navbar-light-disabled-color`, `$navbar-light-toggler-icon-bg`, `$navbar-light-toggler-border-color` (replace `-light-` with `-dark-` for dark navbar)

### Card Variables

* `$card-spacer-y`, `$card-spacer-x`
* `$card-border-radius`
* `$card-border-color`
* `$card-bg`

### Miscellaneous Variables

* Common Border Radius: `$border-radius`, `$border-radius-lg`, `$border-radius-sm`
* Common Shadows: `$box-shadow`, `$box-shadow-sm`, `$box-shadow-lg`
* Define if using tabs or other components: `$component-active-bg`, `$component-active-color`
* Common Transition: `$transition-base`, `$transition-fade`, `$transition-collapse`

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
