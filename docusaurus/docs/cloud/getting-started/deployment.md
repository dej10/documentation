---
title: Deployment
displayed_sidebar: cloudSidebar
description: Learn how to deploy your Strapi application on Strapi Cloud.
canonicalUrl: https://docs.strapi.io/cloud/getting-started/deployment.html
---

# Strapi Cloud

This is a step-by-step guide for deploying your Strapi application on Strapi Cloud. Before you are able to access Strapi Cloud, you must first [request access](#requesting-access) to the Beta release.

## Prerequisites

Before you can deploy your Strapi application on Strapi Cloud, you need to have the following prerequisites:

* Strapi version `4.4.x` or higher
* Database: Project must be compatible with PostgreSQL. Use of any external database is not supported.
* Project(s) source code hosted on [GitHub](https://github.com)
    * The connected repository can contain multiple Strapi applications. Each Strapi app must be in a separate directory.

:::warning
Importing data from an existing Strapi application and data backups for a Strapi Cloud application are not supported at this time. These features will be available in the future.
:::

## Getting started

1. Navigate to the [Strapi Cloud](https://cloud.strapi.io) login page.

    ![Strapi Cloud login page](/img/assets/cloud/login.png)

2. You are prompted to **Log In with GitHub**. Your Strapi Cloud account is created during this initial login.

3. Once logged in, you will be redirected to the Strapi Cloud **Projects** page. From here you can create your first Strapi Cloud project.

    ![Strapi Cloud Projects page](/img/assets/cloud/projects_empty.png)

### Create a project

1. From the **Projects** page, click the **Create Project** button. You are prompted to **Connect with GitHub**.

    :::tip
    Connect the GitHub account and/or Organizations that own the repository or repositories you want to deploy. This can be different from the account that owns the Strapi Cloud account.

    You will be redirected to GitHub to authorize Strapi Cloud to access your repository.
    :::

2. After granting the required access from GitHub, from the **Projects** page select your desired repository to install Strapi Cloud.

    ![Project Import - Select Repository](/img/assets/cloud/import.png)

3. Click **Next** to proceed to the Project Set up page and enter the following information:
    * **Project name**: The name of your Strapi app, this is fetched from the repository name but can be edited. It is automatically converted to slug format (`my-strapi-app`).
    * **GitHub branch**: The default branch to use for this deployment. This uses the [default branch](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/changing-the-default-branch) of the repository but can be changed via the drop-down.
    * **Deploy on push**: When enabled, this will automatically deploy the latest changes from the selected branch. When disabled, you will need to manually deploy the latest changes.

    ![Project Setup](/img/assets/cloud/setup.png)

4. (**Optional**) Select **Show Advanced Settings** to configure the following options:
    * [**Environment variables**](/dev-docs/configurations/environment.md): Environment variables are used to configure your Strapi app.
    * **Base directory**: The directory where your Strapi app is located in the repository. This is useful if you have multiple Strapi apps in the same repository or if you have a monorepo.

    ![Advanced Setup](/img/assets/cloud/advanced.png)

5. Click **Create** to finalize the project creation. An initial deployment is triggered and you are redirected to the **Projects** page.
