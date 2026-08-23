# Experiment No. 2
> Compare Transactional vs Analytical Workloads Using Sample Scenarios

## Aim / Objective:
To study the characteristics of OLTP (transactional) and OLAP (analytical) workloads and classify real-world scenarios into the correct workload type with justification.

## Requirements / Tools Used:
A computer with a word processor or spreadsheet, a web browser for Microsoft Learn documentation, and a printed list of business scenarios provided by the instructor.

## Theory / Background:
**Transactional (OLTP)** workloads handle large numbers of small, fast read/write operations — for example, placing an order or transferring money. They demand ACID properties (Atomicity, Consistency, Isolation, Durability), low latency, and normalized schemas.

**Analytical (OLAP)** workloads process large volumes of historical data to answer business questions — for example, "What were monthly sales by region last year?" They favour read-heavy aggregate queries, denormalized or star schemas, and data warehouses.

In Azure, OLTP maps to services like Azure SQL Database, while OLAP maps to Azure Synapse Analytics. Modern architectures often move data from OLTP systems into OLAP stores via ETL/ELT pipelines.

![OLTP vs OLAP architecture](images/lab2/oltp-vs-olap-diagram.png "OLTP vs OLAP with ETL/ELT pipeline")


## Procedure / Steps:
1.  Revise the definitions and properties of OLTP and OLAP workloads from Microsoft Learn (DP-900 learning path).
2.  Prepare a comparison table with parameters: purpose, typical operations, data volume per operation, schema style, latency requirement, users, and example Azure service.
3.  Take at least eight scenarios (see the worksheet below).
4.  Classify each scenario as OLTP or OLAP and write a one-line justification.
5.  Identify which Azure service you would use for each scenario.
6.  Document the comparison table and classifications in the record.

## Sample Code / Data Used:

### OLTP vs OLAP — Reference Comparison

| Parameter              | OLTP                          | OLAP                              |
|-------------------------|-------------------------------|------------------------------------|
| Purpose                 | Run the business             | Analyze the business              |
| Typical Operations      | INSERT / UPDATE / DELETE     | SELECT with aggregates            |
| Data Volume per Query   | Few rows                     | Thousands to millions of rows     |
| Schema Style            | Normalized                   | Star / denormalized               |
| Latency Requirement     | Milliseconds (real-time)     | Seconds to minutes (batch/query)  |
| Typical Users           | Front-line staff, applications | Analysts, data scientists, executives |
| Example Azure Service   | Azure SQL Database            | Azure Synapse Analytics           |

### Scenario Classification Worksheet (completed)

| # | Scenario | Workload Type (OLTP/OLAP) | Suggested Azure Service | Justification |
|---|---|---|---|---|
| a | ATM cash withdrawal | **OLTP** | Azure SQL Database | High-concurrency, simple transactions requiring strict ACID compliance to prevent double-spending. |
| b | Quarterly sales trend dashboard | **OLAP** | Azure Synapse Analytics / Power BI | Involves aggregations over historical sales data across multiple quarters for business intelligence. |
| c | Online ticket booking | **OLTP** | Azure SQL Database | Real-time Seat Allocation and booking; requires immediate row-level locks and transaction safety. |
| d | Churn analysis over 5 years of data | **OLAP** | Azure Synapse Analytics / Databricks | Complex historical scanning and machine learning analysis over multi-year, high-volume datasets. |
| e | Adding an item to a shopping cart | **OLTP** | Azure Cosmos DB | High write throughput, low latency requirement for highly available e-commerce user sessions. |
| f | Fraud pattern mining | **OLAP** | Azure Synapse Analytics / Databricks | Pattern analysis, outlier detection, and machine learning models run over massive historical datasets. |
| g | Hotel check-in system | **OLTP** | Azure SQL Database | Immediate update of room status, guest details, and billing upon physical check-in. |
| h | Demand forecasting | **OLAP** | Azure Synapse Analytics / Azure ML | Statistical aggregation and predictive modeling of historical supply-demand curves to plan future stock. |

## Expected Output / Observations:
- **OLTP Workloads**: Characterized by fast, individual queries (e.g., `INSERT`, `UPDATE` by ID) with immediate response times. The data schema is highly normalized (3NF) to minimize redundancy.
- **OLAP Workloads**: Characterized by complex, read-heavy query patterns involving `SUM`, `AVG`, `GROUP BY` over millions of rows. Data is stored in denormalized formats (Star or Snowflake schemas) optimized for scanning.

## Result / Conclusion:
Transactional (OLTP) and Analytical (OLAP) workloads serve distinct but complementary roles in an enterprise. OLTP systems run the daily business operations in real-time, while OLAP systems analyze the resulting historical data. Moving data from OLTP to OLAP is typically accomplished via ETL (Extract, Transform, Load) pipelines in Azure Data Factory.

## Learning Outcomes:
1. Distinguished the functional design patterns of OLTP and OLAP systems.
2. Understood how relational normalization supports transaction processing and how denormalization optimizes read analytics.
3. Learned to select the correct Azure services (Azure SQL Database vs. Azure Synapse Analytics) based on workload characteristics.

## Precautions / Cost Notes:
* **Performance Isolation**: Never run complex, long-running analytical reports directly against a production OLTP database, as this can lock resources and disrupt front-end operations.
* **Synapse Cost Management**: Azure Synapse Analytics compute (dedicated SQL pools) is billed per hour. Always pause the compute pool when not running active analysis to avoid high idle costs.

