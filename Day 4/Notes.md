# Odoo Development Course – Day 4 Notes
## Topic: Odoo Architecture (Three-Tier, MVC, Request Flow, ORM)

**Course:** Odoo Development  
**Day:** 4  
**Status:** ✅ Completed

---

# Learning Objectives

After completing Day 4, I learned:

- Odoo Architecture
- Three-Tier Architecture
- MVC Architecture
- Request Flow
- ORM (Object Relational Mapping)
- PostgreSQL Database
- Odoo Database Structure
- Basic PostgreSQL Commands

---

# 1. What is Odoo Architecture?

Odoo Architecture explains how data moves from the user to the database and back to the user.

Whenever a user:

- Logs in
- Creates a Customer
- Creates a Product
- Confirms a Sales Order
- Creates an Invoice

Odoo follows the same architecture.

```
User
 │
 ▼
Browser
 │
 ▼
Odoo Server
 │
 ▼
ORM
 │
 ▼
PostgreSQL
 │
 ▼
ORM
 │
 ▼
Odoo Server
 │
 ▼
Browser
 │
 ▼
User
```

---

# 2. Three-Tier Architecture

Odoo follows Three-Tier Architecture.

```
+----------------------------------+
| Presentation Layer               |
| Browser                          |
+----------------------------------+

             │
             ▼

+----------------------------------+
| Application Layer                |
| Odoo Server                      |
| Python                           |
| Controllers                      |
| Models                           |
| Business Logic                   |
+----------------------------------+

             │
             ▼

+----------------------------------+
| Database Layer                   |
| PostgreSQL                       |
+----------------------------------+
```

---

## Layer 1 – Presentation Layer

User Interface

Examples

- Login Page
- Dashboard
- CRM
- Sales
- Inventory
- Forms
- Reports

Technologies

- HTML
- CSS
- JavaScript
- XML

---

## Layer 2 – Application Layer

Business Logic Layer

Contains

- Python
- Controllers
- Models
- Security
- ORM

Example

```python
if amount > 10000:
    approval_required = True
```

---

## Layer 3 – Database Layer

Database used

```
PostgreSQL
```

Stores

- Customers
- Products
- Employees
- Sales Orders
- Purchase Orders
- Attendance
- Invoices
- Users
- Permissions

---

# 3. MVC Architecture

MVC means

- Model
- View
- Controller

```
User

↓

View (XML)

↓

Controller

↓

Model

↓

ORM

↓

PostgreSQL
```

---

## Model

Written in

```
Python
```

Stores

- Business Logic
- Database Records

Example

```python
from odoo import models, fields

class Student(models.Model):
    _name = "student.student"

    name = fields.Char()
```

---

## View

Written in

```
XML
```

Examples

- Form View
- Tree View
- Kanban View
- Calendar View
- Search View

Example

```xml
<form>
    <sheet>
        <group>
            <field name="name"/>
        </group>
    </sheet>
</form>
```

---

## Controller

Written in

```
Python
```

Handles

- HTTP Requests
- User Requests
- Response

Example

```python
from odoo import http

class Student(http.Controller):

    @http.route('/student')
    def student(self):
        return "Hello Student"
```

---

# 4. ORM (Object Relational Mapping)

ORM allows Python code to communicate with PostgreSQL without writing SQL.

Without ORM

```sql
SELECT * FROM res_partner;
```

With ORM

```python
self.env['res.partner'].search([])
```

ORM automatically converts Python code into SQL.

---

# CRUD Operations

## Create

```python
self.env['res.partner'].create({
    'name': 'Sugumar'
})
```

---

## Read

```python
self.env['res.partner'].search([])
```

---

## Update

```python
partner.write({
    'name': 'Sugumar R'
})
```

---

## Delete

```python
partner.unlink()
```

---

# ORM Flow

```
Python

↓

ORM

↓

SQL

↓

PostgreSQL
```

---

# 5. Request Flow

```
User

↓

Browser

↓

HTTP Request

↓

Odoo Server

↓

Controller

↓

Model

↓

ORM

↓

PostgreSQL

↓

ORM

↓

Model

↓

Controller

↓

Browser

↓

User
```

---

# 6. PostgreSQL Database

PostgreSQL is an open-source Relational Database Management System (RDBMS).

It stores

- Customers
- Products
- Employees
- Users
- Sales Orders
- Purchase Orders
- Stock
- Accounting
- Contacts

Database used

```
odoo18db
```

---

# PostgreSQL Architecture

```
Browser

↓

Odoo Server

↓

ORM

↓

PostgreSQL
```

---

# Important Tables

| Table | Purpose |
|--------|---------|
| res_partner | Customers & Contacts |
| res_users | Users |
| product_template | Products |
| sale_order | Sales Orders |
| purchase_order | Purchase Orders |
| account_move | Accounting Entries |
| stock_move | Inventory |
| ir_model | Models |
| ir_ui_view | Views |

---

# PostgreSQL Commands Practiced

## Open PostgreSQL

```bash
sudo -u postgres psql
```

---

## List Databases

```sql
\l
```

---

## Connect to Odoo Database

```sql
\c odoo18db
```

---

## List Tables

```sql
\dt
```

---

## Show Contacts

```sql
SELECT id, name FROM res_partner LIMIT 10;
```

---

## Count Contacts

```sql
SELECT COUNT(*) FROM res_partner;
```

---

## Show Users

```sql
SELECT id, login FROM res_users;
```

---

## Describe Table

```sql
\d res_partner
```

---

## Exit PostgreSQL

```sql
\q
```

---

# Day 4 Practical Completed

Successfully completed:

- Connected to PostgreSQL
- Listed databases
- Connected to Odoo database
- Listed all tables
- Viewed contact records
- Counted records
- Viewed Odoo users
- Exited PostgreSQL

---

# Advantages of Odoo Architecture

- Modular Design
- Secure
- Scalable
- Easy Maintenance
- Reusable Code
- Fast Development
- Clean Separation of Layers

---

# Advantages of ORM

- No SQL required
- Faster Development
- More Secure
- Easy Maintenance
- Cleaner Code

---

# Interview Questions

### 1. What architecture does Odoo follow?

Answer:

Three-Tier Architecture and MVC Architecture.

---

### 2. Which database does Odoo use?

Answer:

PostgreSQL.

---

### 3. What is ORM?

Answer:

ORM (Object Relational Mapping) converts Python code into SQL automatically.

---

### 4. Which language is used for Models?

Answer:

Python.

---

### 5. Which language is used for Views?

Answer:

XML.

---

### 6. What is the role of Controller?

Answer:

Handles HTTP requests between the browser and the model.

---

# Key Points to Remember

- Browser is the Presentation Layer.
- Odoo Server is the Application Layer.
- PostgreSQL is the Database Layer.
- Models are written in Python.
- Views are written in XML.
- ORM connects Python with PostgreSQL.
- Every request passes through Browser → Odoo Server → ORM → PostgreSQL.

---

# Day 4 Summary

| Topic | Status |
|--------|--------|
| Odoo Architecture | ✅ |
| Three-Tier Architecture | ✅ |
| MVC | ✅ |
| Request Flow | ✅ |
| ORM | ✅ |
| PostgreSQL | ✅ |
| Database Commands | ✅ |
| Practical Session | ✅ |

---

# Day 4 Status

**Theory:** ✅ Completed

**Practical:** ✅ Completed

**Database Practice:** ✅ Completed

**Overall Completion:** **100%**

---

# Next Topic (Day 5)

- Create First Custom Module
- Scaffold Command
- Module Folder Structure
- __manifest__.py
- __init__.py
- Python Models
- XML Views
- Install Custom Module
- First CRUD Application
