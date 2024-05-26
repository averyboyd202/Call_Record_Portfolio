📞

# Call Data Management in Snowflake

This repository contains a Snowflake SQL script designed to manage call data. The script includes creating a table, inserting sample data, and querying the data based on specific criteria. Below is a detailed explanation of each part of the script.

## Table Creation

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

## Sample Data Insertion

The second part of the script inserts sample data into the `call_data` table. This section demonstrates how to populate the table with initial data for testing and verification purposes.

Example of inserted data:
```sql
INSERT INTO call_data (call_date, call_type, software_version, caller_employee_id, agent_id, resolved, escalated_to_tier2, repeat_caller, category, subcategory, caller_notes, servicenow_incident_record)
VALUES 
    ('2024-05-26 09:15:00', 'Technical', '1.0.0', 'E12345', 'A67890', TRUE, FALSE, FALSE, 'Software', 'Installation', 'Caller reported installation issues', 'INC000001'),
    ('2024-05-26 10:30:00', 'Support', '1.2.3', 'E54321', 'A09876', FALSE, TRUE, TRUE, 'Hardware', 'Replacement', 'Caller requested hardware replacement', 'INC000002');
