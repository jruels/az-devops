# Azure DevOps Pipelines Setup Guide

This guide walks through setting up and using Azure Pipelines, from creating your initial DevOps account to running your first pipeline.

## Initial Setup

### Creating Your DevOps Account

1. Visit https://aex.dev.azure.com/
2. Log in with your provided credentials
3. Keep all prepopulated fields as they are
4. Click "Continue"

### Creating Your Organization

1. Click "Create new organization"
2. Uncheck the spam prevention box
3. Name your organization following the format: `<student#MMDDYYYY>`

### Creating Your First Project

1. Name your project: `azdevopsMMDDYYYY`
2. Keep the "Private" setting
3. Click "Create project"

## Setting Up a Self-Hosted Agent

Azure Pipelines can use Microsoft-hosted agents, but they're costly. Instead, we'll set up a self-hosted agent on a Linux VM.

### Prerequisites

- A GitHub account (create one at https://github.com/ if needed)
- A Linux VM for hosting the agent

### Installing the Agent

1. Access Agent Pools:

   - Sign in to your organization at `https://dev.azure.com/{yourorganization}`
   - Navigate to Azure DevOps → Organization settings

   ![Choose Organization settings.](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/media/agent-pools-tab/organization-settings.png?view=azure-devops)

   - Select "Agent pools"

   ![Choose Agent pools tab.](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/media/agent-pools-tab/agent-pools.png?view=azure-devops)

2. Configure the Agent:

   - Select the "Default" pool
   - Click the "Agents" tab
   - Choose "New agent"
   - Select "Linux" and "x64" architecture

3. Download and Install:

   ```bash
   # Download the agent
   wget https://vstsagentpackage.azureedge.net/agent/3.248.0/vsts-agent-linux-x64-3.248.0.tar.gz
   
   # Create and navigate to agent directory
   mkdir $HOME/az-agent
   cd $HOME/az-agent
   
   # Extract the agent
   tar -zxvf ../vsts-agent-linux-x64-3.248.0.tar.gz
   ```

4. Configure the Agent:

   - Run `./config.sh`
   - When prompted:
     - Server URL: `https://dev.azure.com/{your-organization}`
     - Authentication type: `AAD`
     - Complete device code flow authentication in browser
     - Select "Default" for agent pool

## Creating Your First Pipeline

### Setting Up the Repository

1. Fork this repository: `https://jruels/python-sample-vscode-flask-tutorial`

### Creating the Pipeline

1. In your Azure DevOps project, go to Pipelines → New pipeline
2. Select "GitHub" as your code source
3. Sign in to GitHub if prompted
4. Select your forked repository
5. Install Azure Pipelines app if prompted
6. When the Python package template appears, replace it with this YAML:

```yaml
trigger:
- main

resources:
- repo: self

stages:
- stage: Build
  displayName: Build image
  jobs:
  - job: Build
    displayName: Build
    pool:
      name: Default  
      
    steps:
    - task: Docker@2
      displayName: Build an image
      inputs:
        command: 'build'
        Dockerfile: '**/Dockerfile'
        tags: '$(Build.BuildId)'
    
    - script: |
        docker images |head -2
      displayName: Verify and list the new image
```

7. Click "Save and run"
8. Commit the new `azure-pipelines.yml` file to your repository

## Managing Your Pipelines

### Viewing Pipelines

Access the pipelines dashboard via the left menu. You'll see a view similar to this:

![Screenshot of pipelines landing page.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipelines-overview.png?view=azure-devops)

View options:

- "Recent": Shows recently run pipelines (default view)
- "All": Shows all pipelines

![Screenshot of options for viewing pipeline runs on the pipelines landing page.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/view-pipelines.png?view=azure-devops)

When viewing recently run pipelines, you'll see something like this:

![Screenshot of recently run pipelines.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipelines-overview-pipeline-context-menu.png?view=azure-devops)

### Pipeline Run Details

The pipeline runs view shows all pipeline executions:

![Screenshot of pipeline runs.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/all-pipeline-runs.png?view=azure-devops)

You can manage runs using the context menu:

![Screenshot of pipeline run context menu.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-run-context-menu.png?view=azure-devops)

### Pipeline Details Page

The details page provides comprehensive information about your pipeline:

![Screenshot of pipeline details page.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-overview.png?view=azure-devops)

### Run Summary

The run summary provides status and details of your pipeline execution:

![Screenshot of pipeline run summary.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-run-summary.png?view=azure-devops)

### Jobs and Stages View

Monitor your pipeline's progress through different stages:

![Screenshot of pipeline jobs and stages.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-jobs-pane.png?view=azure-devops)

Individual steps within jobs can be viewed in detail:

![Screenshot of pipeline tasks.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-steps-list.png?view=azure-devops)

The steps view includes additional options:

![Screenshot of pipeline tasks content menu.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-steps-context-menu.png?view=azure-devops)

### Pipeline Controls

During execution, you have several control options:

![Screenshot of cancelling a pipeline run.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/cancel-pipeline-run.png?view=azure-devops)

The "More actions" menu provides additional management options:

![Screenshot of pipeline run summary page more actions menu.](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/pipeline-run-summary-context-menu.png?view=azure-devops)

## Best Practices

- Regularly monitor pipeline runs
- Review build logs for errors
- Keep pipeline configurations in version control
- Use meaningful names for pipelines and stages
- Clean up old runs to manage storage

This guide provides the foundation for working with Azure Pipelines. As you become more familiar with the system, you can explore advanced features and customize pipelines for your specific needs.