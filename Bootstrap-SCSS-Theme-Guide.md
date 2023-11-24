Your website's main stylesheet can be built by customizing, themeing and compiling Bootstrap v4.5+ using ESBuild to bundle and build SCSS files into a CSS file. We import Frappe's website SCSS files which in imports Bootstrap. Frappe provides additional variables and styling for its built in components and pages.

* Create a directory for SCSS files `public/paralogic_web/scss/paralogic_theme/`
* Keep the directory organized by splitting into multiple SCSS files: `type.scss`, `buttons.scss`, `forms.scss`, `utils.scss`, ...
* Create an SCSS bundle file `public/paralogic_web/scss/paralogic_theme.bundle.scss` (this will be built into a CSS file by Frappe/ESBuild)

## Theme Bundle File

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

## Bootstrap Variables Reference

* Refer to https://github.com/twbs/bootstrap/blob/v4.5.0/scss/_variables.scss for a list of all bootstrap's SCSS variables
* Refer to https://github.com/twbs/bootstrap/blob/v4.5.0/scss/_root.scss for a list of all boostrap's *CSS* :root variables

## Common Option Variables

* `$enable-rounded` for border radius on common elements
* `$enable-shadows`
* `$enable-gradients`

## Colors Variables

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

## Fonts and Typography Variables

* You should create a separate font CSS directory and file for letting the browser down the fonts using [Transfonter](https://transfonter.org/)
* Make sure to include your font css in `hooks.py` `web_include_css`
* Font Family: always define `$font-family-sans-serif` along with fallback font similar to actual font
* Headings Size: `$h1-font-size`, ..., `$h6-font-size`
* Headings Margin Bottom: `$headings-margin-bottom`
* Headings Font: you may define `$headings-font-family` (for example `$font-family-serif` for headings)
* Always define font sizes in rem

## Miscellaneous Variables

* Common Border Radius: `$border-radius`, `$border-radius-lg`, `$border-radius-sm`
* Common Shadows: `$box-shadow`, `$box-shadow-sm`, `$box-shadow-lg`
* Define if using tabs or other components: `$component-active-bg`, `$component-active-color`
* Common Transition: `$transition-base`, `$transition-fade`, `$transition-collapse`

## Navbar Variables

* Padding: `$navbar-padding-x`, `$navbar-padding-y`
* `$navbar-light-color`, `$navbar-light-hover-color`, `$navbar-light-active-color`, `$navbar-light-disabled-color`, `$navbar-light-toggler-icon-bg`, `$navbar-light-toggler-border-color` (replace `-light-` with `-dark-` for dark navbar)

## Card Variables

* `$card-spacer-y`, `$card-spacer-x`
* `$card-border-radius`
* `$card-border-color`
* `$card-bg`

## Standalone SCSS Files

You may want to create standalone SCSS files that do not include the whole Frappe/Bootstrap CSS code for various reasons like

* Page specific styling
* Optional component styling

We recommend keeping only common elements (that will be used in multiple pages) in the Theme SCSS file and keeping all the page specific SCSS separate to keep the common theme CSS minimal in size and organized.

To create, bundle, and build a standalone SCSS file

* Create an SCSS bundle file `public/paralogic_web/scss/about.bundle.scss` (will be built by Frappe)
* `@import 'frappe/public/scss/website/variables'` to get access to all the SCSS variables
* Add `{{ include_style("about.bundle.css") }}` in your page HTML file's `{% block style %}` to include it in your page
