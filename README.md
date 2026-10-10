## ETL Project + Flask Dashboard

### 📌 Overview

Build an ETL pipeline using Python with three data sources:

* `customers.csv`
* `orders.parquet`
* `products.csv` — retrieved from an API [Link](https://raw.githubusercontent.com/MohammedHameds/test1455/refs/heads/main/products.csv)

Clean, transform, merge the data, load the final Sales table into **SQL Server**, and display it using a **Flask dashboard**.

### 🔄 Transformations

**Customers**

* Remove duplicates
* Standardize city
* Validate age
* Handle missing email
* Create `full_name`

**Orders**

* Remove duplicate `order_id`
* Validate quantity
* Convert `order_date` to datetime
* Validate `customer_id`

**Products**

* Remove duplicates
* Standardize product/category
* Validate `unit_price`
* Convert price to numeric

### 💰 Sales

Merge the three datasets and calculate:

```python
sales["total_amount"] = sales["quantity"] * sales["unit_price"]
```

Final columns:

```text
order_id
customer
product
quantity
unit_price
total_amount
```

### 🔐 Database credentials (.env)

Database credentials are read from a `.env` file at the project root, using `python-dotenv`.

**Setup:**

1. Copy the template: `cp .env.example .env`
2. Edit `.env` and fill in your real SQL Server values.

**.env file structure** — one `KEY=value` pair per line (no quotes needed, `#` starts a comment):

```dotenv
DB_DRIVER=ODBC Driver 18 for SQL Server    # installed ODBC driver name
DB_SERVER=localhost                        # host or "localhost\SQLEXPRESS" / "tcp:host,1433" for Azure
DB_DATABASE=etl_db                         # target database name
```

| Variable      | Meaning                                             |
| ------------- | --------------------------------------------------- |
| `DB_DRIVER`   | ODBC driver name used by the connection string      |
| `DB_SERVER`   | SQL Server host/instance to connect to              |
| `DB_DATABASE` | Database where the `Sales` table is loaded          |


> ⚠️ The `.env` file contains secrets and is listed in `.gitignore` — never commit it.
> Only the placeholder template `.env.example` is tracked in version control.

Install the dependency if needed: `pip install python-dotenv`

### 🗄️ SQL Server

Load the final `Sales` table into SQL Server (credentials loaded from `.env`).

### 🌐 Flask Dashboard

Create a Flask application that:

1. Connects to SQL Server.
2. Retrieves the `Sales` table.
3. Displays the data in an HTML dashboard.

The page is rendered from the template **`templates/dashboard.html`**.

Visit `http://127.0.0.1:5000` to view the dashboard.

