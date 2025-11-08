let MDEProcess = dynamic(["MsSense.exe","MpDefenderCoreService.exe","MsMpEng.exe"]);
let SuspendPID =
DeviceProcessEvents
| where TimeGenerated > ago(1d)
| where FileName has "WerFaultSecure"
| summarize arg_max(TimeGenerated, *) by DeviceId
| extend PID=tostring(extract(@"-p\s+(\d+)", 1, ProcessCommandLine))
| project PID;
DeviceProcessEvents
| where TimeGenerated > ago(30d)
| where tostring(ProcessId) has_any(SuspendPID)
| where FileName has_any(MDEProcess)
