# Day 6 Notes – Student Model, Views & Security in Odoo 18

## Objective

Create the first custom Odoo application that stores Student information using the Odoo ORM and displays it through List and Form views.

---

# Topics Covered

- Odoo ORM Model
- Model Fields
- __init__.py
- __manifest__.py
- Security Access
- List View
- Form View
- Action
- Menu
- Install & Upgrade Module
- Create Student Record

---

# Project Structure

student_management/

├── __init__.py

├── __manifest__.py

├── models/

│   ├── __init__.py

│   └── student.py

├── security/

│   └── ir.model.access.csv

├── views/

│   ├── views.xml

│   └── templates.xml

├── controllers/

├── demo/

└── __pycache__/

---

# Student Model

Location

models/student.py

```python
from odoo import models, fields

class Student(models.Model):
    _name = "student.student"
    _description = "Student"

    name = fields.Char(string="Student Name", required=True)
    roll_no = fields.Char(string="Roll Number")
    age = fields.Integer(string="Age")
    gender = fields.Selection([
        ('male', 'Male'),
        ('female', 'Female')
    ], string="Gender")
    email = fields.Char(string="Email")
    phone = fields.Char(string="Phone")
    dob = fields.Date(string="Date of Birth")
    course = fields.Char(string="Course")
```

---

# Model Registration

models/__init__.py

```python
from . import student
```

---

# Manifest File

__manifest__.py

```python
'depends': ['base'],

'data': [
    'security/ir.model.access.csv',
    'views/views.xml',
],
```

---

# Security File

security/ir.model.access.csv

```csv
id,name,model_id:id,group_id:id,perm_read,perm_write,perm_create,perm_unlink
access_student_student,student.student,model_student_student,,1,1,1,1
```

---

# List View

Odoo 18 uses **list** instead of **tree**.

```xml
<list>
    <field name="name"/>
    <field name="roll_no"/>
    <field name="age"/>
    <field name="gender"/>
    <field name="course"/>
</list>
```

---

# Form View

```xml
<form>
    <sheet>
        <group>
            <field name="name"/>
            <field name="roll_no"/>
            <field name="age"/>
            <field name="gender"/>
            <field name="email"/>
            <field name="phone"/>
            <field name="dob"/>
            <field name="course"/>
        </group>
    </sheet>
</form>
```

---

# Window Action

```xml
<record id="action_student" model="ir.actions.act_window">
    <field name="name">Students</field>
    <field name="res_model">student.student</field>
    <field name="view_mode">list,form</field>
</record>
```

---

# Menu

```xml
<menuitem
    id="menu_student_root"
    name="Student Management"/>

<menuitem
    id="menu_student"
    name="Students"
    parent="menu_student_root"
    action="action_student"/>
```

---

# Important Odoo 18 Change

Old Versions

```xml
<tree>
```

Odoo 18

```xml
<list>
```

Old

```xml
tree,form
```

New

```xml
list,form
```

---

# Upgrade Module

```bash
python3 odoo-bin \
-c debian/odoo.conf \
-d student_db \
-u student_management
```

---

# Run Odoo

```bash
python3 odoo-bin -c debian/odoo.conf
```

---

# Browser

```
http://localhost:8069
```

---

# Student Record Example

Student Name : Ravi

Roll Number : 101

Age : 44

Gender : Male

Email : iniya@gmail.com

Phone : 9876543210

Date of Birth : 01/01/1978

Course : Odoo Development

---

# Learning Outcome

After completing Day 6, you can:

- Create an Odoo Model
- Use Odoo ORM Fields
- Register Models
- Create Security Rules
- Create List Views
- Create Form Views
- Create Window Actions
- Create Menus
- Install Custom Modules
- Upgrade Modules
- Create and Save Records

---

# Key Points

- Every model needs `_name`
- Every model must be imported in `__init__.py`
- Every model needs access rights
- Odoo 18 uses `list` view
- XML files are loaded through `__manifest__.py`
- Actions connect models with views
- Menus make modules accessible

---

# Result

✅ Student Management Module Created Successfully

✅ Student Record Saved Successfully

✅ Module Running Successfully in Odoo 18

---

# Day 6 Status

**Completed Successfully – 100%**
