# Recovered lab commands and troubleshooting notes

These excerpts were recovered from the original September 2026 lab conversations. They are instructional commands from the lab walkthrough, not a recovered standalone script or a fresh execution transcript. Expected outputs below are not evidence that a command was run successfully.

## Inspect the departmental SMB share

Run on FILE01:

```powershell
Get-SmbShare -Name 'Departments$' |
Select-Object Name,Path,FolderEnumerationMode
```

The intended final configuration is `FolderEnumerationMode : AccessBased`. Verify the actual output before drawing conclusions.

## Create a harmless access-test file

The walkthrough instructed creating this file on FILE01 from an elevated Command Prompt:

```cmd
echo Security department test file > "D:\Shares\Security\Security_Audit_Test.txt"
```

This writes a test file and overwrites a file of the same name. Use only the isolated lab and ensure the path contains disposable test data.

## Test a departmental access boundary

On CLIENT01, while signed in as the lab test user `JGR\dbrooks`:

```cmd
type "\\FILE01\Departments$\Security\Security_Audit_Test.txt"
```

The intended result is denied access for an unauthorized user. The lab encountered a path-not-found response while access-based enumeration was enabled. That response alone does not prove that a particular NTFS ACL or audit configuration is correct.

## Inspect matching SMB access-check events

The walkthrough supplied this PowerShell query for FILE01:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security';Id=5145} -MaxEvents 50 |
Where-Object {$_.Message -match 'dbrooks' -and $_.Message -match 'Security_Audit_Test'} |
Select-Object -First 1 -ExpandProperty Message
```

The query searches the most recent 50 matching event IDs. No output does not prove that no event exists: it may be outside that window or may not match the text filter. Reading the Security log requires appropriate privileges. Event availability depends on the audit policy.

## Troubleshooting recorded in the walkthrough

- Cached SMB connections were considered while testing enumeration behavior.
- The walkthrough distinguished a share-root access check from a file-level check containing `Security\Security_Audit_Test.txt`.
- Temporary changes to enumeration were discussed for a controlled audit test; the intended final setting remained access-based enumeration.
- The closing instructions called for VMware snapshots of DC01, CLIENT01 and FILE01 named `Enterprise-Lab-Completed`. These instructions do not independently prove snapshot creation.

## Evidence status

The shared conversations expose the command text, but their original screenshot attachments display as image placeholders in the retrieved public view. Original images have not been imported into this repository. These notes do not substitute for screenshot evidence, effective policy exports, or actual command output.
