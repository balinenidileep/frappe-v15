You can make your web pages dynamic and editable by creating DocTypes for individual pages and listings. You can then use the DocTypes for updating the context of your web pages. The context can then by used by your Jinja templates to generate content from your database. Frappe provides a "Desk" view for your admin users to configure the system and modify content without having to design an admin panel yourself.

## Built-in DocTypes

### Website Settings

You can configure the following from Website Settings

* Page Title Prefix
* Default Homepage Route (can also be defined in `hooks.py`)
* Logo / Brand Image (can also be overriden in the navbar templates)
* Favicon (can also be defined in `hooks.py`)
* Navbar Links
* Footer Links
* Hide Login Option
* Include Search Bar Option
* Disable Signup Option
* Banner HTML (Above navbar)
* Google Analytics
* Additional `<head>` HTML
* Additional `robots.txt` directives
* Route redirect rules (can also be defined in `hooks.py`)

### Contact Us Settings

You can configure the following from Contact Us Settings

* Address Details
* Contact Details
* Contact Form Query Options
* Contact Form Email Forwarding
* Contact Form Automated Acknowledgement Email Template

## Enable Developer Mode

Before creating DocTypes, make sure `developer_mode` is enabled in your `site_config.json` or `common_site_config.json` so that the DocType is exported in your app. See https://frappeframework.com/docs/user/en/guides/app-development/how-enable-developer-mode-in-frappe.

## DocType Naming

Before creating any DocType, first you need to decide on the name of the DocType. The name of the DocType should be well thought as changing the name of the DocType is difficult

* DocType names should always be singular and in Title Case: `Product Category` instead of `product_categories`
* Make sure the name does not conflict with any existing DocType
* You may prefix the name with `Website` to avoid conflicts for example `Website Product` or `Website Item` or `Website Service`
* You may prefix the name with your website name for example `ParaLogic Service`

Your fields should also have clean and descriptive names:

* "Field Label" should always be in Title Case for ex: `Product Category`
* "Field Name" should always be in snake_case for ex: `product_category`
* Keep your fieldnames simple: `title` instead of `homepage_title`, `description` instead of `card_description`
* Keep your fieldanmes 

## DocType Options for CMS

Some common DocType options to consider when making a CMS DocType:

* The module for your DocTypes should always be your website app's module for example: `ParaLogic Web`
* Enable "Track Changes" so that all changes are logged
* Enable "Make Attachments Public by Default" if the uploaded attachments are not private
* Give full permissions to "Website Manager" role
* Set "Image" DocType property as the image field's fieldname if there is a main image for the DocType

Some common fields to add in your DocType:

* `title` field for page title

Keep your DocType organized and robust

* Keep a clean layout with Section Breaks, Column Breaks and Tab Breaks
* Use relevant field types, do not use Data fieldtype for dates, numbers and currencies
* Add fields in your list view's standard filters (for non-single DocTypes)
* Make fields mandatory if that field is crucial or if missing information can cause issues
* Use Text Editor fieldtype to allow rich text editing
* Use Small Text or Text or Long Text to allow long texts
* Use HTML Editor if the input is meant to be in HTML

## Page DocType (Single DocType)

To make a web page dynamic, you can create a Single DocType. A Single DocType is a DocType that has only one record in the database instead of a list of records. When making a DocType, make sure to enable the "Is Single" checkbox.

To add data from your Page DocType into your Jinja context, you can include the Python code in your web page's python file:

```python
def get_context(context):
	context.title = context.data.title or "ParaLogic"
	context.data = frappe.get_single("ParaLogic Homepage")
```

## Listing DocType (Generators)
...
