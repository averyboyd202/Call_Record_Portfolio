📞

# Call Data Management in Snowflake

This repository contains a Snowflake SQL script designed to manage call data. The script includes creating tables, inserting sample data, and querying the data based on specific criteria. Below is a detailed explanation of each part of the script.

## Table Creation

### Call Data Table

The first part of the script creates a table named `call_data` with the following columns:

- `call_date`: Date and time of the call
- `call_type`: Type of the call (e.g., Technical, Support)
- `software_version`: Software version used during the call
- `caller_employee_id`: ID of the caller (employee)
- `agent_id`: ID of the agent handling the call
- `resolved`: Call resolved status (TRUE if resolved, FALSE if not)
- `escalated_to_tier2`: Whether the call was escalated to Tier 2 support (TRUE/FALSE)
- `repeat_caller`: Whether the caller is a repeat caller (TRUE/FALSE)
- `category`: Category of the call (e.g., Software, Hardware)
- `subcategory`: Subcategory of the call (e.g., Installation, Replacement)
- `caller_notes`: Notes taken during the call
- `servicenow_incident_record`: ServiceNow incident record associated with the call

### Caller Information Table

The script also creates a table named `caller_info` to store additional information about callers:

- `caller_employee_id`: ID of the caller (employee)
- `alphanumeric_employee_id`: Alphanumeric ID of the caller
- `department`: Department of the caller
- `job_code`: Job code of the caller
- `active_status`: Active or inactive status of the caller (TRUE/FALSE)
- `l1_manager`: L1 manager
- `l2_manager`: L2 manager
- `l3_manager`: L3 manager
- `l4_manager`: L4 manager
- `l5_manager`: L5 manager
- `executive_representative`: Executive representative
- `l1_manager_email`: L1 manager email
- `l2_manager_email`: L2 manager email
- `employee_email`: Employee email
- `tenure`: Tenure of the employee
- `salary`: Salary of the employee

## Sample Data Insertion

The script inserts sample data into both tables. This section demonstrates how to populate the tables with initial data for testing and verification purposes.

## Data Selection

The final part of the script retrieves data from the `call_data` table and joins it with the `caller_info` table to include additional caller details. The query is designed to select call records from May 2024 that are resolved and were not escalated to Tier 2 support.

Example of the query:
```sql
SELECT 
    cd.call_date, 
    cd.call_type, 
    cd.software_version, 
    cd.caller_employee_id, 
    cd.agent_id, 
    cd.resolved, 
    cd.escalated_to_tier2, 
    cd.repeat_caller, 
    cd.category, 
    cd.subcategory, 
    cd.caller_notes, 
    cd.servicenow_incident_record,
    ci.alphanumeric_employee_id, 
    ci.department, 
    ci.job_code, 
    ci.active_status, 
    ci.l1_manager, 
    ci.l2_manager, 
    ci.l3_manager, 
    ci.l4_manager, 
    ci.l5_manager, 
    ci.executive_representative, 
    ci.l1_manager_email, 
    ci.l2_manager_email, 
    ci.employee_email, 
    ci.tenure, 
    ci.salary
FROM 
    call_data cd
LEFT JOIN 
    caller_info ci
ON 
    cd.caller_employee_id = ci.caller_employee_id
WHERE 
    cd.call_date BETWEEN '2024-05-01' AND '2024-05-31'
    AND cd.resolved = TRUE
    AND cd.escalated_to_tier2 = FALSE;
