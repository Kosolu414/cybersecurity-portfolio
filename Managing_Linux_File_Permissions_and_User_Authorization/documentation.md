# Managing Linux File Permissions & User Authorization

* **Scenario:** As a security professional working with an organization's research team, the system's current file and directory permissions did not align with the strict authorization requirements needed to keep sensitive data secure. The goal was to audit the existing file system permissions, identify misconfigurations, and modify them to ensure proper access control.

### Step by Step Implementation

* **Phase 1:** Auditing the File SystemAction: Navigated to the targeted directory (e.g., /home/researcher2/projects) and ran the ls -la command to expose all files, subdirectories, and hidden files (like .project_x.txt).  
**Analysis:** Analyzed the 10-character string (e.g., -rw-rw-r--) to determine the exact read ($r$), write ($w$), and execute ($x$) rights allocated to the User, Group, and Other.

* **Phase 2:** Remediating Unauthorized Access
**Action:** Identified files where unauthorized users or broad "other" groups had write or execute access.  
**Correction:** Utilized the chmod command to restrict permissions. For example, explicitly removing write or execute access from others or groups (chmod o-w filename or chmod g-x directory_name) to match corporate compliance.

* **Phase 3:** Verification.  
**Action:** Re-ran ls -la to confirm that the permissions string correctly updated and that the system achieved the desired secure state.

### 📈 Key Outcomes & Security Impact

* **Principle of Least Privilege:** Successfully restricted sensitive files so only authorized researchers can modify them.
* **System Hardening:** Mitigated risks of internal unauthorized data manipulation or malicious script execution by revoking unnecessary execute ($x$) rights on files and directories.
* **Compliance:** Realigned the directory structures with organizational security policies.

* **[👉 View File permissions Report](./File_permissions_in_Linux.pdf)*** 
