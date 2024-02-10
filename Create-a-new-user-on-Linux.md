Frappe does not allow installation on root user. If you do not have a non-root user you can create a new user using the following commands.

**Create a new user**

```bash
sudo adduser frappe
```

**Add user to sudo group**

```bash
usermod -aG sudo frappe
```