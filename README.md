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

## Configuring Travis CI

To configure Travis CI, we create a `.travis.yml` file, which will contain
information for Travis on how to handle the compilation of the project.

We have to specify an environment, which is one of the list below (which can
[be found in the docs of Travis CI][docs-languages]):

![List of languages supported by Travis CI][img-languages]

In our case, we use `node_js` and we want it to run `npm test`. This means we
have to specify which NodeJS versions we want to test and what command we want
to run. The `node_js` environment will run `npm install` for us, so we don't
need to mention that.

```yaml
language: node_js

node_js:
  - "node"
  - "6"

script:
  - npm test
```

Now we need to go to [our Travis account][travis-mya] and enable the repository
we want to use.

![Enable the repo][img-enable-repo]

After we've done this, we can commit everything we've added, and push it to
GitHub. Travis will then start running a build and will report back the
results.

```bash
git add .eslintrc .travis.yml package.json
git commit -m "Initial commit"
```

As we don't have any code yet, the build may fail as eslint has nothing to
check and will report an error instead.

## Fixing the code

![First build, which fails][img-build-fail]

As the current code is broken, we need to fix it. The Travis CI log contains
error information on what's broken and what is not.

```
$ npm test
> travis-demo@1.0.0 test /home/travis/build/teamfieldtrip/travis-demo
> eslint src/

/home/travis/build/teamfieldtrip/travis-demo/src/index.js
  1:1   error  Expected an assignment or function call and      no-unused-expressions
               instead saw an expression
  1:10  error  Missing space before function parentheses        space-before-function-paren
  2:5   error  Expected indentation of 2 spaces but found 4     indent
  2:17  error  Extra semicolon                                  semi
  4:5   error  Expected indentation of 2 spaces but found 4     indent
  4:28  error  Missing space before function parentheses        space-before-function-paren
  5:9   error  Expected indentation of 6 spaces but found 8     indent
  5:41  error  Extra semicolon                                  semi
  6:6   error  Extra semicolon                                  semi
  8:5   error  Expected indentation of 2 spaces but found 4     indent
  8:60  error  Extra semicolon                                  semi
  9:3   error  Extra semicolon                                  semi
✖ 12 problems (12 errors, 0 warnings)

npm ERR! Test failed.  See above for more details.

The command "npm test" exited with 1.
```

It's a lot of errors, but not too much to worry about. After fixing the code
and commit it, the build will succeed.

```patch
diff --git a/src/index.js b/src/index.js
index 68f697a..f5055da 100644
--- a/src/index.js
+++ b/src/index.js
@@ -1,9 +1,9 @@
-(function() {
-    'use strict';
+(function () {
+  'use strict'

-    var sayHello = function() {
-        console.log('Mein little Füher');
-    };
+  var sayHello = function () {
+    console.log('Mein little Füher')
+  }

-    document.addEventListener('DOMContentLoaded', sayHello);
-});
+  document.addEventListener('DOMContentLoaded', sayHello)
+}())
```

After we've applied the above patch, and committed it, the build will succeed.

<!-- TODO add image -->
![Second build, which passes][img-build-pass]

<!-- Links -->
[travis-shield]: https://img.shields.io/travis/teamfieldtrip/travis-demo.svg
[travis-link]: https://travis-ci.org/teamfieldtrip/travis-demo

[license-shield]: https://img.shields.io/github/license/teamfieldtrip/travis-demo.svg
[license-link]: LICENSE.md

[standard-shield]: https://img.shields.io/badge/code_style-standard-brightgreen.svg
[standard-link]: http://standardjs.com/

[docs-languages]: https://docs.travis-ci.com/
[img-languages]: img/languages.png
[img-enable-repo]: img/enable-repo.png
[img-build-fail]: img/build-failed.png
[img-build-pass]: img/build-passed.png

[travis]: https://travis-ci.org/
[travis-mya]: https://travis-ci.org/profile/
