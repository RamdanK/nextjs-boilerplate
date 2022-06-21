## Project Setup

We'll begin by creating a default NextJs application with a Typescript template.

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Engine Locking

We would like for all developers working on this project to use the same Node engine and package manager we are using. TO do that we create two new files:

- `.nvmrc` -- Will tell other uses of the project which version of Node is used
- `.npmrc` - WIll tell other users of the project which package manager is used

We are using `Node v14.19.0` and `yarn` for this project so we set those values like so:

`.nvmrc`

```.nvmrc
14.19.0
```

`.npmrc`

```
engine-strict=true
```

You can check your version of Node with `node --version` and make sure you are setting the correct one. A list of Node version codenames can be found [here](https://github.com/nodejs/Release/blob/main/CODENAMES.md)

Note that the use of `engine-strict` didn't specifically say anything about `yarn`, we do that in `package.json`:

`package.json`

```json
  "name": "brixee-link-bio",
  "version": "0.1.0",
  "private": true,
  ...
  "engines": {
    "node": ">=14.0.0",
    "yarn": ">=1.22.0",
    "npm": "please-use-yarn"
  },
  ...
```

## ESLint
We'll begin with ESLint, which is easy because it automatically comes installed and pre-configured with Next.js projects.

We are just going to add a little bit of extra configuration and make it a bit stricter than it is by default. If you disagree with any of the rules it sets, no need to worry, it's very easy to disable any of them manually. We configure everything in .eslintrc.json which should already exist in your root directory:

`.eslintrc.json`

```
{
  "extends": ["next", "next/core-web-vitals", "eslint:recommended"],
  "globals": {
    "React": "readonly"
  },
  "rules": {
    "no-unused-vars": [1, { "args": "after-used", "argsIgnorePattern": "^_" }]
  }
}
```

In the above small code example we have added a few additional defaults, we have said that React will always be defined even if we don't specifically import it, and I have added a personal custom rule that I like which allows you to prefix variables with an underscore _ if you have declared them but not used them in the code.

I find that scenario comes up often when you are working on a feature and want to prepare variables for use later, but have not yet reached the point of implementing them.