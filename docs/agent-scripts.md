---
sidebar_label: 'Scripts'
title: Define FiservCCM scripts
description: "Instructions for creating the error checking scripts required by the FiservCCM connector in the OpCon script library."
tags:
  - Procedural
  - System Administrator
  - Automation Engineer
---

# Define FiservCCM Scripts

**Theme:** Configure | **Audience:** System Administrator, Automation Engineer

## What is it?

The FiservCCM implementation uses a script to provide the error checking for each task run. This script is requested during the agent definition and the contents of the script are passed during task startup to enable the creation of a unique file for each task.

## Script Contents
The script is used to define non-critical error messages that can change the result of the task run from **Failed** to **Finished OK**. 
The objective is to prevent workflows from being stopped due to configured non-critical error conditions.

```
ERROR=InvalidAccountStatus;RESULT=OK;TASKID=12,16,18
```
where
- **ERROR**  indicates the error to check for. This value is found in the Value field of the error message (i.e. `<Message><DictionaryContents><Item><Key>ResponseCode</Key><Value>InvalidAccountStatus</Value></Item></DictionaryContents></Message>` )
- **RESULT** is the end result if the error matches. OK means the job completion status is changed from **Failed** to **Finished OK**.
- **TASKID** indicates which FiservCCM tasks are affected by this. When TASKID= contains no values, then all tasks that contain the error are changed to a **Finished OK** status. If TASKID=n,n,n contains values, then only those defined task ids are changed to a **Finished OK** status.  

### Rule format

- Enter one rule per line, with no blank lines. A blank line stops error checking, and the job stays **Failed**.
- Every rule needs `ERROR=`, `RESULT=` and `TASKID=`. `TASKID=` can be left empty, but it must be present.
- Each ERROR value can appear in only one rule.
- Only `RESULT=OK` changes the outcome.
- The ERROR value is matched, case-sensitively, anywhere in the message of a step history entry with Error severity.
- TASKID values are compared with the CCM task number reported in the stored procedure's output.
- Error checking runs only when the job has failed. When a rule matches, the job finishes with exit code 0.

## Define scripts

To define FiservCCM scripts, complete the following steps:

1.  Open Solution Manager.
2.  Select **Library**.
3.  Select **Scripts**.
4.  Select **Script Types** from the upper right-hand corner.
    1.  Select **+Add**.
    2.  In the **Name** field enter **Fiserv CCM**.
    3.  In the **File Extension** field enter **txt**.
    4.  In the **Description** field enter **Used for FiservCCM Integration**.
    5.  Select **Save**.
5.  Select **Script Runners** from the upper right-hand corner.
    1.  Select **+Add**.
    2.  In the **Name** field enter **Fiserv CCM**.
    3.  In the **OS** field select **Fiserv CCM** from the list.
    4.  In the **Type** field select **Fiserv CCM** from the list.
    5.  In the **Command** field enter **cmd.exe /c**.
    6.  Select **Save**.
6.  Select **Scripts** from the upper right-hand corner, and create the Error Checking script:
    1.  Select **+Add**.
    2.  In the **Name** field enter a name for the script. It is suggested using the proposed agent name and append **error-checking** to the name.
    3.  In the **Type** field select **Fiserv CCM** from the list.
    4.  Assign the required roles.
    5.  In the **Script** field paste the  error checking contents.
    6.  Select **Save**.
