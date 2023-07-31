---
layout: docs
title: "Vercel with Astro - Integrations"
---

{% include icons/vercel.html width="50" color="#00C7B7" %}
{% include icons/astro.html width="50" color="#FF5D01" %}

# Vercel with Astro

Learn how to make Vercel, Astro, and Dotenv Vault work together. This tutorial assumes you have already created a `.env` file and [synced it](/docs/tutorials/sync).

You can find a complete [example repo here](https://github.com/dotenv-org/integration-example-vercel-astro).

## 1. Install dotenv

Install [dotenv](https://github.com/motdotla/dotenv).

```
$ npm install dotenv --save
```

## 2. Preload dotenv

Preload Astro scripts using dotenv. This will inject the environment variables ahead of Astro.

```
"scripts": {
  "dev": "node -r dotenv/config ./node_modules/.bin/astro dev",
  "start": "node -r dotenv/config ./node_modules/.bin/astro dev",
  "build": "node -r dotenv/config ./node_modules/.bin/astro build",
  "preview": "node -r dotenv/config ./node_modules/.bin/astro preview",
  "astro": "astro"
},
```
[example](https://github.com/dotenv-org/integration-example-vercel-astro/blob/master/package.json)

## 3. Run dotenv-vault build

Run npx dotenv-vault build to build your encrypted .env.vault file.

```
$ npx dotenv-vault build
```

## 4. Get DOTENV_KEY

Run npx dotenv-vault keys production.

```
$ npx dotenv-vault keys production
remote:   Listing .env.vault decryption keys... done

dotenv://:key_1234@dotenv.org/vault/.env.vault?environment=production
```

## 5. Set DOTENV_KEY

Visit your Vercel Project > Settings > Environment Variables.

Set **DOTENV_KEY** to the value returned in step 4.

{% include helpers/screenshot.html url="/assets/img/misc/221270962-670778f0-8cf2-4997-9d83-802e0b4d2f9b.png" %}

## 6. Commit and push

That's it!

Commit those changes safely to code and push to GitHub.

When the build runs, it will recognize the `DOTENV_KEY`, decrypt the .env.vault file, and load the production environment variables to `ENV`. If a `DOTENV_KEY` is not set (like during development on your local machine) it will fall back to regular dotenv.

It worked if you see the message 'Loading env from encrypted .env.vault'.

{% include helpers/screenshot.html url="/assets/img/misc/221258650-e5991d39-91cf-4ccf-a9cd-30ddd271918b.png" %}