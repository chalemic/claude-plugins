# Salesforce Development Plugin for Claude Code

This plugin bundles six skills that automate the Salesforce development workflow inside Claude Code — covering Apex and LWC authoring, static code analysis, deployment, and test execution. Skills activate automatically based on context: for example, writing an Apex class triggers the authoring guidelines, which then chain through analysis, deployment, and testing without requiring manual invocation. Coding standards are defined in Markdown rule files inside each skill's `rules/` folder, so you can customize naming conventions, DML practices, testing requirements, and LWC patterns by editing those files directly.

## Skills

| Skill | Triggers when... |
|---|---|
| `write-apex` | Writing or modifying Apex classes or triggers |
| `write-lwc` | Writing or modifying Lightning Web Components |
| `salesforce-code-analysis` | Running Salesforce Code Analyzer on Apex or LWC files |
| `deploy-to-salesforce` | Deploying Apex, triggers, or LWC to a Salesforce org |
| `run-apex-tests` | Running Apex unit tests with coverage reporting |
| `run-lwc-tests` | Running LWC Jest unit tests with coverage reporting |

## Requirements

- [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli) (`sf`)
- [Salesforce Code Analyzer](https://forcedotcom.github.io/sfdx-scanner/) (`sf plugins install @salesforce/sfdx-scanner`)

## Support

This plugin is shared as-is for personal use. I will not be responding to help requests, issues, or pull requests.
