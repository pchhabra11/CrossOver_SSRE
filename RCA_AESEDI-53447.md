# PostMortem/Root Cause Analysis for AES EDI | JIRA Issue ( AESEDI-53447) 

## Date
2019-06-07

## Authors
*Pulkit Chhabra*

*Operations Team*

## Status
Complete, resolved

## Summary
The customer data was not sent from AES EDI. The investigation showed that the file with the data was sent however, it did not get processed due to an issue with the AES CIS service.

## Impact
About 486,000 records were affected and the EDI to CIS monitoring service too.

## Root Causes
Sending files with a large number of records while simultaneously running the patching script caused a wreck in the data processing. This issue with AES CIS service futher escalated to data not getting processed leading to missing records.

## Trigger
A large amount of files were not processed.

## Resolution
Reloading the *AES CIS* monitoring service allowed us to spot the missed records that were not discovered automatically. Following this the data file was resent leading to the resolution.

## Detection
Customer created a Jira Ticket to alert us on this failure. *Please refer JIRA Issue: (AESEDI-53447)*


## Action Items
| Action Item | Type | Owner | Bug |
| ----------- | ---- | ----- | --- |
| Writing of monitoring policy to detect records missings | prevent | Pulkit Chhabra | **DONE** |
| Monitor the data ingesters and processors (ETL) | prevent | Pulkit Chhabra | (Jira Issue No: AESCIS-38263)**TODO** |

## Lessons Learned
1. More monitoring plugins and modules to watch this critical part of our infrastructure. 
2. Slack notifications have to be added for alerting the team whenever a data discrepancy is detected in future so that such occurences are prevented in future.
3. Patching opearations should not be executed while data processing is in progress at AES EDI.

## Timeline

2019-06-07 (*all times UTC*)

| Time  | Description |
| ----- | ----------- |
| 11:56 | Discovering of the missing files |
| 12:00 | Restarting of the AES CIS monitoring module |
| 12:15 | Starting of the data processing of the records files |
| 13:00 | Completion of the data processing of all the 486,000 records files |
