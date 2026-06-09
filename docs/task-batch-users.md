---
sidebar_label: 'Batch Users'
title: Define FiserCCM batch users
description: "Instructions for creating the OpCon batch users required by the FiservCCM connector for SQL Server authentication."
tags:
  - Procedural
  - System Administrator
---

# Define FiservCCM Batch Users

**Theme:** Configure | **Audience:** System Administrator

## What is it?

The FiservCCM integration requires OpCon batch users to supply credentials for the Fiserv CCM SQL Server database. These users are created once and then selected by name when configuring a task.

The following batch users are required:
- The SQL Server User.

## Define a batch user

![Defining a Batch User](../static/img/task-batch-user.png)

To define FiservCCM batch users, complete the following steps:

1.  Open Solution Manager.
2.  From the Home page select **Library**.
3.  From the **Security** menu select **Batch Users**.
4.  Select **+Add** to add a new Batch User.
5.  Select **Fiserv CCM** from the **Select the target OS** list.
6.  Enter the User name that will be used to create the token in the **Identifier** field.
7.  Enter the password of the defined API User in the **Password** and **Confirm** fields.
8.  Select **Save**.

Repeat for each required batch user.