---
title: Steps
description: Adding steps to define your project's deployment process.
position: 2
---

Octopus strives to make it quick and easy to define your project's deployment process.  Selecting the **ADD STEP** button displays a list of built-in step templates, custom step templates, and community contributed step templates.

Built-in steps are powerful and flexible enough to handle the most common deployment scenarios.  

![](built-in-steps.png "width=500")

Custom step templates enable you to encapsulate common steps/scenarios within your team or company. 

Learn more about [Custom Step Templates](/docs/deployment-process/steps/custom-step-templates.md).

Octopus community library integration makes it easy to find steps templates that work with the frameworks and technologies you use without the need for custom scripting.

![](community-steps.png "width=500") 

Learn more about [Community Step Templates](/docs/deployment-process/steps/community-step-templates.md).

Learn more about [Updating Step Templates](/docs/deployment-process/steps/updating-step-templates.md) and [Exporting Step Templates](/docs/deployment-process/steps/exporting-step-templates.md)

:::hint
Prior to Octopus 3.7, selecting the add step button showed a popup list of built-in steps and any installed step templates (community contributed or custom).  Installing a community step required visiting the [Community Library](http://library.octopusdeploy.com/) and importing the step manually.  For more information, see [community step templates](/docs/deployment-process/steps/community-step-templates.md).

![](/docs/images/5672131/5865901.png "width=500")
:::

## Common Step Properties {#Deployingapplications-Commonstepproperties}

All steps have a name, which is used to identify the step.

:::success
**What&#39;s in a Name?**
Be careful when changing names! Octopus commonly uses names as a convenient identity or handle to things, and the steps and actions in a deployment process are special in that way. For example you can use [output variables](/docs/deployment-process/variables/output-variables.md) to chain steps together, and you use the name as the indexer for the output variable. For example: `#{Octopus.Action[StepA].Output.TestResult}`
:::

## Adding an installed step {#Addingsteps-Addinganinstalledstep}

The add step page displays the built-in steps first which includes common steps to deploy IIS web sites, windows services, run scripts and more.  The built-in steps have been develop by the Octopus team to handle the most common deployment scenarios and it also.  This section also includes any custom step templates added in the library.  Hover over a step and click add step to go configure the step.

![](add-builtin-step.png "width=300")

## Adding a community contributed step templates {#Addingsteps-Addingacommunitycontributedsteptemplates}

The add step page also displays community contributed step templates available to install and add.  You can search for a specific template or you can browse through the categories.  Installing a community step template is easy.  Hover over a step and select Install and add step.  This will display a pop-up dialog where you can confirm to install and add the step.  This will take you to the configuration page for the step template.

![](install-community-step.png "width=300")

![](install-community-step-popup.png "width=500")

If you select view details, this will take you to the community step details page which shows you the complete details of the step include the source code.  You can install the step or go back to the list of steps.

![](install-community-step-details.png "width=500")

## Adding an updated version of a community step template {#Addingsteps-Addinganupdatedversionofacommunitysteptemplate}

Sometimes updates are available for step templates.  In this case, you will notice the step template has an option to update the step.  If you select update, this will take you to the community step details with the option to update the latest version of the step template.  Community step templates can also be updated in the library as needed.

![](update-community-step.png)

![](update-community-step-details.png "width=500")

:::success
If a step you want isn't built-in you should check out the community contributed [step templates](/docs/deployment-process/steps/index.md). If you still don't find it, don't forget: *Octopus can do anything, as long as you can script the instructions*. Maybe you could contribute your scripts back to the community?
:::

## Execution Order

The steps that you add to your deployment process will, by default, execute in sequence.

![](5865849.png "width=300")
If a step is configured to execute across multiple deployment targets, it will execute across all of those deployment targets in parallel, unless you specify a window size. Specifying a window size limits the number of deployment targets steps will execute against in parallel.

![](5865850.png "width=300")

Steps can include multiple actions.

![](5865848.png "width=500")

## Example: A simple deployment process {#DeploymentProcesses-Example:Asimpledeploymentprocess}

In the example shown below there are three steps that will be executed from top to bottom. The first is a [manual intervention](/docs/deployment-process/steps/manual-intervention-and-approvals.md) which executes on the Octopus Server pausing the deployment until someone intervenes and allow the deployment to continue. This step will only execute when targeting the Production [environment](/docs/infrastructure/environments/index.md). The remaining steps both [deploy a package](/docs/deployment-process/deploying-packages/index.md) and execute [custom scripts](/docs/deploying-applications/custom-scripts/index.md) on all of the [deployment targets](/docs/infrastructure/index.md) with the [role](/docs/infrastructure/environments/target-roles/index.md) **web-server**.

![](simple-process.png "width=500")

## Example: A rolling deployment {#DeploymentProcesses-Example:Arollingdeployment} {#rolling-deployments}

Let's consider a more complex example like the one shown below. In this example we have configured Octopus to deploy a web application across one or more servers in a web farm behind a load balancer. This process has a single **step** and three **actions** which form a [rolling deployment](/docs/deployment-patterns/rolling-deployments.md).

![](rolling-process.png "width=500")
