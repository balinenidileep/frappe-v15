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

## DocType Controller for CMS

When you create a DocType in developer mode, it will create a directory in your app like `paralogic_web/doctype/website_homepage/` with files:

* `website_homepage.py` backend controller
* `website_homepage.js` frontend client script
* `website_homepage.json` DocType Meta exported as JSON

To add back end validations and triggers on modifying the document you can update your backend controller. One important code to add in your backend controller is cache invalidation:

```python
class WebsiteHomepage(Document):
	def on_update(self):
		from frappe.website.utils import clear_cache
		clear_cache()
```

The `clear_cache` method can either clear cache for a specific route or clear cache for the whole website. To be safe we will clear cache for the whole website when ever the Website Homepage document is updated/saved.

## Page DocType (Single DocType)

To make a web page dynamic, you can create a Single DocType. A Single DocType is a DocType that has only one record in the database instead of a list of records. When making a DocType, make sure to enable the "Is Single" checkbox.

To add data from your Page DocType into your Jinja context, you can include the Python code in your web page's python file:

```python
def get_context(context):
	context.title = context.data.title or "ParaLogic"
	context.data = frappe.get_single("Website Homepage")

	services = frappe.get_all("Website Service",
		filters={'show_on_homepage': 1},
		order_by="sorting_index, creation")

	context.services = [frappe.get_doc("Website Service", d.name) for d in services]
```

To use the data you added to your Jinja context you can access all the keys you added in the `context` object in your Jinja template

```Jinja
<h1>{{ data.subtitle }}</h1>

<p>{{ data.get_formatted("introduction") }}</p>

<ul>
{% for service in services %}
	<li>{{ service.name }}</li>
{% endfor %}
</ul>
```

## Listing DocType (Generators)
...
