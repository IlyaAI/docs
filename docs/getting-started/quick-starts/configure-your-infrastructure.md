---
title: Configure your Infrastructure
position: 2
description: A quick-start to configure your infrastructure for Octopus Deploy.
---

Before you can deploy your applications, you need to configure the infrastructure you’ll be deploying to. In this quick-start, we’ll configure an **Octopus Tentacle** on the same virtual machine we installed **Octopus Deploy** on in [the previous guide](/docs/getting-started/quick-start/install-a-trial-version-of-octopus-deploy.md).

### What you need

* A trial instance of Octopus Deploy.
* [Octopus Tentacle installer](https://octopus.com/downloads).

### Add an environment

Environments are groups of machines that you deploy to.

1. From the **Octopus Web Portal Dashboard**, click {{Environments>Add Environment}}.
1. Give the environment a name, we’ll use “Test Environment”.
1. Select **Use guided failure mode by default**.
1. Click **Save**.

### Add a deployment target

Octopus needs to know where to deploy your applications. In this step we’ll configure Octopus to deploy applications to your local machine (or inside the virtual machine you’re using).

1. From the **Environments** tab, click **Add deployment target**.

   ![Add deployment target](add-deployment-target.png width="500")
1. Select **Listening Tentacle**.
1. Copy the **thumbprint** (the long string of bolded alphanumeric characters further down the screen) as we’ll need that to configure the **Tentacle**.

   ![Thumbprint](thumbprint.png width="500")
1. Leave the browser open as we’ll be coming back here shortly.

### Install Octopus Tentacle

**Octopus Tentacle** is a lightweight deployment agent service that runs as a Windows service. Tentacle needs to be installed on all the machines you plan to deploy software to. In this guide we’re deploying **Octopus Deploy** and **Octopus Tentacle** on the same machine.

1. Start the Octopus Tentacle installer.
1. Click **next** then accept the license.
1. Accept the default installation location and click **install**.
1. Allow the app to make changes to your device.
1. When the installer has finished, click **Finish** to launch **Tentacle Manager**.

![Tentacle Manager](tentacle-manager.png width="500")

### Configure the Tentacle

1. In Tentacle Manager, click **Get Started…**.
1. Click **Next** and accept the default storage locations.
1. We’ll install Tentacle as a **Listening Tentacle** so accept the default and click **Next**.
1. Paste the thumbprint you copied earlier into the **Octopus Thumbprint** field and click **Next**.
1. Click **Install**.
1. When you see “Installation complete”, click **Finish**.

![Successful tentacle installation](tentacle-installation-successful.png width="500")

### Discover the Tentacle

Now we need to connect **Octopus Deploy** and the **Tentacle** we’ve installed.

1. Back in the **Octopus Web Portal**, continuing in the **New Deployment Target** screen, enter the hostname: *localhost*.
1. Click **Discover**.
1. Enter a unique name for the deployment target. I’m using *Local Machine*.
1. Add a role for the deployment target. I’m using *Test-server*.
1. Click **Save**.

### Health Check

To make sure **Octopus** and **Tentacle** are communicating properly, we’ll conduct a health check.

1. Click the **Check health**.

The task progress is displayed on the screen.

![Health Check](health-check.png width=500")

Congratulations, your infrastructure is configured.
