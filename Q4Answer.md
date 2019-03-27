# Data file not processed Postmortem (AESEDI-53447)

## Date

2019-03-26

## Authors

* kikohernandez92

## Status

Completed and solved

## Summary

According to the customer, the data was not sent; however, the investigation shows the file was sent but not processed by the AES CIS Service due to another issue (Jira Issue: 
AESCIS-38263).

## Impact

486,000 records in total were affected.

## Root Causes

AES CIS service crashed while trying to process the file and run a script at the same time, which ended in a lock of resources.

## Trigger

The attempt to process the records' file while running other scripts

## Resolution

Reloaded the AES CIS monitoring service, discovered the missing records not being processed and resent the file.

## Detection

Customer detected the failure and alerted thorugh JIRA (Issue: AESEDI-53447)

## Action Items

| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| Design and apply a manual monitoring policy | mitigate | kikohernandez92 | n/a **DONE** |
| Improve and better monitoring process to detect issues with AES CIS service | prevent | kikohernandez92 | Jira Issue: AESCIS-38263  **TODO** |

## Lessons Learned

### What went well

* Resending the file updated the records promptly and correctly

### What went wrong

* The AES CIS monitoring service shouldn't lock when processing customer data files.

### Where we got lucky

* Normally reloading the AES CIS allowed to see the missing records.

## Timeline

2019-03-26 (*all times UTC*)

| Time  | Description |
| ----- | ----------- |
| 11:56 | Customer detects missing records from his data and creates issue |
| 12:00 | **Investigation Begins** Issue noted and responded |
| 12:04 | File is sent correctly, according to AES EDI logs |
| 12:10 | Reloading AES CIS service and log analysis returned failure to process the data |
| 12:20 | **Investigation ends** |
| 12:37 | Resending records' file |
| 13:00 | Records correctly processed |

