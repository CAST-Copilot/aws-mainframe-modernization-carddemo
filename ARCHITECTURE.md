# CardDemo Application - Architecture Discovery Report

**Generated:** 2025-11-13  
**Application:** Carddemo  
**Analysis Tool:** CAST Imaging MCP  
**Delivery Date:** 2025-06-17T07:22:00

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Application Overview](#application-overview)
3. [Technology Stack](#technology-stack)
4. [Architectural Components](#architectural-components)
5. [Application Statistics](#application-statistics)
6. [Transactions & Entry Points](#transactions--entry-points)
7. [Data Architecture](#data-architecture)
8. [Program Inventory](#program-inventory)
9. [External Dependencies & Packages](#external-dependencies--packages)
10. [Quality & Security Insights](#quality--security-insights)
11. [Architectural Patterns](#architectural-patterns)
12. [Component Relationships](#component-relationships)

---

## Executive Summary

CardDemo is a comprehensive mainframe credit card management application designed to showcase AWS and partner technologies for mainframe migration and modernization scenarios. The application demonstrates realistic mainframe patterns including COBOL programming, CICS transaction processing, VSAM data management, and batch processing with JCL.

### Key Metrics
- **Total Lines of Code:** 32,818
- **Total Elements:** 909
- **Total Interactions:** 2,083
- **Transactions (Entry Points):** 47
- **Data Graphs:** 55
- **COBOL Programs:** 29
- **Component Groups:** 5 major architectural layers

---

## Application Overview

CardDemo simulates a complete credit card management system with capabilities for:

- **Customer Management:** Account creation, updates, and maintenance
- **Card Management:** Credit card issuance, updates, and lifecycle management
- **Transaction Processing:** Authorization, posting, and reconciliation
- **Billing & Payments:** Statement generation and payment processing
- **User Administration:** Security and user access management
- **Reporting:** Transaction reports and analytics

The application is architected to support both online (CICS) and batch (JCL) processing modes, demonstrating typical mainframe application patterns.

---

## Technology Stack

### Primary Technologies

| Technology | Purpose | Usage |
|------------|---------|-------|
| **COBOL** | Business logic implementation | 29 programs (batch & online) |
| **IBM CICS** | Online transaction processing | 18 CICS transactions |
| **IBM z/OS JCL** | Batch job orchestration | 40+ batch jobs |
| **VSAM KSDS** | Primary data storage | Multiple key-sequenced datasets |
| **BMS** | Screen definition & mapping | 17 screen maps |

### Supporting Technologies

- **VSAM AIX:** Alternate indexes for optimized data access
- **GDG (Generation Data Groups):** Versioned dataset management
- **CICS Transient Data:** Queue management
- **JCL Utilities:** IDCAMS, IEBGENER, SORT, IEFBR14
- **Assembler:** System-level utilities (MVSWAIT, COBDATFT)

---

## Architectural Components

The CardDemo application is organized into **5 major architectural layers** based on CAST taxonomy analysis:

### 1. **Screen Interaction Layer**
- **Elements:** 17 objects
- **Purpose:** User interface presentation
- **Components:** BMS maps for terminal display
- **Technologies:** IBM CICS BMS

### 2. **Transactional Services Layer**
- **Elements:** 18 objects
- **Purpose:** Online transaction management
- **Components:** CICS transaction definitions
- **Technologies:** IBM CICS, COBOL

### 3. **Logic Services Layer**
- **Elements:** 176 objects
- **Purpose:** Business logic processing
- **Sub-components:**
  - **Business Logic:** 176 objects - Core business rules and processing
  - **Data Access Services:** 6 objects - Data access abstraction
- **Technologies:** COBOL programs, procedures, sections

### 4. **Data File Services Layer**
- **Elements:** 84 objects
- **Purpose:** Data persistence and storage
- **Sub-components:**
  - **DataSet Storage:** 73 objects - Primary VSAM and sequential files
  - **File Storage:** 27 objects - Temporary and utility files
  - **Local Persistence:** 5 objects - Session and transient data
- **Technologies:** VSAM KSDS, GDG, Sequential files

### 5. **Batch Services Layer**
- **Elements:** 40 objects
- **Purpose:** Batch processing and job orchestration
- **Sub-components:**
  - **Script Batch Interfaces:** 40 objects - JCL jobs and procedures
- **Technologies:** IBM z/OS JCL, COBOL batch programs

### Component Interaction Map

```
┌─────────────────────────────────────────────────────────┐
│           Screen Interaction (17 objects)               │
│                    BMS Maps                             │
└───────────────────┬─────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────┐
│      Transactional Services (18 objects)                │
│              CICS Transactions                          │
└───────────────────┬─────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────┐
│         Logic Services (176 objects)                    │
│    ┌─────────────────┬──────────────────────────┐      │
│    │ Business Logic  │  Data Access Services    │      │
│    │   (176 objs)    │      (6 objs)            │      │
│    └─────────────────┴──────────────────────────┘      │
└──────┬──────────────────────────────────────────────────┘
       │                                    ▲
       ▼                                    │
┌─────────────────────────────────────────────────────────┐
│         Data File Services (84 objects)                 │
│    ┌─────────────┬─────────────┬───────────────┐       │
│    │  DataSet    │    File     │    Local      │       │
│    │  Storage    │   Storage   │ Persistence   │       │
│    │  (73 objs)  │  (27 objs)  │   (5 objs)    │       │
│    └─────────────┴─────────────┴───────────────┘       │
└─────────────────────────────────────────────────────────┘
       ▲
       │
┌──────┴──────────────────────────────────────────────────┐
│         Batch Services (40 objects)                     │
│         Script Batch Interfaces                         │
└─────────────────────────────────────────────────────────┘
```

---

## Application Statistics

### Code Metrics

| Metric | Value |
|--------|-------|
| Lines of Code (LOC) | 32,818 |
| Total Elements | 909 |
| Total Interactions | 2,083 |
| Element Types | 23 different types |

### Element Type Distribution

| Element Type | Count |
|--------------|-------|
| JCL Data Set | Multiple |
| Cobol Programs | 29 |
| CICS Transactions | 18 |
| CICS Maps | 17 |
| JCL Jobs | 40+ |
| Cobol CopyBooks | Multiple |
| VSAM KSDS Files | Multiple |
| GDG Datasets | Multiple |
| Cobol Paragraphs | Multiple |
| Cobol Sections | Multiple |

### Interaction Types

The application uses 37 different interaction types including:
- **CALL** - Program-to-program invocations
- **READ/WRITE** - Data file operations
- **EXEC_CICS** - CICS command execution
- **PERFORM** - COBOL paragraph execution
- **INCLUDE** - Copybook inclusions
- **SELECT/USE** - File and resource selection
- **OPEN/CLOSE** - File management
- And 30 more interaction patterns

---

## Transactions & Entry Points

The application exposes **47 transaction entry points**, divided between online CICS transactions and batch JCL jobs.

### Online CICS Transactions (18 Transactions)

#### User Interface Transactions

| Transaction | Size | Stack | Purpose | Program |
|-------------|------|-------|---------|---------|
| **CC00** | 41 | COBOL, CICS, JCL | Signon Screen | COSGN00C |
| **CM00** | 41 | COBOL, CICS, JCL | Main Menu | COMEN01C |
| **CAVW** | 89 | COBOL, CICS, JCL | Account View | COACTVWC |
| **CAUP** | 161 | COBOL, CICS, JCL | Account Update | COACTUPC |
| **CCLI** | 169 | COBOL, CICS, JCL | Credit Card List | COCRDLIC |
| **CCDL** | 81 | COBOL, CICS, JCL | Credit Card Details | COCRDSLC |
| **CCUP** | 97 | COBOL, CICS, JCL | Credit Card Update | COCRDUPC |
| **CT00** | 75 | COBOL, CICS, JCL | Transaction List | COTRN00C |
| **CT01** | 75 | COBOL, CICS, JCL | Transaction View | COTRN01C |
| **CT02** | 76 | COBOL, CICS, JCL | Transaction Add | COTRN02C |
| **CR00** | 61 | COBOL, CICS, JCL | Transaction Reports | CORPT00C |
| **CB00** | 69 | COBOL, CICS, JCL | Bill Payment | COBIL00C |

#### Administrative Transactions

| Transaction | Size | Stack | Purpose | Program |
|-------------|------|-------|---------|---------|
| **CA00** | 41 | COBOL, CICS, JCL | Admin Menu | COADM01C |
| **CU00** | 88 | COBOL, CICS, JCL | List Users | COUSR00C |
| **CU01** | 53 | COBOL, CICS, JCL | Add User | COUSR01C |
| **CU02** | 55 | COBOL, CICS, JCL | Update User | COUSR02C |
| **CU03** | 55 | COBOL, CICS, JCL | Delete User | COUSR03C |

#### Utility Transactions

| Transaction | Size | Stack | Purpose |
|-------------|------|-------|---------|
| **CDV1** | 2 | COBOL, CICS | Date/Time Utility |

### Batch JCL Jobs (29+ Jobs)

#### Data Management Jobs

| Job Name | Size | Stack | Purpose |
|----------|------|-------|---------|
| **ACCTFILE** | 7 | JCL | Load Account Master |
| **CARDFILE** | 15 | COBOL, JCL | Load Card Data |
| **CUSTFILE** | 10 | COBOL, JCL | Load Customer Data |
| **XREFFILE** | 12 | JCL | Load Cross-Reference |
| **TRANFILE** | 15 | COBOL, JCL | Load Transaction Data |
| **TRANCATG** | 7 | JCL | Load Transaction Categories |
| **TRANTYPE** | 7 | JCL | Load Transaction Types |
| **DISCGRP** | 7 | JCL | Load Disclosure Groups |
| **TCATBALF** | 7 | JCL | Load Category Balances |
| **DUSRSECJ** | 10 | JCL | Setup User Security |

#### Processing Jobs

| Job Name | Size | Stack | Purpose |
|----------|------|-------|---------|
| **POSTTRAN** | 43 | COBOL, JCL | Transaction Posting |
| **INTCALC** | 39 | COBOL, JCL | Interest Calculation |
| **CREASTMT** | 47 | COBOL, JCL | Statement Generation |
| **TRANREPT** | 54 | COBOL, JCL | Transaction Report |

#### Utility Jobs

| Job Name | Size | Stack | Purpose |
|----------|------|-------|---------|
| **CLOSEFIL** | 3 | COBOL, JCL | Close VSAM Files |
| **OEPNFIL** | 3 | COBOL, JCL | Open VSAM Files |
| **TRANBKP** | 14 | JCL | Transaction Backup |
| **COMBTRAN** | 9 | JCL | Combine Transactions |
| **DEFCUST** | 6 | JCL | Define Customer Files |
| **PRTCATBL** | 15 | JCL | Print Category Table |

#### Compilation & Setup Jobs

| Job Name | Size | Stack | Purpose |
|----------|------|-------|---------|
| **CBADMCDJ** | 6 | COBOL, JCL | Admin Compile |
| **CBLDBMS** | 24 | COBOL, JCL | BMS Compilation |
| **CICCMP** | 28 | COBOL, JCL | CICS Compile |
| **CNJBATMP** | 21 | COBOL, JCL | Batch Compile |

#### Data Reading Jobs

| Job Name | Size | Stack | Purpose |
|----------|------|-------|---------|
| **READACCT** | 14 | COBOL, JCL | Read Account Data |
| **READCARD** | 13 | COBOL, JCL | Read Card Data |
| **READCUST** | 13 | COBOL, JCL | Read Customer Data |
| **READXREF** | 13 | COBOL, JCL | Read Cross-Reference |

---

## Data Architecture

The application manages **55 data graphs** (data entity interaction networks), representing the complex data relationships and persistence patterns.

### Core Data Entities

#### 1. Customer Data
- **AWS.M2.CARDDEMO.CUSTDATA.VSAM.KSDS** (57 interactions)
- **Purpose:** Customer master records
- **Access Pattern:** Direct keyed access via VSAM KSDS
- **Used by:** 57 program interactions

#### 2. Account Data
- **AWS.M2.CARDDEMO.ACCTDATA.VSAM.KSDS** (80 interactions)
- **Purpose:** Account master information
- **Access Pattern:** Direct keyed access
- **Used by:** 80 program interactions

#### 3. Card Data
- **AWS.M2.CARDDEMO.CARDDATA.VSAM.KSDS** (35 interactions)
- **AWS.M2.CARDDEMO.CARDDATA.VSAM.AIX** (4 interactions)
- **Purpose:** Credit card records with alternate index
- **Access Pattern:** Primary key and alternate index access
- **Used by:** 39 total program interactions

#### 4. Cross-Reference Data
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.KSDS** (85 interactions)
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.AIX** (3 interactions)
- **AWS.M2.CARDDEMO.CARDXREF.VSAM.AIX.PATH** (37 interactions)
- **Purpose:** Links customers, accounts, and cards
- **Access Pattern:** Multi-keyed access with alternate index path
- **Used by:** 125 total program interactions

#### 5. Transaction Data
- **AWS.M2.CARDDEMO.TRANSACT.VSAM.KSDS** (71 interactions)
- **AWS.M2.CARDDEMO.TRANSACT.VSAM.AIX** (7 interactions)
- **Purpose:** Online transaction records
- **Access Pattern:** Primary and indexed access
- **Used by:** 78 total program interactions

#### 6. User Security
- **AWS.M2.CARDDEMO.USRSEC.VSAM.KSDS** (113 interactions)
- **Purpose:** User authentication and authorization
- **Access Pattern:** Keyed access by user ID
- **Used by:** 113 program interactions (highest usage)

### Reference Data Files

| File | Interactions | Purpose |
|------|--------------|---------|
| **TRANTYPE.VSAM.KSDS** | 18 | Transaction type codes |
| **TRANCATG.VSAM.KSDS** | 18 | Transaction categories |
| **TCATBALF.VSAM.KSDS** | 25 | Category balance tracking |
| **DISCGRP.VSAM.KSDS** | 13 | Disclosure group definitions |

### Transient & Working Storage

| File | Interactions | Purpose |
|------|--------------|---------|
| **DALYTRAN.PS** | 8 | Daily transaction staging |
| **SYSTRAN (GDG)** | 11 | System transaction history |
| **TRANREPT (GDG)** | 20 | Transaction report output |
| **STATEMNT.PS** | 14 | Statement print file |
| **STATEMNT.HTML** | 16 | Statement HTML output |

### Generation Data Groups (GDG)

The application uses GDGs for versioned data management:

| GDG | Purpose |
|-----|---------|
| **AWS.M2.CARDDEMO.SYSTRAN** | System transaction logs |
| **AWS.M2.CARDDEMO.TRANSACT.BKUP** | Transaction backups |
| **AWS.M2.CARDDEMO.TRANSACT.DALY** | Daily transaction snapshots |
| **AWS.M2.CARDDEMO.TRANSACT.COMBINED** | Combined transaction files |
| **AWS.M2.CARDDEMO.TRANREPT** | Transaction reports |
| **AWS.M2.CARDDEMO.TCATBALF.BKUP** | Balance backups |
| **AWS.M2.CARDDEMO.DALYREJS** | Daily rejection records |

### Data File Characteristics

| Characteristic | Details |
|----------------|---------|
| **Primary Storage Type** | VSAM KSDS (Key-Sequenced Data Set) |
| **Index Support** | AIX (Alternate Index) for multi-key access |
| **Backup Strategy** | GDG-based versioning |
| **Record Formats** | Fixed Block (FB) - 80, 150, 300, 350, 500 bytes |
| **Access Methods** | Direct keyed, Sequential, Alternate index paths |

---

## Program Inventory

### COBOL Programs (29 Total)

#### Batch Programs (10)

| Program | Purpose | Type |
|---------|---------|------|
| **CBACT01C** | Account file reader | Batch |
| **CBACT02C** | Account cross-reference | Batch |
| **CBACT03C** | Account card processor | Batch |
| **CBACT04C** | Interest calculation | Batch |
| **CBCUS01C** | Customer file processor | Batch |
| **CBSTM03A** | Statement generation (main) | Batch |
| **CBSTM03B** | Statement generation (sub) | Batch |
| **CBTRN02C** | Transaction posting | Batch |
| **CBTRN03C** | Transaction reporting | Batch |

#### Online Transactional Programs (18)

| Program | Purpose | Type | Transaction |
|---------|---------|------|-------------|
| **COSGN00C** | Signon handler | Online | CC00 |
| **COMEN01C** | Main menu | Online | CM00 |
| **COACTVWC** | Account view | Online | CAVW |
| **COACTUPC** | Account update | Online | CAUP |
| **COCRDLIC** | Card list | Online | CCLI |
| **COCRDSLC** | Card details | Online | CCDL |
| **COCRDUPC** | Card update | Online | CCUP |
| **COTRN00C** | Transaction list | Online | CT00 |
| **COTRN01C** | Transaction view | Online | CT01 |
| **COTRN02C** | Transaction add | Online | CT02 |
| **CORPT00C** | Report menu | Online | CR00 |
| **COBIL00C** | Bill payment | Online | CB00 |
| **COADM01C** | Admin menu | Online | CA00 |
| **COUSR00C** | User list | Online | CU00 |
| **COUSR01C** | User add | Online | CU01 |
| **COUSR02C** | User update | Online | CU02 |
| **COUSR03C** | User delete | Online | CU03 |
| **CSUTLDTC** | Date utility | Online | Utility |

#### Utility Programs (1)

| Program | Purpose | Type |
|---------|---------|------|
| **CBTRN01C** | Transaction utility | Generic |

#### External References (1)

| Program | Purpose | Type |
|---------|---------|------|
| **COCRDSEC** | Security module | External (prototype) |

### Program Naming Convention

The application follows a consistent naming convention:

- **CB prefix:** Batch programs
- **CO prefix:** Online (CICS) programs
- **CS prefix:** Shared utilities
- **Suffix C:** COBOL programs
- **Suffix A/B:** Sub-programs or variants

---

## External Dependencies & Packages

The application relies on **11 external packages** and utilities:

### System Utilities (IBM Mainframe)

| Package | Purpose | Usage Count |
|---------|---------|-------------|
| **IDCAMS** | VSAM file management | 71 usages |
| **SORT** | Data sorting utility | 10 usages |
| **IEBGENER** | Dataset copy utility | 10 usages |
| **IEFBR14** | Dummy program for file operations | 8 usages |
| **SDSF** | System Display and Search Facility | 17 usages |
| **HEWL** | Linkage editor | 6 usages |
| **ASMA90** | Assembler | 3 usages |

### COBOL Runtime & Compiler

| Package | Purpose | Usage Count |
|---------|---------|-------------|
| **IGYCRCTL** | COBOL compiler control | 4 usages |
| **CEE3ABD** | Language Environment termination | 18 usages |
| **CEEDAYS** | Date conversion routine | 2 usages |

### CICS Utilities

| Package | Purpose | Usage Count |
|---------|---------|-------------|
| **DFHCSDUP** | CICS system definition | 2 usages |

### Package Dependency Summary

- **Most Critical Dependency:** IDCAMS (71 usages) - Essential for VSAM file management
- **Runtime Critical:** CEE3ABD (18 usages) - Error handling and abnormal termination
- **System Management:** SDSF (17 usages) - Job monitoring and system display

---

## Quality & Security Insights

### Quality Assessment

Based on CAST Imaging structural analysis:

#### Identified Issues

**1. Buffer Overflow Risk (Rule 8478)**
- **Category:** CWE-119, CWE-120, CWE-676, CWE-77, CWE-78, CWE-79, CWE-89, CWE-943
- **Factor:** Security
- **Severity:** Critical
- **Occurrences:** 5 objects affected
- **Description:** Buffer overruns possible when using ADD, SUBTRACT, MULTIPLY, DIVIDE & COMPUTE statements inside loops without SIZE ERROR checking

**Details:**
```
The following statements perform arithmetic operations inside loops:
- ADD, SUBTRACT, MULTIPLY, DIVIDE, COMPUTE
Without proper ON SIZE ERROR handling, these can cause buffer overflows
```

**Remediation:**
```cobol
PERFORM UNTIL A > 100
   ADD 1 TO A
   ON SIZE ERROR 
      DISPLAY "SIZE ERROR DETECTED"
      PERFORM ERROR-HANDLER
   END-ADD
END-PERFORM
```

**Risk Assessment:**
- **Impact:** High - Buffer overflows can lead to data corruption or security vulnerabilities
- **Likelihood:** Medium - Depends on data volumes and loop iterations
- **Priority:** High - Should be addressed in security hardening

### Security Factors

| Factor | Status | Notes |
|--------|--------|-------|
| **Structural Security** | Issues Found | 5 objects with buffer overflow risk |
| **Input Validation** | Review Needed | Online transactions need validation review |
| **Authentication** | Implemented | USRSEC file with 113 interaction points |
| **Authorization** | Implemented | User security checks throughout |

### Code Quality Metrics

| Metric | Value | Assessment |
|--------|-------|------------|
| **Total Structural Flaws** | 1 pattern type | Manageable scope |
| **Affected Objects** | 5 out of 909 | 0.55% impact |
| **Security Categories** | 8 CWE mappings | Comprehensive coverage |

### Recommendations

1. **Immediate Actions:**
   - Review and add ON SIZE ERROR handling to arithmetic operations in loops
   - Conduct security audit of the 5 affected objects
   - Implement automated testing for boundary conditions

2. **Medium-term Actions:**
   - Establish coding standards requiring SIZE ERROR handling
   - Implement static code analysis in CI/CD pipeline
   - Add unit tests for edge cases in arithmetic operations

3. **Long-term Actions:**
   - Consider modernizing critical business logic to languages with built-in overflow protection
   - Implement comprehensive security testing framework
   - Regular security assessments and penetration testing

---

## Architectural Patterns

### Design Patterns Observed

#### 1. **Layered Architecture**
The application follows a strict layered architecture:
- **Presentation Layer:** BMS screens (17 maps)
- **Transaction Layer:** CICS transaction handlers (18 transactions)
- **Business Logic Layer:** COBOL programs (29 programs)
- **Data Access Layer:** VSAM file I/O operations
- **Persistence Layer:** VSAM datasets and GDGs

#### 2. **Separation of Concerns**
- **Online vs. Batch:** Clear separation between CICS online programs (CO prefix) and batch programs (CB prefix)
- **Data vs. Logic:** Data structures (copybooks) separated from program logic
- **UI vs. Business:** BMS maps separated from business logic programs

#### 3. **Menu-Driven Navigation**
- Hierarchical menu structure starting from main menu (CM00)
- Separate admin menu (CA00) for administrative functions
- Context-based navigation with transaction routing

#### 4. **CRUD Operations Pattern**
Consistent CRUD pattern across entities:
- **List:** View multiple records (e.g., CCLI for cards, CU00 for users)
- **View:** Display single record details (e.g., CCDL, CAVW)
- **Add:** Create new records (e.g., CU01, CT02)
- **Update:** Modify existing records (e.g., CCUP, CU02, CAUP)
- **Delete:** Remove records (e.g., CU03)

#### 5. **Batch Processing Pattern**
Standard batch job sequence:
1. **Close Files** (CLOSEFIL)
2. **Process Data** (POSTTRAN, INTCALC)
3. **Backup** (TRANBKP)
4. **Generate Reports** (CREASTMT, TRANREPT)
5. **Open Files** (OEPNFIL)

#### 6. **Error Handling**
- CEE3ABD for abnormal termination (18 usage points)
- Centralized error handling approach
- Transaction rollback capabilities

#### 7. **Security Pattern**
- Authentication at entry point (CC00 - Signon)
- Authorization checks throughout (USRSEC file with 113 interactions)
- Separate admin role and menu structure

#### 8. **Data Versioning**
- GDG (Generation Data Groups) for historical data management
- Backup and restore capabilities
- Audit trail through transaction logs

---

## Component Relationships

### Inter-Component Dependencies

#### Direct Dependencies

```
Transactional Services (18 objects)
    ├── depends on → Logic Services (176 objects)
    │                   └── depends on → Data File Services (84 objects)
    └── uses → Screen Interaction (17 objects)

Batch Services (40 objects)
    ├── depends on → Logic Services (176 objects)
    └── depends on → Data File Services (84 objects)

Logic Services (176 objects)
    ├── depends on → Data File Services (84 objects)
    ├── calls back to → Batch Services (40 objects)
    └── orchestrates → Transactional Services (18 objects)
```

#### Bidirectional Relationships

- **Logic Services ↔ Transactional Services:** Mutual dependencies for transaction processing
- **Logic Services ↔ Batch Services:** Batch jobs call business logic components
- **Logic Services ↔ Data File Services:** Continuous data access patterns
- **Data File Services → Logic Services:** File events trigger business logic

### Critical Integration Points

#### 1. **User Security Integration**
- **File:** AWS.M2.CARDDEMO.USRSEC.VSAM.KSDS
- **Interactions:** 113 (highest in application)
- **Connected to:** All user-facing transactions
- **Critical Path:** Authentication flows

#### 2. **Cross-Reference Integration**
- **Files:** CARDXREF.VSAM.KSDS + AIX + PATH
- **Interactions:** 125 total
- **Connected to:** Customer, Account, and Card modules
- **Critical Path:** All relationship queries

#### 3. **Transaction Processing Hub**
- **File:** TRANSACT.VSAM.KSDS
- **Interactions:** 71
- **Connected to:** Online transactions, batch posting, reporting
- **Critical Path:** All financial operations

### Data Flow Patterns

#### Online Transaction Flow

```
User Input (BMS Screen)
    ↓
CICS Transaction
    ↓
COBOL Online Program (CO*)
    ↓
VSAM Data Access
    ↓
BMS Screen Output
```

#### Batch Processing Flow

```
Scheduled Job (JCL)
    ↓
COBOL Batch Program (CB*)
    ↓
Sequential File Processing
    ↓
VSAM Update
    ↓
Report Generation (GDG)
```

### Key Dependencies Summary

| Component | Depends On | Dependency Count | Criticality |
|-----------|------------|------------------|-------------|
| Screen Interaction | Transactional Services | High | Medium |
| Transactional Services | Logic Services | High | High |
| Logic Services | Data File Services | Very High | Critical |
| Logic Services | Batch Services | Medium | Medium |
| Batch Services | Logic Services | High | High |
| Batch Services | Data File Services | High | Critical |

---

## Appendix: File Locations

### Source Code Structure

```
/app
├── /asm                    # Assembler programs
├── /bms                    # BMS screen maps (17 maps)
├── /cbl                    # COBOL programs (29 programs)
├── /cpy                    # COBOL copybooks
├── /cpy-bms                # BMS copybooks
├── /csd                    # CICS system definition
├── /jcl                    # JCL batch jobs (40+ jobs)
├── /proc                   # JCL procedures
├── /data                   # Sample data files
├── /maclib                 # Macro libraries
├── /ctl                    # Control files
├── /catlg                  # Catalog definitions
└── /scheduler              # Job scheduling scripts
```

### Optional Feature Modules

```
/app/app-authorization-ims-db2-mq    # Credit card authorization with IMS/DB2/MQ
/app/app-transaction-type-db2        # Transaction type management with DB2
/app/app-vsam-mq                     # Account extraction via MQ
```

---

## Document Information

**Report Generated By:** CAST Imaging MCP Tools  
**Analysis Date:** 2025-11-13  
**Application Snapshot:** Onboarding-202506170722  
**Delivery Date:** 2025-06-17T07:22:00  

**Imaging System:** CAST Imaging Demo v3  
**Analysis Depth:** Full application static code analysis  
**Coverage:** 100% of application components  

**Tools Used:**
- `imaging-mcp-applications` - Application discovery
- `imaging-mcp-stats` - Statistical analysis
- `imaging-mcp-architectural_graph` - Component architecture mapping
- `imaging-mcp-transactions` - Entry point analysis
- `imaging-mcp-data_graphs` - Data entity relationship analysis
- `imaging-mcp-objects` - Object inventory
- `imaging-mcp-packages` - Dependency analysis
- `imaging-mcp-quality_insights` - Quality and security assessment

---

## Glossary

**AIX** - Alternate Index: Secondary index for VSAM datasets allowing multi-key access  
**BMS** - Basic Mapping Support: CICS screen definition system  
**CICS** - Customer Information Control System: Transaction processing system  
**GDG** - Generation Data Group: Versioned dataset collection  
**JCL** - Job Control Language: Batch job scripting language  
**KSDS** - Key-Sequenced Data Set: VSAM indexed file organization  
**VSAM** - Virtual Storage Access Method: Mainframe file system  

---

**End of Architecture Discovery Report**
