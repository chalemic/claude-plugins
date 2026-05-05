---
name: deploy-to-salesforce
description: Deploy source files like Apex, triggers, and Lightning Web Components (LWC) to the default Salesforce org. Use during Salesforce development to get the code to the server so it can be tested.
---

# Deploy to Salesforce

Deploy recently modified Apex classes, triggers, and Lightning Web Components (LWC).

## Steps

### Step 1: Identify the files to deploy

If invoked from `/write-apex` or `/write-lwc`, the files are already known from conversation context — use those.

If invoked standalone, rely on the current conversation context to determine which files are in scope.

Determine the metadata type from the file's folder:
- `classes/` → `ApexClass:<ClassName>`
- `triggers/` → `ApexTrigger:<TriggerName>`
- `lwc/<componentName>/` → `LightningComponentBundle:<componentName>` — the component name is the **folder name**, not the individual file name

### Step 2: Check for a default org

Run `sf config get target-org --json` to check for a default org.

- If one is set, proceed without a `--target-org` flag.
- If none is set, run `sf org list --json` to list available orgs. Present them to the user and ask which org to target. Use `--target-org <SelectedOrg>` in all subsequent deploy commands.

### Step 3: Deploy the files

Verify that a `DeploymentResults/` folder exists in the current working directory. If it does not, create it:

```
mkdir DeploymentResults
```

Generate a timestamp string in the format `YYYYMMDD_HHmmss` and use it as the output filename. Then run the deploy command, writing output into the `DeploymentResults/` folder:

```
sf project deploy start --metadata 'ApexClass:AccountHelper' --json > DeploymentResults/deploymentResults_20260330_142559.json
sf project deploy start --metadata 'ApexClass:AccountHelper' --metadata 'ApexClass:CustomSort' --json > DeploymentResults/deploymentResults_20260330_142559.json
sf project deploy start --metadata 'ApexTrigger:LeadTrigger' --json > DeploymentResults/deploymentResults_20260330_142559.json
sf project deploy start --metadata 'LightningComponentBundle:cssLibrary' --json > DeploymentResults/deploymentResults_20260330_142559.json
sf project deploy start --metadata 'ApexClass:AccountHelper' --target-org myOrg --json > DeploymentResults/deploymentResults_20260330_142559.json
```

### Step 4: Review results and retry on failure

Use the **Read tool** to read the JSON output file — do not use shell commands (python3, jq, cat, etc.) to parse or summarize it, as these require extra permissions. Read the file and report the key fields directly: `result.status`, `result.success`, `numberComponentsDeployed`, `numberComponentsTotal`, and `deployUrl`.

**On success:** Report which components were deployed and surface `result.deployUrl` as a link for quick access in Salesforce Setup.

**On failure:** Read `result.details.componentFailures[]` for error details — each entry includes `fileName`, `lineNumber`, `columnNumber`, and `problem`. Fix the issues in the source files, then re-run the deploy (return to Step 3).

Retry for a maximum of **3 deployment attempts** total. If the deploy is still failing after 3 attempts, stop, present all errors clearly, and ask the user for next steps.

Full examples of success and failure JSON output can be found in [SuccessfulExample.md](SuccessfulExample.md) and [FailedExample.md](FailedExample.md).
