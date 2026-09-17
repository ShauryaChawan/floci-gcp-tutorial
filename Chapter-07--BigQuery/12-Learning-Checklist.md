# 12 — Learning Checklist ✅

Use this checklist before moving to Chapter 8 — Pub/Sub.

## Concepts 🧠

- [ ] I can explain what BigQuery is.
- [ ] I understand why data warehouses exist.
- [ ] I can explain OLTP vs OLAP.
- [ ] I understand Project → Dataset → Table.
- [ ] I understand schemas and common BigQuery data types.
- [ ] I understand the role of analytical data modeling.

## SQL 🔎

- [ ] I can use `SELECT`.
- [ ] I can filter with `WHERE`.
- [ ] I can sort with `ORDER BY`.
- [ ] I can limit results with `LIMIT`.
- [ ] I can aggregate using `COUNT`, `SUM`, `AVG`, `MIN` and `MAX`.
- [ ] I understand `GROUP BY`.
- [ ] I understand `HAVING`.
- [ ] I can use `INNER JOIN` and `LEFT JOIN`.
- [ ] I understand the basic purpose of window functions.

## Performance ⚡

- [ ] I understand partitioning.
- [ ] I understand clustering.
- [ ] I understand partition pruning.
- [ ] I know why unnecessary columns can increase processing.
- [ ] I know why `SELECT *` is often undesirable for large analytical queries.
- [ ] I understand the importance of knowing table grain before joining and aggregating.

## Architecture 🏗️

- [ ] I can explain operational data vs analytical data.
- [ ] I can explain why an application might use Firestore/Datastore/Cloud SQL plus BigQuery.
- [ ] I can draw an operational → ingestion → BigQuery architecture.
- [ ] I understand where Cloud Storage can fit into batch ingestion.
- [ ] I understand how Pub/Sub could later support event-driven ingestion.
- [ ] I can identify tenant-isolation requirements in analytics.

## Interview readiness 🎤

I should be able to answer without notes:

1. What problem does BigQuery solve?
2. What is a data warehouse?
3. OLTP vs OLAP?
4. BigQuery vs Firestore?
5. BigQuery vs Datastore?
6. BigQuery vs Cloud SQL?
7. What is partitioning?
8. What is clustering?
9. What is partition pruning?
10. GROUP BY vs window functions?
11. INNER JOIN vs LEFT JOIN?
12. How does operational data reach BigQuery?
13. How do you prevent duplicate analytical records?
14. How do you handle late-arriving data?
15. What changes between a Floci lab and real GCP?

## Before Chapter 8 🚀

The key mental model to carry forward is:

```text
Operational systems
      ↓
Business events / data
      ↓
Analytics pipeline
      ↓
BigQuery
      ↓
SQL + insights
```

Chapter 8 will introduce **Pub/Sub**, which gives us a way to reason about the event-driven side of this architecture.
