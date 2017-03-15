# Travis CI demo

[![Build status][travis-shield]][travis-link]
[![Standard JS Code Standard][standard-shield]][standard-link]
[![GPL-3.0 license][license-shield]][license-link]

This repo contains a demo for the Travis CI codebase.

## Setting up NPM

We use `npm init`, which is pretty self-explanatory. The only step you need to
really look for is the `test command` question.

For that, we use eslint to check the `/src` directory.

```
test command: eslint src/
```

That's it, then we just need to install the dependencies:

```
npm install --save-dev \
    eslint \
    eslint-config-standard \
    eslint-plugin-import \
    eslint-plugin-promise \
    eslint-plugin-standard
```

## Configuring ESLint

ESLint requires an `.eslintrc` file, which contains configuration data.

Luckily, this is very easy, since the Standard code standard basically defines
all rules for ESLint.

```json
{
  "extends": "standard",
  "env": {
    "node": true
  }
}
```

<!-- Links -->
[travis-shield]: https://img.shields.io/travis/teamfieldtrip/travis-demo.svg
[travis-link]: https://travis-ci.org/teamfieldtrip/travis-demo

[license-shield]: https://img.shields.io/github/license/teamfieldtrip/travis-demo.svg
[license-link]: LICENSE.md

[standard-shield]: https://img.shields.io/badge/code_style-standard-brightgreen.svg
[standard-link]: http://standardjs.com/
