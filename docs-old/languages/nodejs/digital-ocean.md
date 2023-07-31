---
layout: docs
section: "Language Guides"
title: "Deploy a Node.js App to Digital Ocean"
description: Deploy a Node.js app with an encrypted .env.vault file to Digital Ocean.
redirect_from:
  - /docs/integrations/digital-ocean/nodejs
---

{% include docs/headsup.html %}
{% include docs/example_link.html url="https://github.com/dotenv-org/examples/tree/master/nodejs/digital-ocean" %}

## Initial setup

Create an `index.js` file, if you haven't already done so.

##### index.js
```js
// index.js
const PORT = process.env.PORT || 3000
const http = require('http')
const server = http.createServer((req, res) => {
  res.statusCode = 200
  res.setHeader('Content-Type', 'text/plain')
  res.end(`Hello ${process.env.HELLO}`)
})

server.listen(PORT, () => {
  console.log(`Server running on port:${PORT}/`)
})
```

Commit that to code and deploy it to Digital Ocean.

<div class="alert alert-warning">
  <strong>Fork in the road!</strong> Deploying to Digital Ocean takes more steps than we want to document here. Follow their <a href="https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-20-04">guide to deploying a Node.js app to Digital Ocean</a> and then return to this page.
</div>

##### Browser
{% include helpers/screenshot_browser.html url="/assets/img/docs/hello-undefined.png" www="yourapp.com on digital ocean" %}

Once deployed, your app will say `'Hello undefined'` as it doesn't have a way to access the environment variable yet. Let's do that next.

{% include docs/step_install_dotenv.md %}
{% include docs/step_build_env_vault.md %}

## Set DOTENV_KEY

Fetch your production `DOTENV_KEY`.

##### CLI
```shell
npx dotenv-vault@latest keys production
# outputs: dotenv://:key_1234@dotenv.org/vault/.env.vault?environment=production
```

Set `DOTENV_KEY` on Digital Ocean.

##### UI
{% include helpers/screenshot_browser.html url="/assets/img/docs/digitalocean-vars.png" www="digitalocean.com" %}

## Deploy

Commit those changes safely to code and deploy.

That's it! On deploy, your `.env.vault` file will be decrypted and its production secrets injected as environment variables – just in time.

You'll know things worked correctly when you see `'Loading env from encrypted .env.vault'` in your logs. If a `DOTENV_KEY` is not set (for example when developing on your local machine) it will fall back to standard [dotenv](https://github.com/motdotla/dotenv) functionality.

{% include helpers/screenshot_browser.html url="/assets/img/cloudinary/dotenv_vault_digital_ocean_logs_encrypted_loading_env_vault_qcx4yp.png" www="digitalocean.com logs"%}

{% include docs/welldone.html %}