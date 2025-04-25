# 📦 Project Requirements Document
This document includes requirements and project structure for collaboration and automation with Cursor.AI, as well as the definition of a GitHub Actions-based release workflow.

## 1. Project Structure
- **First-level directories** under the root directory each constitute a `sub-project`.
    ```
    .
    ├── .github/
    │   └── workflows/tag-and-release.yml  # Github Actions Workflow
    ├── A/
    │   ├── dir1/
    │   │   ├── file1.ttl       => Release Artifact: A_dir1_file1.ttl
    │   │   └── file1.dlog      => Release Artifact: A_dir1_file1.dlog
    │   └── file2.ttl           => Release Artifact: A_file2.ttl
    └── B/
    └── file3.ttl           => Release Artifact: B_file3.ttl
    ```

## 2. Sub-project File Rules
- Each sub-project can include **zero or more** of the following files:
  - `.ttl`: Turtle format RDF ontology
  - `.dlog`: Datalog format logic programming schema
- These files can be located in **any subdirectory** within the sub-project.

## 3. GitHub Action: Automatic Tagging and Release
### 🔁 Trigger Conditions
- Workflow executes when **PR is merged into main branch**

### 🧠 Variable Definitions
| Variable      | Description                                                       |
|---------------|-------------------------------------------------------------------|
| `SUB_PROJECT` | First-level folder name where changed files are located           |
| `TODAY`       | Current date (yyyyMMdd)                                           |
| `REVISION`    | Number of existing tags with `v{SUB_PROJECT}-{TODAY}-` prefix + 1 |

### 🏷 Tag Creation
- Format: `v{SUB_PROJECT}-{TODAY}-{REVISION}`
- Example: `vA-20250425-1`

### 🚀 Release Creation
- **Release Artifact**:
  - Zip and upload all `.ttl` and `.dlog` files within the `SUB_PROJECT`
- **Release Description**:
  - Display files in a table format with the following columns:
    - Sub-project: Name of the sub-project
    - Path: Relative path from sub-project root
    - Filename: Name of the file
    - Size: File size in bytes
    - Changed: Indicates if the file was changed in this PR (✅ for changed, ❌ for unchanged)
  - If no ontology files in folder:
    - `"No ontology files found in [SUB_PROJECT]"`

### 🛡 Required GitHub Permissions
    ```yaml
    permissions:
    contents: write         # Create tags/releases
    pull-requests: write    # Access PR information
    ```

## 4. Release Description Example
Ontology Release: vA-20250420-1
Date: 20250420
Revision: 1

Ontology Files:
| Sub-project | Path  | Filename  | Size (bytes) | Changed |
|-------------|-------|-----------|--------------|---------|
| A           | dir1  | file1.ttl | 1024         | ❌      |
| A           | dir1  | file1.dlog| 2048         | ✅      |
| A           | .     | file2.ttl | 512          | ❌      |

Note: Files marked with ✅ were changed in this PR.

## 5. Important Notes
1. `.ttl` and `.dlog` files should be included in the zip archive while maintaining folder structure
2. If no files are found, output message: "No ontology files found in [SUB_PROJECT]"
3. Maintain consistency in all tag and release naming conventions
