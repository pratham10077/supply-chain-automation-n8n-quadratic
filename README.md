# Supply-Chain-Automation-n8n-quadratic
End-to-end supply chain automation using n8n (workflow automation) + Quadratic (AI-powered spreadsheet). Automates CSV ingestion from Gmail → Database → Business insights &amp; KPIs.

📦 Supply Chain Automation with n8n & Quadratic
This project demonstrates how to automate data ingestion and analysis for supply chain management using:
n8n – AI-powered workflow automation tool
Postgres / Supabase – Central database for structured, clean data
Quadratic – AI-powered spreadsheet for analysis & business insights
It solves a common real-world problem: manual CSV reports arriving over email, copied into sheets, and analyzed too late to make decisions.

🧭 Problem Statement

Every morning, supply chain teams receive CSV reports by email (e.g., daily orders, stock positions).
Manual download and copy-paste into spreadsheets was time-consuming and error-prone.
No single source of truth → multiple conflicting versions.
Business leaders lacked real-time KPIs like Fill Rate, OTIF, and Backorders.

We needed a way to automate the pipeline:
📧 Gmail → 🛠 n8n → 🗄 Database → 📊 Quadratic → 💡 Insights

⚙️ Technical Architecture
  A[Gmail Trigger] --> B[Extract from CSV File]
  A --> C[Extract from CSV File1]
  B --> D[Insert Rows in Orders Table]
  C --> E[Insert Rows in Inventory Table]
  D --> F[Postgres/Supabase Database]
  E --> F
  F --> G[Quadratic Spreadsheet]
  G --> H[Business Insights & KPIs]

📌 Architecture Highlights
  n8n automates file extraction and data loading.
  Postgres/Supabase provides clean schema for long-term storage.
  Quadratic connects directly to DB for analysis.

🚀 Workflow in Action
  Gmail Trigger – Watches inbox for CSV attachments (e.g., subject: Daily Sales).
  Extract from CSV (Orders) – Parses order data.
  Insert Rows into fact_order_line – Loads structured order data.
  Extract from CSV (Inventory) – Parses inventory snapshot.
  Insert Rows into inventory_snapshot – Loads structured inventory data.
  Quadratic – Connects to DB, calculates KPIs, visualizes results.

📊 KPIs Calculated in Quadratic
  Line Fill Rate = delivery_qty / order_qty
  Volume Fill Rate = Σdelivery_qty / Σorder_qty
  Backorder % = (order_qty – delivery_qty) / order_qty
  OTIF (On Time In Full) = % orders delivered on/before promised date in full
  Stockout Days – Days with zero inventory for SKU

🧑‍💻 Setup Instructions
  1. Clone this Repository
    git clone https://github.com/pratham10077/supply-chain-automation-n8n-quadratic.git
    cd supply-chain-automation-n8n-quadratic

  2. Configure Database
     Create tables using provided schema (schema.sql).
     Add connection credentials to n8n & Quadratic.

  3. Import n8n Workflow
     Open n8n → Import workflow JSON (workflow.json).
     Configure Gmail & DB credentials.
     Test with sample CSVs.

  4. Connect Quadratic
    Open Quadratic → connect to Postgres/Supabase.
    Load tables fact_order_line & inventory_snapshot.
    Use provided final_sheet.xlsx & final_grid.grid for exercises.

🎯 What I Learned
  ✅ Automation saves time – No more manual copy-paste from Gmail.
  ✅ Idempotency matters – Prevents duplicate inserts when workflows rerun.
  ✅ Validation is key – Row counts, schema checks avoid silent errors.
  ✅ AI-powered spreadsheets are serious tools – Quadratic can analyze DB-scale data smoothly.
  ✅ Business > dashboards – Insights like “top 10 SKUs causing 80% of missed fill rate” helped drive action.
