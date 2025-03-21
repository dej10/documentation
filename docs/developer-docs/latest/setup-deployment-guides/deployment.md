---
title: Deployment - Strapi Developer Docs
description: Learn how to develop locally with Strapi and deploy Strapi with various hosting options.
canonicalUrl: https://docs.strapi.io/developer-docs/latest/setup-deployment-guides/deployment.html
---

# Deployment

Strapi provides many deployment options for your project or application. Your Strapi applications can be deployed on traditional hosting servers or your preferred hosting provider. 

The following documentation covers how to develop locally with Strapi and deploy Strapi with several common hosting options.

::: callout ☁️ Strapi Cloud
Don't want to deploy Strapi by yourself? <a href="https://strp.cc/3rywrsu" target="_blank" id="deployment-section-cloud-link">Join the cloud waitlist</a> to soon get access to a platform to easily deploy and host your project.
:::

::: strapi Community Guides
In addition to the official deployment guides maintained by Strapi that are found here, community-maintained guides for additional providers are available in the [Strapi Forum](https://forum.strapi.io/c/community-guides/28).
:::

## General guidelines

### Hardware and software requirements

To provide the best possible environment for Strapi the following requirements apply to development (local) and staging and production workflows.

- Node LTS (v14 or v16) **Odd-number releases of Node are not supported (e.g. v13, v15).**
- NPM v6 (or the version shipped with the LTS Node versions)
- Standard build tools for your OS (the `build-essentials` package on most Debian-based systems)
- Hardware specifications for your server (CPU, RAM, storage):

| Hardware | Minimum | Recommended |
|----------|---------|-------------|
| CPU      | 1 core  | 2+ cores    |
| Memory   | 2GB     | 4GB+        |
| Disk     | 8GB     | 32GB+       |

- A supported database version:

::: strapi Database deployment
Deploying databases along with Strapi is covered in the [databases guide](/developer-docs/latest/setup-deployment-guides/configurations/required/databases.md#databases-installation-guides).
:::

| Database   | Minimum | Recommended |
|------------|---------|-------------|
| MySQL      | 5.7.8   | 8.0         |
| MariaDB    | 10.3    | 10.6        |
| PostgreSQL | 11.0    | 14.0        |
| SQLite     | 3       | 3           |

- A supported operating system:

| Operating System | Minimum | Recommended |
|------------------|---------|-------------|
| Ubuntu (LTS)     | 20.04   | 22.04       |
| Debian           | 10.x    | 11.x        |
| CentOS/RHEL      | 8.x     | 9.x         |
| macOS            | 10.15   | 11.0        |
| Windows Desktop  | 10      | 11          |
| Windows Server   | 2019    | 2022        |

### Application Configuration

#### 1. Configure

We recommend using environment variables to configure your application based on the environment, for example:

```js
// Path: ./config/server.js

module.exports = ({ env }) => ({
  host: env('APP_HOST', '0.0.0.0'),
  port: env.int('NODE_PORT', 1337),
});
```

Then you can create a `.env` file or directly set environment variables in your chosen deployment platform:

```
APP_HOST=10.0.0.1
NODE_PORT=1338
```

::: tip
To learn more about configuration details, see the [configurations](/developer-docs/latest/setup-deployment-guides/configurations.md) documentation.
:::

#### 2. Launch the server

Before running your server in production you need to build your admin panel for production:

:::: tabs card

::: tab yarn

```bash
NODE_ENV=production yarn build
```

:::

::: tab npm

```bash
NODE_ENV=production npm run build
```

:::

::: tab Windows

```bash
npm install cross-env
```

Then in your `package.json` scripts section:

```bash
"build:win": "cross-env NODE_ENV=production npm run build",
```

And run:

```bash
npm run build:win
```

:::

::::

Run the server with the `production` settings:

:::: tabs card

::: tab yarn

```bash
NODE_ENV=production yarn start
```

:::

::: tab npm

```bash
NODE_ENV=production npm start
```

:::

::: tab Windows

```bash
npm install cross-env
```

Then in your `package.json` scripts section:

```bash
"start:win": "cross-env NODE_ENV=production npm start",
```

And run:

```bash
npm run start:win
```

:::

::::

::: caution
We highly recommend using [pm2](https://github.com/Unitech/pm2/) to manage your process.
:::

If you need a server.js file to be able to run `node server.js` instead of `npm run start` then create a `./server.js` file as follows:

```js
const strapi = require('@strapi/strapi');

strapi(/* {...} */).start();
```

### Advanced configurations

If you want to host the administration on another server than the API, [please take a look at this dedicated section](/developer-docs/latest/development/admin-customization.md#deployment).

## Hosting Provider Guides

Manual guides for deployment on the following platforms:

<div>
	<InstallLink link="deployment/hosting-guides/amazon-aws.html">
    <template #icon>
    <svg width="64" height="64" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg"><g fill="#fff" fill-rule="evenodd"><path d="M15.63 31.388l-7.135-2.56V18.373l7.135 2.43zm1.3 0l7.135-2.56V18.373l-7.135 2.432zm-7.7-13.8l7.2-2.033 6.696 2.16-6.696 2.273zm-2.092-.8L0 14.22V3.75l7.135 2.43zm1.307 0l7.135-2.56V3.75L8.443 6.192zm-7.7-13.8l7.2-2.043 6.696 2.16-6.696 2.273zm23.052 13.8l-7.135-2.56V3.75l7.135 2.43zm1.3 0l7.135-2.56V3.75l-7.135 2.43zm-7.7-13.8l7.2-2.033 6.696 2.16-6.696 2.273z" fill-rule="nonzero"></path></g></svg>
    </template>
		<template #title>Amazon AWS</template>
		<template #description>
			Step by step guide for deploying on AWS EC2
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/hosting-guides/azure.html">
    <template #icon>
    <svg width="100" height="77.43" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 19.68 15.24"><path d="M9.105 14.43l4.642-.82.043-.01-2.387-2.84a403.945 403.945 0 0 1-2.387-2.853c0-.014 2.465-6.802 2.479-6.826.004-.008 1.682 2.888 4.066 7.02l4.09 7.09.031.054-7.587-.001-7.587-.001 4.597-.812zM0 13.566c0-.004 1.125-1.957 2.5-4.34L5 4.893l2.913-2.445C9.515 1.104 10.83.002 10.836 0a.512.512 0 0 1-.047.118L7.625 6.903l-3.107 6.663-2.259.003c-1.242.002-2.259 0-2.259-.004z" fill="#fff"/></svg>
    </template>
		<template #title>Azure</template>
		<template #description>
			Step by step guide for deploying on Azure
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/hosting-guides/digitalocean-app-platform.html">
		<template #icon>
			<svg width="178" height="177" viewBox="0 0 178 177" xmlns="http://www.w3.org/2000/svg"><g fill="#fff" fill-rule="evenodd"><path d="M89 176.5v-34.2c36.2 0 64.3-35.9 50.4-74-5.1-14-16.4-25.3-30.5-30.4-38.1-13.8-74 14.2-74 50.4H.8C.8 30.6 56.6-14.4 117.1 4.5c26.4 8.3 47.5 29.3 55.7 55.7 18.9 60.5-26.1 116.3-83.8 116.3z" fill-rule="nonzero"></path><path d="M89.1 142.5H55v-34.1h34.1zM55 168.6H28.9v-26.1H55zM28.9 142.5H7v-21.9h21.9v21.9z"></path></g></svg>
		</template>
		<template #title>DigitalOcean App Platform</template>
		<template #description>
			Manual step by step guide for deploying on DigitalOcean App Platform
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/hosting-guides/digitalocean.html">
		<template #icon>
			<svg width="178" height="177" viewBox="0 0 178 177" xmlns="http://www.w3.org/2000/svg"><g fill="#fff" fill-rule="evenodd"><path d="M89 176.5v-34.2c36.2 0 64.3-35.9 50.4-74-5.1-14-16.4-25.3-30.5-30.4-38.1-13.8-74 14.2-74 50.4H.8C.8 30.6 56.6-14.4 117.1 4.5c26.4 8.3 47.5 29.3 55.7 55.7 18.9 60.5-26.1 116.3-83.8 116.3z" fill-rule="nonzero"></path><path d="M89.1 142.5H55v-34.1h34.1zM55 168.6H28.9v-26.1H55zM28.9 142.5H7v-21.9h21.9v21.9z"></path></g></svg>
		</template>
		<template #title>DigitalOcean Droplets</template>
		<template #description>
			Manual step by step guide for deploying on DigitalOcean droplets
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/hosting-guides/google-app-engine.html">
		<template #icon>
			<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24" version="1.1"><path d="M6.969 3L4.094 8.188l1.468 2.624L8.438 6h10.25L17 3zm8.75 4l2.969 4.906L13.625 21H17l5-9-2.781-5zM12 8c-2.207 0-4 1.793-4 4s1.793 4 4 4 4-1.793 4-4-1.793-4-4-4zM3.531 9.219L2 12l4.969 9H12.5l1.656-3h-5.75zM12 10c1.102 0 2 .898 2 2 0 1.102-.898 2-2 2-1.102 0-2-.898-2-2 0-1.102.898-2 2-2z" fill="#fff"/></svg>
		</template>
		<template #title>Google App Engine</template>
		<template #description>
			Manual step by step guide for deploying on GCP's App Engine
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/hosting-guides/heroku.html">
    <template #icon>
    <svg xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 5.12 5.12" preserveAspectRatio="xMinYMin meet"><path d="M3.068 4.415V2.382s.132-.487-1.63.2C1.436 2.6 1.436.7 1.436.7L2.01.697v1.2s1.61-.635 1.61.48v2.026h-.555zm.328-2.986h-.6c.22-.27.42-.73.42-.73h.63s-.108.3-.44.73zm-1.95 2.982V3.254l.58.58-.58.58z" fill="#fff"/></svg>
    </template>
		<template #title>Heroku</template>
		<template #description>
			Step by step guide for deploying on Heroku
		</template>
	</InstallLink>
</div>


## Optional Software Guides

Additional guides for optional software additions that compliment or improve the deployment process when using Strapi in a production or production-like environment.

<div>
	<InstallLink link="deployment/optional-software/caddy-proxy.html">
    <template #icon>
    <!-- <img src="assets/deployment/caddy-monotone.svg"/> -->
    CAD
    </template>
		<template #title>Caddy</template>
		<template #description>
			Overview of proxying Strapi with Caddy
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/optional-software/haproxy-proxy.html">
    <template #icon>
    HAP
    </template>
		<template #title>HAProxy</template>
		<template #description>
			Overview of proxying Strapi with HAProxy
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/optional-software/nginx-proxy.html">
    <template #icon>
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="-35.5 26 32 32" width="64" height="64"><path d="M-33.442 42.023v-7.637a.68.68 0 0 1 .385-.651l13.173-7.608c.237-.148.503-.178.74-.03l13.232 7.637a.71.71 0 0 1 .355.651V49.63a.71.71 0 0 1-.355.651l-11.367 6.57a56.27 56.27 0 0 1-1.806 1.036c-.266.148-.533.148-.8 0l-13.202-7.608c-.237-.148-.355-.326-.355-.622v-7.637z" fill="#fff"/><path d="M-24.118 39.18v8.9c0 1.006-.8 1.894-1.865 1.865-.65-.03-1.154-.296-1.5-.858-.178-.266-.237-.562-.237-.888V35.836c0-.83.503-1.42 1.154-1.687s1.302-.207 1.954 0c.622.178 1.095.562 1.5 1.036l7.874 9.443c.03.03.06.09.118.148v-9c0-.947.65-1.687 1.57-1.776 1.154-.148 1.924.68 2.042 1.54v12.6c0 .7-.326 1.214-.918 1.54-.444.237-.918.296-1.42.266a3.23 3.23 0 0 1-1.954-.829c-.296-.266-.503-.592-.77-.888l-7.49-8.97c0-.03-.03-.06-.06-.09z" fill="#3498DB"/></svg>
    </template>
		<template #title>Nginx</template>
		<template #description>
			Overview of proxying Strapi with Nginx
		</template>
	</InstallLink>
</div>

<div>
	<InstallLink link="deployment/optional-software/process-manager.html">
    <template #icon>
    <!-- <img src="assets/deployment/caddy-monotone.svg"/> -->
    PM2
    </template>
		<template #title> PM2 Process Manager</template>
		<template #description>
			Overview of using the PM2 process manager with Strapi.
		</template>
	</InstallLink>
</div>
