# CardDemo Application - Architecture Discovery Report

> **Generated using CAST Imaging MCP Tools**  
> **Date:** 2025-11-13  
> **Application:** Carddemo  
> **Delivery:** Onboarding-202506170722

---

## Executive Summary

The CardDemo application is a mainframe-based card management system built using COBOL, IBM CICS, and IBM z/OS JCL technologies. This report provides a comprehensive architectural analysis based on static code analysis performed using CAST Imaging tools.

### Key Metrics

| Metric | Value |
|--------|-------|
| **Total Lines of Code** | 32,818 |
| **Total Elements** | 909 |
| **Total Interactions** | 2,083 |
| **Transactions** | 47 |
| **Data Graphs** | 55 |
| **Architectural Components** | 5 |
| **Technology Categories** | 15 |
| **External Packages** | 11 |

---

## Technology Stack

### Primary Technologies

1. **COBOL** - Core business logic implementation
2. **IBM CICS** - Transaction processing and online functionality
3. **IBM z/OS JCL** - Job control and batch processing

### Element Types (38 types identified)

The application utilizes a diverse set of mainframe element types:

- **Data Storage:** JCL Data Set, KSDS VSAM File, PDS Dataset, GDG Dataset, Temporary Dataset, CICS DataSet
- **Programs:** Cobol Batch Program, Cobol Transactional Program, Cobol Program, Unknown Program
- **Code Structure:** Cobol Paragraph, Cobol Section, Cobol CopyBook, Cobol File Link
- **Transaction Processing:** CICS Transaction, CICS Map, CICS Transient Data
- **Job Control:** JCL Job, JCL Step, JCL Procedure, JCL Included
- **Utilities:** IBM Utility, CICS Utility, Data Set Utility

### Interaction Types (37 types identified)

Complex interactions between components including:
- **Data Operations:** READ, WRITE, UPDATE, DELETE, INSERT, SELECT, OPEN, CLOSE
- **Control Flow:** CALL, PERFORM, GOTO, FIRE, EXEC_CICS
- **Relationships:** DEFINE, REFER, RELY_ON, PROTOTYPE, INHERIT, EXTEND, IMPLEMENT
- **Communication:** POST, GET, PAGE_FORWARD, PAGE_INCLUDE, MENTION
- **Error Handling:** CATCH, THROW, RAISE
- **System Operations:** MONITOR, INSTANTIATE, USE, OVERRIDE, INCLUDE, HIDE, INSTANCE_OF, MEMBER, SET

---

## Architectural Components

The application is organized into **5 main architectural components** at the component level:

### 1. Screen Interaction (17 objects)
- **Purpose:** User interface and screen management
- **Role:** Handles mainframe terminal interactions through CICS maps and screens

### 2. Transactional Services (18 objects)
- **Purpose:** Online transaction processing
- **Role:** Manages CICS transactions for real-time operations
- **Dependencies:** Interacts with Logic Services

### 3. Logic Services (176 objects)
- **Purpose:** Core business logic implementation
- **Role:** Central processing hub containing business rules and algorithms
- **Dependencies:** 
  - Receives calls from Batch Services, Data File Services, and Transactional Services
  - Makes calls to Batch Services, Data File Services, Screen Interaction, and Transactional Services

### 4. Data File Services (84 objects)
- **Purpose:** Data access and persistence layer
- **Role:** Manages VSAM files, datasets, and data operations
- **Dependencies:** Interacts with Logic Services

### 5. Batch Services (40 objects)
- **Purpose:** Batch job processing
- **Role:** Handles scheduled jobs and bulk data operations
- **Dependencies:** Interacts with Data File Services and Logic Services

### Component Dependencies

```
Screen Interaction
         ↓
Transactional Services ←→ Logic Services ←→ Batch Services
                              ↓ ↑                ↓
                         Data File Services ←────┘
```

---

## Technology Category Breakdown

At a more granular level, the architecture consists of **15 technology categories**:

| Category | Objects | Description |
|----------|---------|-------------|
| **Cobol Business Logic** | 81 | Core business rules and processing |
| **JCL Business Logic** | 58 | Batch job control logic |
| **DataSet Files** | 44 | Data storage files |
| **JCL Batch Processing** | 40 | Batch job processing infrastructure |
| **CICS Business Logic** | 26 | Online transaction business logic |
| **Dataset File** | 21 | Individual dataset definitions |
| **CICS Transaction Processing** | 18 | Transaction management |
| **Mainframe Presentation** | 17 | User interface elements |
| **IBM Utility** | 9 | IBM system utilities |
| **CICS DataSet Storage** | 8 | CICS file definitions |
| **Cobol Data File Access** | 6 | File I/O operations |
| **Cobol File** | 6 | File declarations |
| **CICS Data Storage** | 5 | CICS data management |
| **Data Set Utility** | 1 | Dataset utilities |
| **CICS Utility** | 1 | CICS utilities |

---

## Transactions and Endpoints

The application exposes **47 transactions** (API/UI endpoints) that can be categorized into:

### CICS Transactions (18 total)

These are online, interactive transactions accessed through CICS terminals:

| Transaction | ID | Size | Description |
|------------|-----|------|-------------|
| **CA00** | 7264 | 41 | Account management entry point |
| **CAUP** | 7266 | 161 | Account update (largest transaction) |
| **CAVW** | 7265 | 89 | Account view |
| **CB00** | 7263 | 69 | Bill management |
| **CC00** | 7259 | 41 | Credit card management entry |
| **CCDL** | 7262 | 81 | Credit card deletion |
| **CCLI** | 7261 | 169 | Credit card listing |
| **CCUP** | 7260 | 97 | Credit card update |
| **CDV1** | 7258 | 2 | Card validation |
| **CM00** | 7257 | 41 | Main menu |
| **CR00** | 7256 | 61 | Report generation |
| **CT00** | 7255 | 75 | Transaction processing |
| **CT01** | 7254 | 75 | Transaction type 01 |
| **CT02** | 7253 | 76 | Transaction type 02 |
| **CU00** | 7252 | 88 | Customer management |
| **CU01** | 7251 | 53 | Customer operation 01 |
| **CU02** | 7250 | 55 | Customer operation 02 |
| **CU03** | 7249 | 55 | Customer operation 03 |

### JCL Batch Jobs (29 total)

These are scheduled or on-demand batch processing jobs:

#### Data File Management Jobs
- **ACCTFILE** (7217) - Account file processing
- **CARDFILE** (7218) - Card file processing
- **CUSTFILE** (7223) - Customer file processing
- **TRANFILE** (7241) - Transaction file processing
- **XREFFILE** (7245) - Cross-reference file processing

#### Transaction Processing Jobs
- **INTCALC** (7229, size: 39) - Interest calculation
- **POSTTRAN** (7231, size: 43) - Transaction posting
- **COMBTRAN** (7221) - Combined transaction processing
- **TRANBKP** (7239) - Transaction backup

#### Report Generation Jobs
- **CREASTMT** (7222, size: 47) - Statement creation
- **TRANREPT** (7243, size: 54) - Transaction report
- **PRTCATBL** (7232) - Print category table

#### Data Read Operations
- **READACCT** (7233) - Read account data
- **READCARD** (7234) - Read card data
- **READCUST** (7235) - Read customer data
- **READXREF** (7236) - Read cross-reference data

#### System Maintenance Jobs
- **CLOSEFIL** (7220) - Close files
- **OEPNFIL** (7230) - Open files
- **DEFCUST** (7225) - Define customer
- **DISCGRP** (7227) - Discount group processing
- **DUSRSECJ** (7228) - User security job
- **CBADMCDJ** (7219) - Card administration job
- **TCATBALF** (7238) - Transaction category balance
- **TRANCATG** (7240) - Transaction category
- **TRANTYPE** (7244) - Transaction type

#### Sample/Utility Jobs
- **CBLDBMS** (7247) - COBOL database sample
- **CICCMP** (7248) - CICS compile
- **CNJBATMP** (7246) - Batch template

### JCL Procedures (1)
- **REPROC** (7267, size: 54) - Reusable procedure

### Transaction Architecture Example

#### Transaction CA00 (Account Entry)
```
CICS Transaction (CA00)
    ↓ EXEC_CICS
Cobol Transactional Program (3 programs)
    ↓ CALL
Cobol Paragraphs (7 paragraphs)
    ↓ READ/PERFORM/FIRE
CICS DataSet → KSDS VSAM File (1 file)
```

#### Transaction CAUP (Account Update - Most Complex)
```
CICS Transaction (CAUP)
    ↓ EXEC_CICS
Cobol Transactional Program (5 programs)
    ↓ CALL/EXEC_CICS
Cobol Paragraphs (28 paragraphs)
    ↓ READ/PERFORM
CICS DataSets (4) → KSDS VSAM Files (3) + JCL Data Set (1)
    ↓ CALL
IBM Utility (1)
```

---

## Data Architecture

The application manages **55 data graphs** (data entity interaction networks):

### Primary Data Entities

#### Account Data (ACCTDATA)
- **AWS.M2.CARDDEMO.ACCTDATA.VSAM.KSDS** (ID: 7190, size: 80)
  - Most complex data entity
  - Accessed by 23 start points
  - Interacts with 5 batch programs, 11 JCL steps, 5 JCL jobs, 3 CICS transactions
  - Central to account management operations

#### Card Data (CARDDATA)
- **AWS.M2.CARDDEMO.CARDDATA.VSAM.KSDS** (ID: 7191, size: 35)
- **AWS.M2.CARDDEMO.CARDDATA.VSAM.AIX** (ID: 7170) - Alternate index

#### Customer Data (CUSTDATA)
- **AWS.M2.CARDDEMO.CUSTDATA.VSAM.KSDS** (ID: 7192, size: 57)
- **AWS.CUSTDATA.CLUSTER** (ID: 7179)
- **AWS.CCDA.CUSTDATA.CLUSTER** (ID: 7180)

#### Cross-Reference Data (CARDXREF)
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.KSDS** (ID: 7209, size: 85)
  - Second most complex data entity
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.AIX.PATH** (ID: 7186, size: 37)
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.AIX** (ID: 7208)

#### Transaction Data (TRANSACT)
- **AWS.M2.CARDDEMO.TRANSACT.VSAM.KSDS** (ID: 7204, size: 71)
- **AWS.M2.CARDDEMO.TRANSACT.VSAM.AIX** (ID: 7198)
- **AWS.M2.CARDDEMO.TRANSACT.BKUP** (ID: 7203) - Backup
- **AWS.M2.CARDDEMO.TRANSACT.DALY** (ID: 7202) - Daily transactions
- **AWS.M2.CARDDEMO.TRANSACT.COMBINED** (ID: 7173)

#### Daily Transaction Data
- **AWS.M2.CARDDEMO.DALYTRAN.PS** (ID: 7188, size: 8)
- **AWS.M2.CARDDEMO.DALYREJS** (ID: 7187, size: 8) - Daily rejects

#### Category and Type Data
- **AWS.M2.CARDDEMO.TCATBALF.VSAM.KSDS** (ID: 7194, size: 25) - Transaction category balance
- **AWS.M2.CARDDEMO.TRANCATG.VSAM.KSDS** (ID: 7201, size: 18) - Transaction category
- **AWS.M2.CARDDEMO.TRANTYPE.VSAM.KSDS** (ID: 7206, size: 18) - Transaction type
- **AWS.M2.CARDDEMO.DISCGRP.VSAM.KSDS** (ID: 7185, size: 13) - Discount group

#### Security and User Data
- **AWS.M2.CARDDEMO.USRSEC.VSAM.KSDS** (ID: 7182, size: 113)
  - Most complex security entity
  - Manages user authentication and authorization

#### Report and Statement Data
- **AWS.M2.CARDDEMO.STATEMNT.HTML** (ID: 7175, size: 16) - HTML statements
- **AWS.M2.CARDDEMO.STATEMNT.PS** (ID: 7174, size: 14) - Print statements
- **AWS.M2.CARDDEMO.TRANREPT** (ID: 7199, size: 20) - Transaction reports

#### Transaction Processing Data
- **AWS.M2.CARDDEMO.TRXFL.VSAM.KSDS** (ID: 7176, size: 30) - Transaction flow
- **AWS.M2.CARDDEMO.SYSTRAN** (ID: 7184, size: 11) - System transactions
- **AWS.M2.CARDDEMO.DATEPARM** (ID: 7200, size: 14) - Date parameters

#### CICS Data
- **JOBS** (ID: 7210) - CICS transient data queue

#### System Libraries and Reference Data
- **CEE.SCEELKED** (ID: 7162) - Language Environment linkedit
- **CEE.SCEELKEX** (ID: 7161) - Language Environment exec
- **CEE.SCEEMAC** (ID: 7159) - Language Environment macros
- **CEE.SCEESAMP** (ID: 7164) - Language Environment samples
- **CSF.SCSFMOD0** (ID: 7163) - Cryptographic services
- **IGY.SIGYCOMP.V63** (ID: 7166) - COBOL compiler
- **OEM.CICSTS.DFHCSD** (ID: 7171) - CICS system definition
- **OEM.CICSTS.V05R06M0.CICS.SDFHCOB** (ID: 7158) - CICS COBOL library
- **OEM.CICSTS.V05R06M0.CICS.SDFHLOAD** (ID: 7172) - CICS load library
- **OEM.CICSTS.V05R06M0.CICS.SDFHMAC** (ID: 7160) - CICS macros
- **AWS.M2.CARDDEMO.CPY** (ID: 7165) - COBOL copybooks

### Data Flow Patterns

The Account Data (ACCTDATA) entity demonstrates typical data flow:

```
KSDS VSAM File (ACCTDATA)
    ↓ DEFINE
Cobol Batch Program (4 programs)
    ↓ CALL
Cobol Paragraphs (51 paragraphs)
    ↓ PERFORM
    ├─ READ operations (6)
    ├─ JCL Step WRITE operations (7)
    └─ JCL Job WRITE operations (5)
        ↓
    CICS DataSet
        ↓ READ
    Cobol Transactional Program (3 programs)
        ↓ EXEC_CICS
    CICS Transaction (3 transactions)
```

### File Organization

- **VSAM KSDS Files:** Primary indexed files for main data storage (18 files)
- **VSAM AIX Files:** Alternate indexes for additional access paths (3 files)
- **GDG Datasets:** Generation data groups for historical data (6 files)
- **PS Files:** Physical sequential files for batch processing (11 files)
- **JCL Data Sets:** Job control and parameter files (12 files)

---

## Package Dependencies

The application depends on **11 external packages** (IBM system utilities and services):

| Package | Component ID | Used Objects | Using Objects | Purpose |
|---------|--------------|--------------|---------------|---------|
| **IDCAMS** | IDCAMS | 1 | 71 | Access Method Services - Most heavily used for VSAM operations |
| **SORT** | SORT | 1 | 10 | Sort utility for data ordering |
| **IEBGENER** | IEBGENER | 1 | 10 | Data set utility for copying |
| **IEFBR14** | IEFBR14 | 1 | 8 | Null program for dataset allocation/deletion |
| **SDSF** | SDSF | 1 | 17 | System Display and Search Facility |
| **HEWL** | HEWL | 1 | 6 | Linkage editor |
| **CEE3ABD** | CEE3ABD | 1 | 18 | Language Environment abnormal termination |
| **IGYCRCTL** | IGYCRCTL | 1 | 4 | COBOL compiler control |
| **ASMA90** | ASMA90 | 1 | 3 | Assembler |
| **DFHCSDUP** | DFHCSDUP | 1 | 2 | CICS system definition utility |
| **CEEDAYS** | CEEDAYS | 1 | 2 | Date manipulation service |

### Package Interaction Insights

- **IDCAMS** is the most critical dependency with 71 interaction points, handling all VSAM file operations
- **CEE3ABD** (18 interactions) and **SDSF** (17 interactions) are heavily used for error handling and job monitoring
- The application relies on standard IBM mainframe utilities for compilation, linking, and data management

---

## Key Architectural Findings

### Strengths

1. **Layered Architecture:** Clear separation between presentation (Screen Interaction), business logic (Logic Services), data access (Data File Services), and batch processing (Batch Services)

2. **Modular Design:** 176 logic service objects provide granular business functionality

3. **Comprehensive Transaction Coverage:** 47 transactions cover both online (CICS) and batch (JCL) processing needs

4. **Robust Data Management:** 55 data graphs with proper indexing (VSAM KSDS/AIX) and backup strategies (GDG datasets)

5. **Mainframe Best Practices:** Uses standard IBM utilities and follows z/OS conventions

### Complexity Indicators

1. **Large Transaction Complexity:** 
   - CAUP transaction (161 objects) and CCLI transaction (169 objects) are highly complex
   - May benefit from decomposition for maintainability

2. **Extensive Data Relationships:**
   - USRSEC data entity (113 objects) indicates complex security logic
   - CARDXREF (85 objects) and ACCTDATA (80 objects) show intricate data access patterns

3. **High Interaction Count:** 2,083 interactions across 909 elements (average ~2.3 interactions per element)

4. **Technology Diversity:** 38 different element types and 37 interaction types indicate a sophisticated system

### Modernization Considerations

1. **CICS Transactions:** 18 CICS transactions could be candidates for RESTful API conversion

2. **Batch Jobs:** 29 JCL batch jobs could be migrated to modern scheduling frameworks

3. **Data Migration:** VSAM files (18 primary KSDS) could be migrated to relational or NoSQL databases

4. **Business Logic:** 81 COBOL business logic objects represent core functionality requiring careful migration

5. **Screen Interaction:** 17 mainframe screen objects could be replaced with modern web/mobile UIs

---

## Component Dependencies Matrix

| From Component | To Component | Relationship |
|----------------|--------------|--------------|
| Batch Services | Data File Services | Data I/O |
| Batch Services | Logic Services | Business processing |
| Data File Services | Logic Services | Data operations |
| Logic Services | Batch Services | Job invocation |
| Logic Services | Data File Services | CRUD operations |
| Logic Services | Screen Interaction | UI updates |
| Logic Services | Transactional Services | Transaction management |
| Transactional Services | Logic Services | Business logic calls |

---

## Technology Distribution

### Code Distribution by Technology

- **COBOL Business Logic:** 26.5% (81/305 code objects)
- **JCL Business Logic:** 19.0% (58/305 code objects)
- **CICS Business Logic:** 8.5% (26/305 code objects)

### Data Distribution by Type

- **DataSet Files:** 44 (72.1% of file objects)
- **Dataset File:** 21 (34.4% of file objects)
- **CICS DataSet Storage:** 8 (13.1% of file objects)

---

## Recommendations

### For Understanding the Application

1. **Start with CICS Transactions:** The 18 CICS transactions provide entry points to understand user-facing functionality
2. **Focus on Logic Services:** The 176 logic service objects contain the core business rules
3. **Map Data Flows:** Use the 55 data graphs to understand how information moves through the system
4. **Review Batch Processing:** The 29 JCL batch jobs reveal scheduled and bulk operations

### For Maintenance

1. **Transaction Complexity:** Review and potentially refactor CAUP (161) and CCLI (169) transactions
2. **Data Entity Complexity:** Monitor USRSEC (113), CARDXREF (85), and ACCTDATA (80) for performance
3. **Dependency Management:** IDCAMS usage (71 points) should be carefully managed during any data layer changes

### For Modernization

1. **API-First Approach:** Convert CICS transactions to microservices/APIs progressively
2. **Data Migration:** Plan VSAM-to-modern database migration with proper indexing strategy
3. **UI Modernization:** Replace 17 mainframe screens with modern responsive interfaces
4. **Batch Modernization:** Migrate JCL jobs to containerized batch processing
5. **Security Enhancement:** Modernize the USRSEC security model to contemporary authentication/authorization

---

## Appendix: Tool Usage Reference

This report was generated using the following CAST Imaging MCP tools:

- `imaging-mcp-applications` - Listed available applications
- `imaging-mcp-stats` - Retrieved application statistics
- `imaging-mcp-architectural_graph` - Analyzed architectural components and relationships
- `imaging-mcp-transactions` - Discovered API/UI endpoints
- `imaging-mcp-data_graphs` - Mapped data entity interaction networks
- `imaging-mcp-packages` - Identified external package dependencies
- `imaging-mcp-transaction_details` - Analyzed specific transaction architectures
- `imaging-mcp-data_graph_details` - Examined data flow patterns

---

## Glossary

- **CICS:** Customer Information Control System - IBM's transaction processing system
- **COBOL:** Common Business-Oriented Language - Legacy programming language
- **GDG:** Generation Data Group - Historical dataset versioning
- **JCL:** Job Control Language - Batch job definition language
- **KSDS:** Key Sequenced Data Set - Indexed VSAM file type
- **VSAM:** Virtual Storage Access Method - IBM's file access method
- **z/OS:** IBM's mainframe operating system

---

*End of Report*
