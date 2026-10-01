# Source Data Design

## 1. Purpose

This document defines the source data model, source-system responsibilities,
schema standardization strategy, and reconciliation approach for the
Employee Recognition Data Platform.

The objective is to establish a consistent canonical data model before
source data is processed through the Azure Data Engineering platform.

---

## 2. Source Systems

The project currently contains source data maintained in Azure ADLS Gen2
and version-controlled datasets maintained in GitHub.

### Azure ADLS Gen2

Azure ADLS contains the runtime source data used by the data platform.

Current source domains include:

- Employees
- Recognitions
- Recognition Rules
- Redemptions
- Organization Changes
- Metadata

### GitHub

GitHub is used for:

- Source dataset version control
- Pipeline configuration
- Metadata configuration
- SQL
- Databricks code/notebooks
- Architecture documentation
- Data Engineering project documentation

GitHub datasets may be used to increase test/data volume, but they must
be standardized and reconciled before being introduced into the runtime
data platform.

---

## 3. Canonical Employee Model

The Azure employee schema is the canonical employee model for this project.

### Canonical Schema

| Column | Description |
|---|---|
| employee_id | Unique employee identifier |
| employee_name | Employee full name |
| department_id | Department identifier |
| department_name | Department name |
| manager_id | Employee's manager identifier |
| job_title | Employee job title |
| location | Employee work location |
| joining_date | Employee joining date |
| employment_status | Current employment status |
| effective_date | Effective date of the employee record |
| email | Optional employee email address |

The `email` attribute may be incorporated from GitHub where available.

---

## 4. GitHub-to-Canonical Schema Mapping

The GitHub employee dataset contains a similar employee structure but
uses different column names.

| GitHub Column | Canonical Column | Transformation |
|---|---|---|
| employee_id | employee_id | ID reconciliation required |
| employee_name | employee_name | Direct mapping |
| department | department_name | Rename |
| designation | job_title | Rename |
| manager_id | manager_id | ID reconciliation required |
| location | location | Direct mapping |
| joining_date | joining_date | Type standardization |
| status | employment_status | Rename |
| email | email | Direct mapping |
| — | department_id | Derive/reconcile |
| — | effective_date | Populate according to source strategy |

---

## 5. Employee ID Strategy

Employee IDs are treated as business keys.

The existing Azure source uses IDs such as:

E1001, E1002, E1003

The GitHub dataset uses a different identifier convention.

GitHub employee records must therefore NOT be directly appended to the
Azure employee source without reconciliation.

The integration process must:

1. Identify existing employee IDs.
2. Identify new employee records.
3. Detect duplicate employees.
4. Map manager relationships.
5. Map department relationships.
6. Validate referential integrity.
7. Generate or assign canonical employee IDs where required.
8. Preserve the canonical ID across downstream datasets.

---

## 6. Referential Integrity

Employee IDs are referenced by multiple source domains.

### Recognition

- giver_employee_id
- receiver_employee_id

### Redemptions

- employee_id

### Organization Changes

- employee_id
- old_manager_id
- new_manager_id

Therefore, an employee ID must remain consistent across all datasets.

Example:

Employee:

E1006

Recognition:

giver_employee_id = E1006

Redemption:

employee_id = E1006

All references must resolve to the same employee.

---

## 7. Source Domain Responsibilities

### Employees

Provides the current employee master/current-state attributes.

### Recognitions

Provides recognition events including:

- giver
- receiver
- category
- points
- event timestamp
- arrival timestamp

### Recognition Rules

Provides business rules used to validate recognition events.

### Redemptions

Provides reward redemption transactions and points consumed.

### Organization Changes

Provides organizational change events such as:

- department changes
- manager changes
- effective dates

This dataset will support CDC and SCD Type 2 processing.

### Metadata

Provides configuration used by the metadata-driven ingestion framework.

---

## 8. Data Reconciliation Strategy

GitHub data will not directly overwrite the existing Azure source.

The reconciliation process will be:

GitHub Dataset
    ↓
Schema Standardization
    ↓
ID Reconciliation
    ↓
Duplicate Detection
    ↓
Department/Manager Validation
    ↓
Referential Integrity Validation
    ↓
Canonical Employee Dataset

Only validated records will be introduced into the runtime data platform.

---

## 9. Data Quality Rules

The employee dataset should satisfy the following checks:

- employee_id must not be null
- employee_id must be unique
- employee_name must not be null
- department_id must exist
- manager_id must resolve where applicable
- joining_date must be valid
- employment_status must contain an allowed value
- location should be populated
- duplicate employees must be identified
- employee relationships must remain consistent

Invalid records should be routed to a quarantine process rather than
silently discarded.

---

## 10. Architectural Decision

The project will use the Azure employee schema as the canonical model.

GitHub provides version-controlled data and engineering artifacts.
ADLS provides the runtime data platform.

The project will demonstrate controlled source integration rather than
direct file replacement.

This approach supports data quality, lineage, reproducibility,
referential integrity, and enterprise-grade data engineering practices.
