---
title: FiservCCM release notes
description: Version history and change details for FiservCCM, including new features and improvements.
tags:
  - type/reference
  - role/automation-engineer
  - role/system-administrator
  - feature/fiservCCM-acs
sidebar_label: 'Release notes'
---

# FiservCCM Connector Release Notes

This page lists changes for each FiservCCM Connector release, organized by version. 

## 26

### 0.0

June 2026

#### What's new

:eight_spoked_asterisk: **CON-5**: Initial Release of FiservCCM intehration.

#### Why this matters

Provides additional capabilities specific to CCM integration not provided by using the generic SQL Agent.
- includes a mechanism to determine if an error condition can be changed to **Finished OK** to prevent workflow stoppage for non-critical errors.
- returns the Step History information if selected (Info, Warning, Error or Verbose) in the job log.
- if an error condition occurs will always include the error information in the job log. 

#### Fixes

