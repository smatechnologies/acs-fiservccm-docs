---
title: Define a FiservCCM job task
sidebar_label: Task definition
description: "Define a Fiser CCM task in OpCon to submit a request to execute the stored procedure in the Fiserv CCM database."
tags:
  - Procedural
  - Automation Engineer
  - Jobs
  - Agents
---

# Define a Kubernetes job task

**Theme:** Configure  
**Who Is It For?** Automation Engineer

## What is it?

A FiservCCM task submits a SQL request to the Fiserv CCM database to execute the **CCM_ScheduleTaskV3** stored procedure.
The stored procedure is submitted using the Microsoft **SQLCMD.exe** utility. The started process is monitored for completion.

If the request completes successfully, the selected Step History logs will be retrieved and appended to the OpCon job log.

If the request fails, the selected Step History logs plus the **Error** logs will be retrieved and appended to the OpCon job log.
The error log will be checked to determine if the error is a non-critical error defined in the error checking script. If it is the
action defined in the erro checking script will be taken.

If no Step History logs are selected and the task fails, the error logs will be appended to the OpCon job log.

- Use this procedure when you need to schedule a Fiserv CCM task through OpCon


The Fiserv CCM Connector supports the following task type:

| Task type | Description |
|---|---|
| Execute | executes a SQL statement against the defined MS SQL Database |

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
9. In the **Integration Selection** section, select the Kubernetes agent previously defined.
10. In the **Task Configuration** section, complete the following fields:

    | Field | Description |
    |---|---|
    | **ServeName\\Instance** | The name of the database server and instance if required |
    | **Database Name** | The name of the database |
    | **SQL Statement** | The SQL Statement to submit for execution |
    | **Authentication** | select a database user|
    | **Batch User** | Select a Fiserv CCM batch user from the drop-down list (user must have database privileges) |
    | **Step History** | Select which log types to retrieve. Note that Error log type is always retrieved and displayed if the task failed even if it is not selected |
    | **Failure Criteria** | Set the failure criteria for the taks |
 

11. Select the **Save** button. The job is added to the schedule.

## FAQs

**Can I use OpCon global properties in task fields?**  
Yes. Global properties using the `[[property_name]]` token syntax are supported in all task configuration fields.

## Glossary

