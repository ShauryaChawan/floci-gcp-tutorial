# 98 — BigQuery Commands Cheat Sheet 🚀

> ⚠️ **Important:** This is a revision sheet, not a guarantee that every command is implemented by Floci. Verify the commands exposed by your local environment with `--help`. Production Google Cloud syntax and capabilities should be checked against current documentation.

## CLI discovery

| Command | Purpose |
|---|---|
| `gcloud --version` | Check Google Cloud CLI |
| `gcloud config list` | Show active configuration |
| `gcloud --help` | Discover available commands |
| `gcloud <command> --help` | Inspect command-specific help |

## BigQuery SQL patterns

| Task | SQL pattern |
|---|---|
| Select columns | `SELECT col1, col2 FROM table;` |
| Filter rows | `WHERE condition` |
| Sort | `ORDER BY column DESC` |
| Limit | `LIMIT 10` |
| Count | `COUNT(*)` |
| Sum | `SUM(amount)` |
| Average | `AVG(amount)` |
| Group | `GROUP BY column` |
| Group filter | `HAVING SUM(amount) > 100000` |
| Inner join | `JOIN table2 ON ...` |
| Left join | `LEFT JOIN table2 ON ...` |
| Ranking | `RANK() OVER (ORDER BY metric DESC)` |
| Row numbering | `ROW_NUMBER() OVER (...)` |
| Running total | `SUM(metric) OVER (ORDER BY date)` |

## Restaurant analytics queries

### Total revenue

```sql
SELECT SUM(total_amount) AS revenue
FROM orders
WHERE status = 'COMPLETED';
```

### Revenue by outlet

```sql
SELECT
  outlet_id,
  SUM(total_amount) AS revenue
FROM orders
WHERE status = 'COMPLETED'
GROUP BY outlet_id;
```

### Daily revenue

```sql
SELECT
  order_date,
  SUM(total_amount) AS revenue
FROM orders
WHERE status = 'COMPLETED'
GROUP BY order_date
ORDER BY order_date;
```

### Average order value

```sql
SELECT AVG(total_amount) AS aov
FROM orders
WHERE status = 'COMPLETED';
```

### Date range

```sql
WHERE order_date >= DATE '2026-09-01'
  AND order_date < DATE '2026-10-01'
```

## Performance reminders ⚡

| Practice | Why |
|---|---|
| Select required columns | Avoid unnecessary data processing |
| Filter by partition column | Enables partition pruning when applicable |
| Use appropriate clustering | Helps common filter/group patterns |
| Know table grain | Prevent incorrect aggregations |
| Inspect joins | Avoid accidental row multiplication |
| Limit historical range | Avoid processing data you do not need |

## Interview one-liners 🎤

| Question | Short answer |
|---|---|
| BigQuery? | Managed/serverless analytical data warehouse |
| OLTP? | Transaction-oriented application workload |
| OLAP? | Analytical workload over data, often historical |
| Dataset? | Logical grouping of BigQuery resources/tables |
| Partitioning? | Dividing table data into partitions, often by date/time |
| Clustering? | Organizing data around selected columns for common access patterns |
| BigQuery vs Firestore? | Analytics vs document-oriented application data |
| BigQuery vs Datastore? | Analytics vs operational entity storage |
| BigQuery vs Cloud SQL? | Analytical warehouse vs managed relational operational database |

## Last-minute mental model 🧠

```text
Application
   ↓
Operational database
   ↓
Ingestion / transformation
   ↓
BigQuery
   ↓
SQL analytics
   ↓
Aggregations / JOINs / windows
   ↓
Business insights
```
