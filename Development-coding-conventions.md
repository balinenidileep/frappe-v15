# Frappe Development Coding Conventions

## General Guidelines

- **DO NOT REFORMAT FILES** - This makes for unmanageable PRs and merges
- Files with poor formatting will be handled on a one-off basis by ticket as needed
- Only reformat areas where other developers are not working

## Python Coding Standards

### Spacing and Styling
- Use tabs only (4 space tabs)
- No trailing spaces or tabs
- No empty lines with tabs/spaces

### Indentation
- Use a single `\t` (tab) for each indent level
- Do not use spaces
- Indentation must be consistent in Python and JavaScript

**Example:**
```python
# Non-compliant (spaces used):
def bad_function():
    do_something()        # 4 spaces – NOT allowed in core style

# Compliant (tabs used):
def good_function():
	do_something()        # tab character for indent
```

> Note: The Frappe editorconfig enforces `indent_style = tab` globally.

### Line Length
- JSON files: ~99 characters
- Python files: Follows PEP8 (~79-88 characters)
- Long SQL or query-builder chains may exceed this limit
- Break lines to stay within ~100 characters when possible
- Use natural breakpoints (e.g., before operators)

### Function Size
- Keep functions/methods short
- Break functions/methods that exceed ~10 lines of code
- If a function has multiple logical parts, refactor into smaller functions or classes
- Each method should do one thing

### Naming Conventions
- Use `snake_case` for Python variables and functions
- Use `PascalCase` for class names
- Document variables should match the DocType slug (e.g., `sales_order = frappe.get_doc('Sales Order', name)`)
- Document name variables should be suffixed with `_name` (e.g., `sales_order_name`)
- Avoid cryptic or numbered names

### Class Structure
- In a DocType Python file, define one class per DocType
- Name the class after the DocType (spaces removed)
- Example: In `sales_order.py`, use `class SalesOrder(Document):`
- Put top-level functions first, followed by helper functions (reverse dependency order)

### Decorators
- Use Frappe-provided decorators for special cases
- Annotate server-callable functions with `@frappe.whitelist()`
- Always validate inputs in whitelisted methods

### SQL and Queries
- Prefer Frappe's ORM or query builder over raw SQL
- Use `frappe.get_all`, `frappe.db.get_value`, or `frappe.qb`
- For raw SQL, use parameter binding to avoid injection

**Example:**
```python
# Non-compliant (SQL injection risk):
frappe.db.sql("SELECT age FROM tabUser WHERE name='%s'" % user_name)

# Compliant (parameterized):
frappe.db.sql("SELECT age FROM tabUser WHERE name=%s", user_name)
```

### Comments and Documentation
- Write clear but concise comments
- Code should be mostly self-explanatory
- Comments should explain the "why", not restate the "what"
- Don't over-comment trivial lines
- Document non-obvious logic

**Example:**
```python
# Validating quantities to ensure business rule: total qty must equal sum of items
def validate_quantities(self):
	...
```

### Docstrings
- No strict docstring style enforced
- Use docstrings to explain modules/classes when needed

### Commit Messages
- Use Conventional Commits (e.g., `feat:`, `fix:`, etc.)
- Write descriptive commits, especially for shared custom apps

## Project Structure

### Bench Layout
- All Frappe apps reside under the `apps/` folder of a bench
- Example: After running `bench new-app custom_app`, your app appears at `apps/custom_app`
- This folder is a Python package with a standard scaffold

### Modules and Python Packages
- Every Frappe app is divided into modules
- Modules group DocTypes
- Module names are listed in the app's `modules.txt`
- Default module directory matches app name (e.g., `apps/custom_app/custom_app/`)

### Directory Structure

#### Public Assets (`public/`)
- Location for static assets
- Files served via `/assets/{app_name}/...`
- Example: `apps/custom_app/public/img/logo.png` → `/assets/custom_app/img/logo.png`
- Store client-side JavaScript (.js), CSS, and image files here

#### Templates (`templates/`)
- Contains Jinja templates (HTML)
- Used for pages with `{% include %}` tags

#### Web Pages (`www/`)
- Holds static pages and client-side scripts
- Files correspond directly to portal/page routes

#### Python Package Files
Root directory files include:
- `hooks.py` (Frappe hooks)
- `modules.txt`
- `patches.txt`
- `README.md`
- `setup.py`

### DocType Files
Each DocType has the following files in its module folder:
- `<doctype>.json`: Schema/metadata (fields, permissions, etc.)
- `<doctype>.py`: Server-side controller class (subclass of Document)
- `<doctype>.js` (optional): Client-side form script
- `<doctype>_list.js`, `<doctype>_dashboard.js` (optional): List or dashboard behavior

> Note: Frappe expects matching class names and filenames (e.g., `class SalesOrder(Document)` in `sales_order.py` for DocType "Sales Order")
