# npmdoc-errorhandler

#### api documentation for  [errorhandler (v1.5.0)](https://github.com/expressjs/errorhandler)  [![npm package](https://img.shields.io/npm/v/npmdoc-errorhandler.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-errorhandler) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-errorhandler.svg)](https://travis-ci.org/npmdoc/node-npmdoc-errorhandler)

#### Development-only error handler middleware

[![NPM](https://nodei.co/npm/errorhandler.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/errorhandler)

- [https://npmdoc.github.io/node-npmdoc-errorhandler/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-errorhandler/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-errorhandler/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-errorhandler/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-errorhandler/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-errorhandler/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/expressjs/errorhandler/issues"
    },
    "contributors": [
        {
            "name": "Douglas Christopher Wilson"
        },
        {
            "name": "Jonathan Ong",
            "url": "http://jongleberry.com"
        }
    ],
    "dependencies": {
        "accepts": "~1.3.3",
        "escape-html": "~1.0.3"
    },
    "description": "Development-only error handler middleware",
    "devDependencies": {
        "after": "0.8.2",
        "eslint": "3.10.2",
        "eslint-config-standard": "6.2.1",
        "eslint-plugin-promise": "3.3.2",
        "eslint-plugin-standard": "2.0.1",
        "istanbul": "0.4.5",
        "mocha": "2.5.3",
        "supertest": "1.1.0"
    },
    "directories": {},
    "dist": {
        "shasum": "eaba64ca5d542a311ac945f582defc336165d9f4",
        "tarball": "https://registry.npmjs.org/errorhandler/-/errorhandler-1.5.0.tgz"
    },
    "engines": {
        "node": ">= 0.8"
    },
    "files": [
        "public/",
        "LICENSE",
        "HISTORY.md",
        "index.js"
    ],
    "gitHead": "6bf441d94197219ea6e0f392cb8ccd72602ad357",
    "homepage": "https://github.com/expressjs/errorhandler",
    "license": "MIT",
    "maintainers": [
        {
            "name": "defunctzombie"
        },
        {
            "name": "dougwilson"
        },
        {
            "name": "fishrock123"
        },
        {
            "name": "jongleberry"
        },
        {
            "name": "mscdex"
        },
        {
            "name": "tjholowaychuk"
        }
    ],
    "name": "errorhandler",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git+https://github.com/expressjs/errorhandler.git"
    },
    "scripts": {
        "lint": "eslint .",
        "test": "mocha --reporter spec --bail --check-leaks test/",
        "test-cov": "istanbul cover node_modules/mocha/bin/_mocha -- --reporter dot --check-leaks test/",
        "test-travis": "istanbul cover node_modules/mocha/bin/_mocha --report lcovonly -- --reporter spec --check-leaks test/"
    },
    "version": "1.5.0",
    "bin": {}
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
