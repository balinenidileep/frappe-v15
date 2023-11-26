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

You can store your static asset files in your app's `public/` directory. You can access your assets using the URL: `/assets/paralogic_web/...`. For example the URL to access file file `public/logo/logo.png` will be `/assets/paralogic_web/logo/logo.png`.

Keep your assets organized in your app's `public/` directory. 

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

Always use absolute URLs for linking your assets or web pages. Start your URLs with `/`. For example `/assets/paralogic_web/logo/logo.png` instead of `assets/paralogic_web/logo/logo.png`

## Build System

Frappe bundles and builds JavaScript, SCSS, Markdown and other various file types using ESBuild. Bundle files can be created anywhere in the `public/` directory by naming them with a `.bundle.` in the middle like `paralogic_theme.bundle.scss` or `swiper.bundle.js`. All bundle files are built by running the bench commands:

* `bench update`
* `bench build`

Bundle files are also watched and built automatically when any of the files have changed while the development server is running. The compiled/generated files are named with a hash string in the middle like  `paralogic_theme.bundle.ABC123XYZ.css` in order to prevent the browser from using outdated/cached files.

To use or find the most recent compiled version of the bundle file we have multiple utility methods/Jinja filters

* `bundled_asset("about.bundle.css")` that returns the URL to the most recent built file
* `include_style("paralogic_theme.bundle.css")` that writes `<link href="...">`
* `include_script("swiper.bundle.js")` that writes `<script src="...">`

Read more about Asset Bundling on https://frappeframework.com/docs/user/en/basics/asset-bundling

## SCSS Stylesheets

Your website's main stylesheet can be built by customizing, themeing and compiling Bootstrap v4.5+ using ESBuild to bundle and build SCSS files into a CSS file. We import Frappe's website SCSS files which in turn imports Bootstrap. Frappe provides additional variables and styling for its built in components and pages.

See [SCSS Stylesheet Structure](https://github.com/ParaLogicTech/frappe/wiki/SCSS-Stylesheet-Structure) for details on how to create and implement a Bootstrap Theme Stylesheet

## HTML/Jinja Web Pages

HTML Web Pages can be created by creating files inside your app's `www` directory. HTML files are processed by [Jinja (template engine)](https://jinja.palletsprojects.com/). Python files are treated as backend scripts responsible for providing data to the HTML/Jinja files by updating context variables. Context variables can be used to generate dynamic content for the web pages.

See [HTML Jinja Web Page Structure](https://github.com/ParaLogicTech/frappe/wiki/HTML-Jinja-Web-Page-Structure) for details on how to create web pages and integrate them with Frappe's Jinja base templates

## Using JavaScript Libraries

There are 2 ways to add JavaScript libraries to your app:

1. By downloading the JavaScript library files and putting them in `public/js/` directory to be used as a static asset
2. Using Yarn package manager to download the package and compiling the package using ESBuild

We recommend compiling JavaScript packages rather than downloading the libraries when possible so that only the relevant parts of the library code gets compiled. We highly discourage using CDNs for loading JavaScript libraries in order to ensure long term asset availability on your website.

There are 2 ways to include the JavaScript libraries in your page pages:

1. Add `<script src="...">` in your page's `{% block script %}` for each individual page that requires the library
2. Add `web_include_js = ["/assets/paralogic_web/js/aos.js"]` in `hooks.py` to include the library in all web pages

We recommend including the libraries in specific individual pages if the library is not required in all pages to prevent loading libraries that are not required. If the library is required for all the pages then you should include it in `hooks.py`

## Compiling JavaScript Packages (Swiper example)

We recommend using [Swiper](https://swiperjs.com/) for carousels and sliding content. To compile Swiper:

* Make sure you are in your bench directory `cd path/to/your/bench`
* Change directory to your app directory `cd apps/paralogic_web`
* `yarn add swiper` will download the package and add it to your app's `package.json`
* Create file `public/js/swiper.bundle.js`, import Swiper and expose the Swiper class

```js
import Swiper from 'swiper';
import { Navigation, Pagination, Thumbs, Autoplay } from 'swiper/modules'; // import only the modules you need
Swiper.use([Navigation, Pagination, Thumbs, Autoplay]); // tell swiper to use the modules
window.Swiper = Swiper; // expose Swiper class to global `window` object
```

* Create file `public/scss/swiper.bundle.scss`, import Swiper's SCSS file and import only the modules you need

```scss
@import "../node_modules/swiper/swiper.scss";
@import "../node_modules/swiper/modules/navigation.scss";
@import "../node_modules/swiper/modules/pagination.scss";
@import "../node_modules/swiper/modules/thumbs.scss";
@import "../node_modules/swiper/modules/controller.scss";
```

* Run `bench build` to compile the bundle files
* Add `{{ include_script("swiper.bundle.js") }}` in your page HTML file's `{% block script %}`
* Add `{{ include_style("swiper.bundle.css") }}` in your page HTML file's `{% block style %}`
* Write your JavaScript to use the Swiper object available as a global `window` variable

## CMS DocType Structure
Page DocTypes, Settings, Website Generators, Data Sources, ...

## JavaScript Utilities
...

## CMS Settings
...

## Favicon
...

## Images
...

## SEO
...

## Reusable Code
...

## Clean Code
...

## Naming Convention
filename/variable names/doctype names

## Coding Convention
tab/spaces...


