Marketplace Management Dashboard (Streamlit)
A web-based marketplace management tool that helps online sellers manage their business in a data-driven way. It loads order data and turns it into simple dashboards showing products, quantities, net profit, margins, and taxes.
What It Does (Planned)
Upload data
Upload order data from CSV or Excel files.
Validate data
Check required columns and basic data types.
Show clear messages when something is wrong.
Analyze performance
Calculate revenue, costs, net profit, margins, and taxes.
Aggregate by product, marketplace, and time period.
Dashboards
Overview with main KPIs.
Product performance (top/bottom products).
Order-level table with filters and search.
Export
Export filtered tables to CSV/Excel for further analysis.
Functional Requirements (Suggested)
Upload one or more CSV/XLSX files with order data.
Validate presence and format of required fields (see data model).
Compute for each order line:
Gross revenue, total cost, net profit, margin %, tax amount.
Provide dashboards with filters by:
Date range, marketplace, product/SKU.
Show an order table with:
Sorting, filtering, and export to CSV/Excel.
Main user flow: Upload → Validate → Analyze → Export.
Non-Functional Requirements (Suggested)
Handle typical datasets up to ~100k rows.
Keep interactions (filters, sorting, charts) under a few seconds.
Show friendly error messages for invalid files.
Run locally by default; no external data upload required.
Organize code into clear modules (ingestion, analytics, UI).
Provide basic logging and simple tests for core logic.
Base Architecture (High-Level)
Streamlit UI
Pages, filters, file upload, and session state.
Data ingestion
Read CSV/XLSX, validate schema, clean data.
Analytics
Compute metrics (revenue, cost, margin, taxes).
Aggregate by product, marketplace, and time.
Visualization
Charts and tables built on top of pandas and Streamlit.
Export
Prepare filtered data for CSV/Excel download.
Simple Architecture Diagram
User (Browser)      |      v Streamlit UI (pages, filters, uploads)      |      v Data Ingestion & Validation (CSV/XLSX -> clean DataFrame)      |      v Analytics (KPIs, aggregations, profit & tax logic)      |      v Visualizations & Exports (charts, tables, CSV/Excel)
Data Model (First Version)
Minimal fields per order line (conceptual):
order_id
order_date
marketplace
sku
product_name
quantity
unit_price
discount (optional)
product_cost
fees (optional)
shipping_cost (optional)
tax_amount
Suggested formulas (conceptual):
gross_revenue = quantity * unit_price - discount
total_cost = product_cost + fees + shipping_cost + tax_amount
net_profit = gross_revenue - total_cost
margin_pct = (net_profit / gross_revenue) * 100 (if gross_revenue > 0)
Suggested Folder Structure
.├─ README.md├─ requirements.txt├─ app/│  ├─ main.py        # Streamlit entrypoint│  ├─ pages/         # Extra pages (overview, products, orders)│  ├─ ingestion/     # File reading and validation│  ├─ analytics/     # Metrics and aggregations│  └─ ui/            # Layouts, charts, tables└─ tests/   ├─ test_ingestion.py   └─ test_analytics.py
Getting Started
Prerequisites
Python 3.10+
pip (and optionally a virtual environment)
Install and Run
git clone <your-repo-url>.gitcd lab-web-app  # or your project folderpython -m venv .venv# Windows (PowerShell).venv\Scripts\Activate.ps1# macOS / Linuxsource .venv/bin/activatepip install -r requirements.txt  # or: pip install streamlit pandasstreamlit run app/main.py
Open the URL shown in the terminal (usually http://localhost:8501).
Minimal Sample Data (Example CSV)
order_id,order_date,marketplace,sku,product_name,quantity,unit_price,discount,product_cost,fees,shipping_cost,tax_amountORD-001,2025-01-05,Amazon,SKU-001,Wireless Mouse,2,20.00,0.00,16.00,4.00,2.00,1.60ORD-002,2025-01-06,Amazon,SKU-002,Keyboard,1,35.00,5.00,18.00,3.50,0.00,2.80
Upload this file in the app to see the first metrics and tables.
Testing (Suggested)
Use pytest for:
Metric functions (net profit, margin, etc.).
Validation functions (required columns, types).
Optionally add formatting/linting with black and ruff.
License & Disclaimer
Choose and document a license (e.g. MIT) here.
This tool is not tax or accounting advice; results depend on the quality of the input data and configured rules.