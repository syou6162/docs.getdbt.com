--- 
title: "Enable dbt Copilot" 
sidebar_label: "Enable dbt Copilot" 
description: "Enable the dbt Copilot AI engine in dbt Cloud to speed up your development." 
---

# Enable dbt Copilot <Lifecycle status='beta'/>

This page explains how to enable the dbt Copilot engine in dbt Cloud, leveraging AI to speed up your development and allowing you to focus on delivering quality data.

## Prerequisites

- Available in the dbt Cloud IDE only.
- Must have an active [dbt Cloud Enterprise account](https://www.getdbt.com/pricing).
- Development environment has been upgraded to ["Versionless"](/docs/dbt-versions/upgrade-dbt-version-in-cloud#versionless).
- By default, dbt Copilot deployments use a central OpenAI API key managed by dbt Labs. Alternatively, you can [provide your own OpenAI API key](#bringing-your-own-openai-api-key-byok).
- Accept and sign legal agreements. Reach out to your Account team to begin this process.

## Enable dbt Copilot

dbt Copilot is only available to your account after your organization has signed the required legal documents. It's disabled by default. A dbt Cloud admin can enable it by following these steps:

1. Navigate to **Account settings** in the navigation menu.

2. Under **Settings**, confirm the account you're enabling.

3. Click **Edit** in the top right corner.

4. Enable the **Enable account access to AI-powered features** option.

5. Click **Save**. You should now have the dbt Copilot AI engine enabled for use.

Note: To disable (only after enabled), repeat steps 1 to 3, toggle off in step 4, and repeat step 5.

<Lightbox src="/img/docs/deploy/example-account-settings.png" width="90%" title="Example of the 'Enable account access to AI-powered feature' option in Account settings" />

### Bringing your own OpenAI API key (BYOK)

Once AI features have been enabled, you can provide your organization's OpenAI API key. dbt Cloud will then leverage your OpenAI account and terms to power dbt CoPilot. This will incur billing charges to your organization from OpenAI for requests made by dbt CoPilot.

Note that Azure OpenAI is not currently supported, but will be in the future.

A dbt Cloud admin can provide their API key by following these steps:

1. Navigate to **Account settings** in the side menu.

2. Find the **Settings** section and click on **Integrations**.

3. Scroll to **AI** and select the toggle for **OpenAI**

4. Enter your API key and click **Save**.