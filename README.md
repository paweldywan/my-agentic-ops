# My Agentic Ops

This repository provides a VS Code Copilot agent workflow for planning and provisioning Azure infrastructure from a workload description. The agents turn requirements into an architecture assessment, generate Bicep infrastructure code, and can provision the resulting resources with the Azure Developer CLI (`azd`).

## What's included

- **01-conductor** coordinates the workflow and verifies the artifacts produced by each stage.
- **02-architect** translates a workload description into resource recommendations, dependencies, naming, and security decisions.
- **03-bicep-deploy** generates Bicep and an `azd` project manifest, then runs the provisioning workflow.
- **Azure Operations Defaults** provides shared CAF-style naming conventions, security requirements, and development and production SKU defaults.
- **VS Code settings** enable repository-provided agents and skills.

## Prerequisites

- Visual Studio Code with GitHub Copilot Chat and support for custom agents.
- Azure Developer CLI (`azd`) installed and authenticated to the intended Azure tenant and subscription.
- Azure permissions to create the resources required by your workload.

## Use the workflow

1. Open this repository in VS Code and start a Copilot Chat session.
2. Select **01-conductor** as the agent.
3. Describe the workload, target environment, Azure region, and any constraints or preferences.
4. Start the workflow only when you are ready to provision resources. The conductor verifies artifacts between stages, and the deployment stage provisions resources through `azd`.
5. Check the deployment summary for the outcome and resource details.

The conductor runs the architecture and infrastructure stages in order, checking that each stage's expected artifacts are present before continuing.

## Before deploying

Review the generated architecture and Bicep for correctness and security, and confirm the active Azure tenant, subscription, and region. Provisioning can create billable resources; review Azure pricing and clean up resources you no longer need.

The shared defaults specify minimum TLS 1.2 for public endpoints, HTTPS-only App Services, managed identities for service-to-service access, Key Vault RBAC, and Entra ID authentication alongside SQL authentication.

## Repository layout

```text
.github/
  agents/       Copilot agent definitions
  skills/       Shared Azure provisioning defaults
  instructions/ Bicep authoring guidance
.vscode/        VS Code Copilot configuration
README.md
```
