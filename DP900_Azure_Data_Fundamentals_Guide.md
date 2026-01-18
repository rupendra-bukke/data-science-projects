# DP900: Azure Data Fundamentals - Complete Learning Guide

## Overview
This notebook covers the Azure Data Fundamentals (DP900) certification exam topics with core concepts, practical examples, tricks, and best practices.

**Exam Details:**
- Exam Code: DP900
- Duration: 60 minutes
- Questions: 40-60
- Passing Score: 70%
- Price: ~$99 USD
- Difficulty: Beginner-Intermediate

**Key Skills Measured:**
- Core data concepts (25-30%)
- Relational data (20-25%)
- Non-relational data (15-20%)
- Analytics and visualization (15-20%)
- Data storage in Azure (10-15%)

---

# Part 1: Core Data Concepts

## 1.1 Data Fundamentals

### What is Data?
- **Data**: Raw facts and figures
- **Information**: Processed data with context
- **Knowledge**: Understanding derived from information

### Data Types
- **Structured**: Organized in tables (databases)
  - Fixed schema
  - Rows and columns
  - Easy to query
  
- **Semi-structured**: Partial organization (JSON, XML)
  - Flexible schema
  - Nested data possible
  - Tags or keys for identification
  
- **Unstructured**: No predefined structure
  - Images, videos, text
  - Large file sizes
  - Requires specialized processing

### TRICK: Identify data types quickly
- Tables with rows/columns → Structured
- JSON, XML files → Semi-structured
- Images, videos, documents → Unstructured

## 1.2 Data Processing Patterns

### Batch Processing
- Process large volumes at once
- Scheduled intervals (daily, weekly)
- Cost-effective
- Delayed results (not real-time)
- Example: Daily report generation

### Stream Processing
- Process data continuously
- Real-time results
- Low latency
- Higher cost
- Example: Stock price updates, sensor data

### Comparison Table
| Aspect | Batch | Stream |
|--------|-------|--------|
| Latency | High | Low |
| Volume | Large | Continuous |
| Cost | Lower | Higher |
| Use Case | Reports | Real-time |
| Example | Daily ETL | Live dashboards |

### TRICK: When to choose
- Historical reports → Batch
- Live dashboards → Stream
- Alert systems → Stream

## 1.3 OLTP vs OLAP

### OLTP (Online Transaction Processing)
- **Purpose**: Daily operations
- **User Type**: End users
- **Transactions**: Many short transactions
- **Data**: Current data (recent)
- **Queries**: Simple, predictable
- **Examples**: Banking app, e-commerce
- **Storage**: Row-oriented (normalized)
- **Performance**: Fast writes

### OLAP (Online Analytical Processing)
- **Purpose**: Historical analysis
- **User Type**: Analysts, managers
- **Transactions**: Few complex transactions
- **Data**: Historical aggregated data
- **Queries**: Complex, ad-hoc
- **Examples**: Business intelligence, dashboards
- **Storage**: Column-oriented (denormalized)
- **Performance**: Fast reads

### TRICK: Quick identification
- "I need to insert a transaction" → OLTP
- "I need to analyze trends" → OLAP
- Real-time app → OLTP
- Analytics platform → OLAP

# Part 2: Relational Data

## 2.1 Relational Database Concepts

### Key Components
- **Table**: Collection of related data (rows and columns)
- **Row**: Single record (tuple)
- **Column**: Attribute or field
- **Primary Key**: Unique identifier for each row
- **Foreign Key**: Reference to another table's primary key
- **Index**: Speeds up data retrieval

### Database Design Concepts
- **Normalization**: Organize data to minimize redundancy
  - 1NF: No repeating groups
  - 2NF: Remove partial dependencies
  - 3NF: Remove transitive dependencies
  
- **Denormalization**: Combine tables for query performance
  - Introduces redundancy
  - Faster queries
  - More storage

### TRICK: Normalization vs Denormalization
- Normalization: Database design (OLTP)
- Denormalization: Analytics design (OLAP)
- Choose based on workload

## 2.2 SQL Fundamentals

### SQL Query Types

**DDL (Data Definition Language)**
```sql
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    Name VARCHAR(100),
    Salary DECIMAL(10, 2)
);

ALTER TABLE Employees ADD Department VARCHAR(50);

DROP TABLE Employees;  -- Deletes entire table
```

**DML (Data Manipulation Language)**
```sql
-- INSERT
INSERT INTO Employees VALUES (1, 'John', 50000, 'Sales');

-- SELECT
SELECT Name, Salary FROM Employees WHERE Salary > 50000;

-- UPDATE
UPDATE Employees SET Salary = 55000 WHERE EmployeeID = 1;

-- DELETE
DELETE FROM Employees WHERE EmployeeID = 1;
```

**DCL (Data Control Language)**
```sql
-- GRANT permissions
GRANT SELECT ON Employees TO user_name;

-- REVOKE permissions
REVOKE INSERT ON Employees FROM user_name;
```

### TRICK: SQL operation acronym
- **CRUD**: Create, Read, Update, Delete
- INSERT (Create), SELECT (Read), UPDATE, DELETE

## 2.3 Relational Database Services in Azure

### Azure SQL Database
- **Type**: Managed SQL Server
- **Deployment**: PaaS (Platform as a Service)
- **Use Case**: OLTP, business applications
- **Scaling**: Automatic
- **Maintenance**: Handled by Azure
- **Cost**: Pay-per-use

### Azure Database for MySQL
- **Type**: Managed MySQL
- **Use Case**: Open-source applications
- **Scaling**: Vertical scaling
- **Popular with**: WordPress, Drupal

### Azure Database for PostgreSQL
- **Type**: Managed PostgreSQL
- **Use Case**: Advanced SQL features
- **Features**: PostGIS (geo-spatial), JSON support
- **Popular with**: Enterprise applications

### Quick Comparison
| Feature | SQL DB | MySQL | PostgreSQL |
|---------|--------|-------|------------|
| Deployment | Cloud | Cloud | Cloud |
| Cost | Higher | Lower | Medium |
| Performance | Highest | Medium | High |
| Enterprise | Yes | Limited | Yes |

### TRICK: Service selection
- Microsoft products → SQL Database
- WordPress/Drupal → MySQL
- Complex queries → PostgreSQL

# Part 3: Non-Relational Data

## 3.1 NoSQL Database Types

### Document Databases
- Store data as documents (JSON, XML)
- Flexible schema
- Nested structures
- Example: MongoDB, Azure Cosmos DB (SQL API)
- Use Case: Web apps, user profiles

```json
{
  "_id": "user123",
  "name": "John Doe",
  "email": "john@example.com",
  "address": {
    "street": "123 Main St",
    "city": "New York"
  },
  "orders": [1001, 1002, 1003]
}
```

### Key-Value Databases
- Simple key-value pairs
- Very fast retrieval
- In-memory caching
- Example: Azure Cache for Redis
- Use Case: Session storage, cache

### Column-Family Databases
- Store data by columns
- Optimized for analytics
- Wide rows
- Example: Apache HBase
- Use Case: Time-series data

### Graph Databases
- Store relationships as edges
- Optimized for queries
- Nodes and relationships
- Example: Azure Cosmos DB (Gremlin API)
- Use Case: Social networks, recommendations

### TRICK: NoSQL type selection
- Flexible JSON data → Document
- Session/cache → Key-Value
- Time-series → Column-Family
- Relationships → Graph

## 3.2 Azure Cosmos DB

### Key Features
- **Multi-model**: SQL, MongoDB, Cassandra, Table, Gremlin APIs
- **Global distribution**: Replicate across regions
- **Consistency levels**: Strong to Eventual
- **Throughput**: Reserved or serverless
- **SLA**: 99.999% availability

### APIs Available
| API | Type | Use Case |
|-----|------|----------|
| SQL | Document | Web apps |
| MongoDB | Document | MongoDB apps |
| Cassandra | Column-Family | Analytics |
| Table | Key-Value | Blob storage |
| Gremlin | Graph | Networks |

### Consistency Levels (Strong → Weak)
1. **Strong**: Most consistent, highest latency, highest cost
2. **Bounded Staleness**: Consistent with max lag
3. **Session**: Consistent within session (default)
4. **Consistent Prefix**: Order guaranteed
5. **Eventual**: Lowest latency, lowest cost

### TRICK: Consistency selection
- Banking → Strong
- User sessions → Session
- Analytics/cache → Eventual

## 3.3 Azure Data Lake and Blob Storage

### Azure Blob Storage
- **Type**: Object storage
- **Use Case**: Unstructured data
- **Blob Types**:
  - Block blobs: Large files (up to 4.75 TB)
  - Append blobs: Logs, append operations
  - Page blobs: VHD disks
- **Access Tiers**:
  - Hot: Frequent access
  - Cool: 30-day minimum
  - Archive: 180-day minimum

### Azure Data Lake Storage (ADLS)
- **Type**: Hierarchical blob storage
- **Features**:
  - Folder/directory structure
  - ACL-based security
  - Optimized for analytics
- **Use Case**: Big data, analytics
- **Format**: Parquet, ORC preferred

### Storage Comparison
| Feature | Blob | ADLS |
|---------|------|------|
| Hierarchy | Flat | Hierarchical |
| Security | Shared access | ACLs |
| Use Case | General | Analytics |
| Performance | Good | Better for analytics |

### TRICK: Storage selection
- Folder-like structure → ADLS
- Random unstructured objects → Blob
- Big data analytics → ADLS

# Part 4: Data Analytics and Visualization

## 4.1 Analytical Workloads

### Exploratory Data Analysis (EDA)
- Investigate data characteristics
- Identify patterns and outliers
- Understand distributions
- Tools: Python (Pandas, NumPy), R, Jupyter

### Descriptive Analytics
- Summarize historical data
- What happened?
- Reports and dashboards
- Example: Sales by region, customer segments

### Diagnostic Analytics
- Understand why events happened
- Root cause analysis
- Drill-down capabilities
- Example: Why did sales drop?

### Predictive Analytics
- Forecast future events
- Machine learning models
- What will happen?
- Example: Customer churn prediction

### Prescriptive Analytics
- Recommend actions
- What should we do?
- Optimization algorithms
- Example: Best pricing strategy

### TRICK: Analytics progression
Descriptive → Diagnostic → Predictive → Prescriptive
(Past → Why → Future → Best Action)

## 4.2 Data Visualization Best Practices

### Visualization Types
| Chart | Use Case | Example |
|-------|----------|----------|
| Line | Trends over time | Stock prices |
| Bar | Categories comparison | Sales by region |
| Pie | Proportions | Market share |
| Scatter | Correlation | Height vs Weight |
| Histogram | Distribution | Age distribution |
| Box Plot | Outliers | Salary ranges |
| Map | Geographic | Regional sales |
| Heat Map | Density | Website heatmap |

### Design Principles
1. **Clarity**: Clear title and labels
2. **Simplicity**: Remove clutter
3. **Accuracy**: Correct data representation
4. **Context**: Provide background
5. **Color**: Use meaningful colors
6. **Accessibility**: Color-blind friendly

### TRICK: Chart selection flow
- Comparing categories → Bar chart
- Showing trends → Line chart
- Showing parts of whole → Pie/Donut
- Showing relationship → Scatter
- Showing distribution → Histogram

## 4.3 Azure Analytics Services

### Power BI
- **Purpose**: Business intelligence and visualization
- **Components**:
  - Power BI Desktop: Development tool
  - Power BI Service: Cloud sharing
  - Power BI Mobile: On-the-go access
- **Features**:
  - Interactive dashboards
  - Real-time updates
  - AI insights
  - Q&A natural language
- **Data Sources**: SQL, Excel, APIs, Web

### Azure Synapse Analytics
- **Purpose**: Large-scale analytics
- **Components**:
  - SQL pools: Big data analysis
  - Spark pools: Machine learning
  - Pipelines: ETL/ELT
- **Use Case**: Enterprise analytics

### Azure Databricks
- **Purpose**: Collaborative data analytics
- **Features**:
  - Apache Spark engine
  - Machine learning support
  - Collaborative notebooks
  - Delta Lake (data quality)

### TRICK: Service selection for analytics
- Business dashboards → Power BI
- Large-scale SQL analytics → Synapse
- ML and data science → Databricks

# Part 5: Data Storage in Azure

## 5.1 Azure Storage Account

### Storage Account Types
- **General-purpose v2**: Default, all services
- **General-purpose v1**: Legacy
- **BlockBlobStorage**: Optimized for blobs
- **FileStorage**: Optimized for file shares
- **StorageV2**: High-performance

### Redundancy Options
1. **LRS (Locally Redundant Storage)**
   - 3 copies in single location
   - Lowest cost
   - Lowest durability

2. **GRS (Geo-Redundant Storage)**
   - 6 copies (3 local + 3 remote)
   - Regional disaster recovery
   - Medium cost

3. **RA-GRS (Read Access GRS)**
   - Can read from secondary
   - Better availability
   - Higher cost

4. **ZRS (Zone-Redundant Storage)**
   - 3 copies in different zones
   - High availability
   - Within region only

### TRICK: Redundancy selection
- Non-critical data → LRS
- Production apps → GRS or RA-GRS
- High availability → RA-GRS
- Cost optimization → LRS

## 5.2 Database Backup and Recovery

### Backup Strategies
- **Full Backup**: Complete copy (baseline)
- **Differential Backup**: Changes since full (faster)
- **Incremental Backup**: Changes since last backup (smallest)
- **Transaction Log Backup**: Point-in-time recovery

### Azure Backup Features
- **Retention**: Hourly, daily, weekly, monthly
- **Geo-redundancy**: Automatic cross-region
- **Point-in-time Recovery**: Restore to specific time
- **Long-term Retention**: Archive old backups

### Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO)
- **RTO**: Maximum acceptable downtime
- **RPO**: Maximum data loss acceptable
- Lower RTO/RPO = Higher cost

### TRICK: Backup planning
- Critical data → Hourly backups, low RTO/RPO
- Historical data → Daily backups, higher RTO/RPO
- Archive data → Less frequent, archived storage

# Part 6: Data Security and Compliance

## 6.1 Data Security Fundamentals

### Security Layers (Defense in Depth)
1. **Physical Security**: Data center access
2. **Network Security**: Firewalls, VNets
3. **Identity & Access**: Authentication, RBAC
4. **Data Protection**: Encryption, masking
5. **Application Security**: Input validation
6. **Monitoring**: Audit logs, alerts

### Authentication Methods
- **Username/Password**: Basic (not recommended alone)
- **Multi-Factor Authentication (MFA)**: 2+ factors
- **Azure AD**: Enterprise identity
- **Service Principal**: App-to-app authentication

### Encryption Types
- **Encryption at Rest**: Data stored encrypted
- **Encryption in Transit**: Data traveling encrypted
- **End-to-End Encryption**: Encrypted throughout
- **TLS (Transport Layer Security)**: Standard for transit

### TRICK: Security implementation
- Enable MFA for all users
- Use SSL/TLS for data transfer
- Encrypt sensitive data at rest
- Regular security audits

## 6.2 Compliance and Data Governance

### Compliance Standards
- **GDPR**: European data protection
- **HIPAA**: Healthcare data (US)
- **PCI-DSS**: Payment card data
- **SOC 2**: Security audit framework
- **ISO 27001**: Information security

### Data Governance
- **Data Classification**: Sensitivity levels
  - Public: No restrictions
  - Internal: Employees only
  - Confidential: Limited access
  - Restricted: Highly sensitive

- **Data Retention**: Keep data policies
  - Minimum: Legal requirements
  - Maximum: Cost optimization

- **Data Lineage**: Track data origin and transformations

- **Data Quality**: Ensure accuracy and completeness

### TRICK: Compliance checklist
- Know applicable standards for your industry
- Classify data by sensitivity
- Encrypt sensitive data
- Maintain audit trails
- Regular compliance reviews

# Part 7: Data Engineering Basics

## 7.1 ETL and ELT Processes

### ETL (Extract, Transform, Load)
```
Source → Extract → Transform → Load → Destination
                (on-premise)           (database)
```
- Transform before loading
- Data quality checks first
- Slower but cleaner
- Traditional approach

### ELT (Extract, Load, Transform)
```
Source → Extract → Load → Transform → Destination
              (cloud)              (cloud)
```
- Load raw data first
- Transform in cloud (scalable)
- Faster ingestion
- Modern approach

### Comparison
| Aspect | ETL | ELT |
|--------|-----|-----|
| Speed | Slow | Fast |
| Complexity | Depends on transform | More flexibility |
| Storage | Small | Large |
| Cloud native | No | Yes |
| Scalability | Limited | High |

### TRICK: Modern choice
- Cloud adoption → ELT
- On-premises → ETL
- Data lakes → ELT

## 7.2 Data Integration Tools

### Azure Data Factory
- **Purpose**: ETL/ELT orchestration
- **Features**:
  - Pipelines for workflows
  - Copy activity for data movement
  - Mapping data flows (visual)
  - Spark/SQL transformations
  - Scheduling and triggers
- **Use Case**: Enterprise data integration

### Azure Synapse Pipelines
- **Purpose**: Unified analytics platform
- **Built on**: Data Factory
- **Additional**: SQL pools, Spark, notebooks
- **Use Case**: Analytics pipeline

### Data Movement Options
1. **Copy Activity**: Simple data transfer
2. **Self-hosted Integration Runtime**: On-premises
3. **Azure Integration Runtime**: Cloud-to-cloud
4. **SSIS Runtime**: Legacy SQL Server

### TRICK: Tool selection
- Simple ETL → Data Factory Copy Activity
- Complex transformations → Synapse Pipelines
- Full analytics → Synapse Analytics

# Part 8: Exam Tips and Quick Reference

## 8.1 Key Concepts Summary

### Data Types
- Structured: Tables
- Semi-structured: JSON, XML
- Unstructured: Files, images

### Processing Patterns
- Batch: Scheduled, large volumes
- Stream: Continuous, real-time

### Database Workloads
- OLTP: Transactions, fast writes
- OLAP: Analytics, complex queries

### Storage Services
- Blob: Unstructured objects
- ADLS: Hierarchical, analytics
- SQL Database: OLTP transactions
- Cosmos DB: NoSQL, global

### Analytics Progression
1. Descriptive: What happened?
2. Diagnostic: Why happened?
3. Predictive: What will happen?
4. Prescriptive: What to do?

## 8.2 Common Exam Patterns

### When you see "Real-time"...
- Stream Analytics
- Event Hubs
- Streaming dataset

### When you see "Large historical data"...
- Data Lake Storage
- Synapse Analytics
- Archive tier

### When you see "No schema changes expected"...
- Relational database
- Normalized schema

### When you see "Flexible schema"...
- Cosmos DB
- Document storage

### When you see "Global distribution"...
- Cosmos DB
- GRS storage
- Multiple regions

## 8.3 Exam Preparation Strategy

### Before the Exam
- Study official exam skills outline
- Take 3-4 practice exams
- Target 85%+ on practice exams
- Get hands-on with Azure services
- Review weak areas
- Know the fundamental concepts

### During the Exam
- Read each question carefully
- Look for keywords (MUST, NOT, best)
- Manage time: ~1 min per question
- Skip hard questions, return later
- Review your answers

### Quick Decision Tree
```
Scenario involves...
├─ Transactions? → SQL Database
├─ Analytics? → Synapse
├─ Real-time? → Stream Analytics
├─ Unstructured data? → Blob/ADLS
├─ Flexible schema? → Cosmos DB
├─ Caching? → Redis
├─ Visualization? → Power BI
└─ Orchestration? → Data Factory
```

### TRICK: Elimination strategy
- Read all options
- Eliminate obviously wrong ones
- Between 2: Choose more recent/modern
- Between similar: Choose more complete

# Part 9: Practice Questions

## Question 1: Data Type Classification
**Scenario**: You have a database of customer transactions with fixed columns and a folder of customer photos. What data types are these?

A) Both structured
B) Both unstructured
C) Transactions are structured, photos are unstructured
D) Transactions are unstructured, photos are structured

**Answer**: C
**Explanation**: Transactions have fixed schema (structured), photos have no structure (unstructured).

---

## Question 2: OLTP vs OLAP
**Scenario**: A system processes customer orders in real-time. Is this OLTP or OLAP?

A) OLAP
B) OLTP
C) Neither
D) Both

**Answer**: B
**Explanation**: Real-time transactions are OLTP (Online Transaction Processing).

---

## Question 3: Storage Selection
**Scenario**: Need to store 1 million customer documents with flexible schema. What's best?

A) Azure SQL Database
B) Azure Cosmos DB
C) Azure Blob Storage
D) Azure Data Lake

**Answer**: B
**Explanation**: Cosmos DB handles documents with flexible schema efficiently.

---

## Question 4: Redundancy Strategy
**Scenario**: Critical business data needs disaster recovery across regions. Which redundancy?

A) LRS
B) GRS
C) ZRS
D) RA-GRS

**Answer**: D (RA-GRS)
**Explanation**: RA-GRS provides cross-region redundancy AND read access.

---

## Question 5: Analytics Type
**Scenario**: Predict which customers will likely leave the company. What type of analytics?

A) Descriptive
B) Diagnostic
C) Predictive
D) Prescriptive

**Answer**: C
**Explanation**: Predictive analytics forecasts future events (customer churn).

# Part 10: Study Resources and Timeline

## Learning Resources

### Official Microsoft Resources
- **Microsoft Learn**: Free training modules
- **Exam Skills Outline**: Download from Microsoft
- **Azure Documentation**: docs.microsoft.com
- **Microsoft Virtual Training Days**: Free instructor-led

### Practice and Hands-on
- **Microsoft Learn Labs**: Free interactive labs
- **Azure Free Tier**: $200 credits for 30 days
- **Practice Exams**: ExamTopics, MeasureUp, Udemy
- **YouTube**: Microsoft and community channels

## 4-Week Study Plan (Beginner Friendly)

### Week 1: Fundamentals
- Day 1-2: Data concepts (structured/unstructured)
- Day 3-4: OLTP vs OLAP
- Day 5: Batch vs Stream processing
- Day 6-7: Review + practice

### Week 2: Data Storage
- Day 1-2: SQL Database basics
- Day 3-4: Blob and ADLS
- Day 5-6: Cosmos DB
- Day 7: Redundancy options

### Week 3: Analytics
- Day 1-2: Analytics types
- Day 3-4: Visualization basics
- Day 5-6: Power BI introduction
- Day 7: Review

### Week 4: Exam Prep
- Day 1-3: Practice exams
- Day 4-5: Review weak areas
- Day 6: Final review
- Day 7: Exam day!

## Success Criteria
- Complete all practice questions
- Achieve 80%+ on practice exams
- Understand core concepts
- Hands-on experience with 3+ services

# Part 11: Final Quick Reference

## Azure Services Quick Reference

| Service | Purpose | Workload |
|---------|---------|----------|
| SQL Database | Relational OLTP | Transactions |
| Synapse | Analytics OLAP | Analytics |
| Cosmos DB | NoSQL Global | Flexible schema |
| Blob Storage | Unstructured | Files, objects |
| ADLS Gen2 | Data lake | Analytics |
| Data Factory | Orchestration | ETL/ELT |
| Power BI | Visualization | BI dashboards |
| Stream Analytics | Real-time | Streaming |
| Redis | Caching | Session/cache |
| Databricks | ML Analytics | Data science |

## Data Concepts Hierarchy

```
Data
├─ Structured (Tables)
│  └─ OLTP (Transactions) OR OLAP (Analytics)
├─ Semi-structured (JSON/XML)
│  └─ Document stores (Cosmos DB)
└─ Unstructured (Files/Media)
   └─ Blob/ADLS Storage
```

## Security Best Practices
- [ ] Enable MFA for all accounts
- [ ] Encrypt sensitive data
- [ ] Use managed identities
- [ ] Implement RBAC
- [ ] Monitor audit logs
- [ ] Use VNets for isolation
- [ ] Regular security reviews
- [ ] Backup critical data

## Pre-Exam Checklist
- [ ] Know all Azure data services
- [ ] Understand OLTP vs OLAP
- [ ] Distinguish data types
- [ ] Know redundancy options
- [ ] Understand analytics types
- [ ] Know visualization best practices
- [ ] Understand ETL vs ELT
- [ ] Know security/compliance basics
- [ ] Score 80%+ on practice exams
- [ ] Get hands-on experience

---

# Congratulations! 🎉

You're ready for the DP900 exam! Remember:
- **Read carefully**: Keywords matter
- **Know the services**: Their purposes and use cases
- **Understand concepts**: Don't just memorize
- **Practice**: Take multiple exams
- **Get hands-on**: Create resources in Azure

**Good Luck! 🚀**
