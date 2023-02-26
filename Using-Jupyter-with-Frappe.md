Change directory to your bench directory and run the command

```bash
cd /path/to/your/bench-directory
bench jupyter
```

This will automatically open a page on your browser, if it does not then you can copy/paste the URL printed on the terminal.

Add the following lines as your first cell in Jupyter to initialize frappe

```python
import frappe
frappe.init(site='site.name', sites_path='/path/to/your/bench-directory/sites')
frappe.connect()
frappe.local.lang = frappe.db.get_default('lang')
frappe.db.connect()
```

Note that your notebooks will be saved in

```
/path/to/your/bench-directory/sites/site.name/jupyter_notebooks/
```