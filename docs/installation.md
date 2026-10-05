---
title: Install FiservCCM
description: How to install the FiservCCM connector on an on-prem OpCon system or SMA Relay installation.
tags: [type/procedural, role/system-administrator, feature/fiservCCM-acs]
sidebar_label: 'Installation'
---

# FiservCCM Installation

## Requirements

- OpCon Cloud or OpCon version 26.0.x or greater.
- The Microsoft SQLCMD utility installed on the server that runs SMANetCom (on-premises) or the relay (OpCon Cloud). The connector starts `SqlCmd.exe` by name, so it must be on the path of that service.
- Insert the CCM_ScheduleTaskV3.sql stored procedure into the Fiserv CCM database.

## Installation

Download the FiservCCM software from the SMA FTP Site.
The software is in
**/OpCon Releases/Integrations/FiservCCM/** 
Select the required version.

- Unzip the ACSFiservCCM.zip file.
- On-prem customers 
  Copy the ACSFiservCCM directory to the \\SAM\\plugins directory
- Cloud customers
  Copy the ACSFiservCCM directory to the \\Relay\\plugins directory

## Stored Procedure
The required stored procedure can be found in the **StoredProcedure** directory of the software distribution.
