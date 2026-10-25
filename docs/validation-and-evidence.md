# Validation and evidence

This is an evidence capture plan for revisiting the completed lab. Expected results below are acceptance criteria, not new test results. No commands were run against the VMs while preparing this repository.

| Area | Check to capture | Expected result |
| --- | --- | --- |
| Domain membership | Sign in to CLIENT01 with a test domain user | Domain authentication succeeds |
| DNS | Query the lab domain and controller from CLIENT01 | Intended records resolve through lab DNS |
| Delegation | Reset a test password with the Help Desk account | Task succeeds in the delegated OU |
| Delegation boundary | Attempt an administrative task outside delegated scope | Access is denied |
| Account recovery | Unlock a test account and verify sign-in | Authentication succeeds after unlock |
| Group Policy | Capture effective policy output | Intended policies apply |
| Share authorization | Access a departmental folder with an authorized test user | Intended access is granted |
| Access boundary | Repeat with a user outside the authorized group | Access is denied |
| Access-based enumeration | Browse with users from different departments | Only authorized folders are visible |
| SMB encryption | Inspect share configuration and negotiated connection | Intended transport protection is active |
| Quota | Exercise the configured 3 GB quota using disposable data | Enforcement matches quota type and limit |
| File screening | Save a harmless empty file with a screened extension | Active screening blocks the configured file type |
| Logging | Capture an event following a controlled test | Event can be tied to the action |

## Evidence to add

- OU and group structure, including administrative separation.
- Delegated permissions and an example delegated task.
- Effective GPO output.
- SMB configuration, NTFS ACLs, FSRM quota and screening settings.
- Paired allowed and denied access checks with captions.

Use evidence from the original lab. Remove passwords, recovery codes, license keys, personal details and unrelated host information before publishing. Keep VM disks, snapshots, backups and user data out of GitHub.

For each item, record the test role, action, expected result, actual result, date and limitations. Document unexpected results and fixes honestly.
