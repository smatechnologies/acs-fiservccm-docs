---
title: Define a FiservCCM job task
sidebar_label: Task definition
description: "Define a Fiserv CCM task in OpCon to submit a request to run the stored procedure in the Fiserv CCM database."
tags:
  - Procedural
  - Automation Engineer
  - Jobs
  - Agents
---

# Define a Fiserv CCM job task

**Theme:** Configure  
**Who Is It For?** Automation Engineer

## What is it?

A FiservCCM task submits a SQL request to the Fiserv CCM database to run the **CCM_ScheduleTaskV3** stored procedure.
The stored procedure is submitted using the Microsoft **SQLCMD.exe** utility. The started process is monitored for completion.

If the request completes successfully, the selected Step History logs are retrieved and appended to the OpCon job log.

If the request fails, the selected Step History logs plus the **Error** logs are retrieved and appended to the OpCon job log.
The error log is checked to determine if the error is a non-critical error defined in the error checking script. If it is, the
action defined in the error checking script is taken.

If no Step History logs are selected and the task fails, the error logs are appended to the OpCon job log.

- Use this procedure when you need to schedule a Fiserv CCM task through OpCon


The Fiserv CCM Connector supports the following task type:

| Task type | Description |
|---|---|
| Execute | Runs a SQL statement against the defined Microsoft SQL Server database |

## Define a Job task

**Prerequisite:** The Fiserv CCM agent must be defined and communicating before a job task can be submitted. See [Agent definition](./agent-definition.md).

To define a Fiserv CCM task, complete the following steps:

1. In Solution Manager, select **Library**.
2. From the **Administration** menu, select **Master Jobs**.
3. Select **+Add**.
4. In the **Schedule** field, select the schedule name from the list.
5. In the **Name** field, enter a unique name for the job within the schedule.
6. In the **Job Type** field, select **Fiserv CCM** from the list.
7. In the **Task Type** field, select **Execute** from the list.
8. Select the **Task Details** button.
9. In the **Integration Selection** section, select the agent previously defined.
10. In the **Task Configuration** section, complete the following fields:

    | Field | Description |
    |---|---|
    | **ServerName\\Instance** | (Required) The name of the SQL Server, and the instance if required |
    | **Database Name** | (Required) The name of the database |
    | **SQL Statement** | The SQL statement to run (value `EXEC CCM_ScheduleTaskV3 nn`, where `nn` is the number of the CCM task to run) |
    | **Authentication** | The connector signs in with SQL Server authentication, using the batch user selected under **User** |
    | **User** > **Batch User** | Select a Fiserv CCM batch user from the list. The connector signs in to SQL Server with this user's name and password, so a batch user is required. See [Batch Users](./task-batch-users.md) |
    | **Step History Log Types to Retrieve** | Select the log types to retrieve: **Info**, **Warning**, **Error** and **Verbose**. Error entries are always retrieved, and are included in the job log when the job fails even if **Error** is not selected |
    | **Failure Criteria** | Set the **Exit Codes** criteria that decide whether the job fails. See [Failure criteria](#failure-criteria) |

11. Select the **Save** button. The job is added to the schedule.

## Failure criteria

The **Exit Codes** criteria are checked against the exit code of SQLCMD. By default, the job fails when the exit code is not 0. SQLCMD runs with the `-b` option, so a SQL error ends it with a non-zero exit code.

Error checking runs only when the job has failed under these criteria. If a rule in the error checking script matches, the job finishes with exit code 0 and a status of **Finished OK**. See [Scripts](./agent-scripts.md).

## Job log

The job log for each run contains:

- The server, database, user and SQL statement, and which Step History log types were selected
- The output of SQLCMD
- The retrieved Step History entries, each with its Step History ID, log date, severity and message
- When the job failed, the result of error checking, including the rule that matched or a note that no rule matched

## FAQs

**Can I use OpCon global properties in task fields?**  
Yes. Global properties using the `[[property_name]]` token syntax are supported in all task configuration fields.

## Glossary

