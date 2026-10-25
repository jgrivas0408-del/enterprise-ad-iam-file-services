# Recovered lab commands and troubleshooting notes

These excerpts were recovered from the original September 2026 walkthrough. They are instructions, not a recovered standalone script or a fresh execution transcript. Expected outputs are not execution evidence. See the [README screenshot gallery](../README.md#selected-original-evidence) for eight original screenshots uploaded separately.

## Inspect the departmental SMB share

On FILE01:

```powershell
Get-SmbShare -Name 'Departments$' |
Select-Object Name,Path,FolderEnumerationMode
```

The intended final FolderEnumerationMode is AccessBased. Verify actual output.

## Create a harmless access-test file

From an elevated Command Prompt on FILE01:

```cmd
echo Security department test file > "D:\Shares\Security\Security_Audit_Test.txt"
```

This writes or overwrites a file. Use only disposable test data in the isolated lab.

## Test a departmental access boundary

On CLIENT01 as the lab test user JGR\dbrooks:

```cmd
type "\\FILE01\Departments$\Security\Security_Audit_Test.txt"
```

The intended result is denied access. The walkthrough encountered path-not-found while access-based enumeration was enabled. That response alone does not establish a particular ACL or audit configuration.

## Inspect matching SMB access-check events

On FILE01 with appropriate Security-log privileges:

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security';Id=5145} -MaxEvents 50 |
Where-Object {$_.Message -match 'dbrooks' -and $_.Message -match 'Security_Audit_Test'} |
Select-Object -First 1 -ExpandProperty Message
```

The query only searches the most recent 50 matching event IDs. Empty output does not establish that no event exists. Audit policy and the text filter affect results.

## Troubleshooting context

The walkthrough considered cached SMB sessions, distinguished share-root and file-level access checks, and discussed temporary enumeration changes for a controlled audit test. The intended final setting remained access-based enumeration. Closing instructions called for VMware snapshots named Enterprise-Lab-Completed; those instructions do not prove snapshot creation.

## Evidence status

Eight original user-supplied screenshots are now included in the README gallery. They cover password resets, lockout, policy checks, server administrator membership, departmental folders and a denied access attempt. Original screenshots of FSRM enforcement, detailed audit events, share encryption, ACLs and quota settings are not included in the selected gallery. No standalone original script or configuration export has been recovered.
