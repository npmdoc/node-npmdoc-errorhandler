# api documentation for  [errorhandler (v1.5.0)](https://github.com/expressjs/errorhandler)  [![npm package](https://img.shields.io/npm/v/npmdoc-errorhandler.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-errorhandler) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-errorhandler.svg)](https://travis-ci.org/npmdoc/node-npmdoc-errorhandler)
#### Development-only error handler middleware

[![NPM](https://nodei.co/npm/errorhandler.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/errorhandler)

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
    "version": "1.5.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module errorhandler](#apidoc.module.errorhandler)
1.  [function <span class="apidocSignatureSpan"></span>errorhandler (options)](#apidoc.element.errorhandler.errorhandler)
1.  [function <span class="apidocSignatureSpan">errorhandler.</span>toString ()](#apidoc.element.errorhandler.toString)
1.  string <span class="apidocSignatureSpan">errorhandler.</span>title



# <a name="apidoc.module.errorhandler"></a>[module errorhandler](#apidoc.module.errorhandler)

#### <a name="apidoc.element.errorhandler.errorhandler"></a>[function <span class="apidocSignatureSpan"></span>errorhandler (options)](#apidoc.element.errorhandler.errorhandler)
- description and source-code
```javascript
function errorHandler(options) {
  // get environment
  var env = process.env.NODE_ENV || 'development'

  // get options
  var opts = options || {}

  // get log option
  var log = opts.log === undefined
    ? env !== 'test'
    : opts.log

  if (typeof log !== 'function' && typeof log !== 'boolean') {
    throw new TypeError('option log must be function or boolean')
  }

  // default logging using console.error
  if (log === true) {
    log = logerror
  }

  return function errorHandler (err, req, res, next) {
    // respect err.statusCode
    if (err.statusCode) {
      res.statusCode = err.statusCode
    }

    // respect err.status
    if (err.status) {
      res.statusCode = err.status
    }

    // default status code to 500
    if (res.statusCode < 400) {
      res.statusCode = 500
    }

    // log the error
    var str = stringify(err)
    if (log) {
      defer(log, err, str, req, res)
    }

    // cannot actually respond
    if (res._header) {
      return req.socket.destroy()
    }

    // negotiate
    var accept = accepts(req)
    var type = accept.type('html', 'json', 'text')

    // Security header for content sniffing
    res.setHeader('X-Content-Type-Options', 'nosniff')

    // html
    if (type === 'html') {
      var isInspect = !err.stack && String(err) === toString.call(err)
      var errorHtml = !isInspect
        ? escapeHtmlBlock(str.split('\n', 1)[0] || 'Error')
        : 'Error'
      var stack = !isInspect
        ? String(str).split('\n').slice(1)
        : [str]
      var stackHtml = stack
        .map(function (v) { return '<li>' + escapeHtmlBlock(v) + '</li>' })
        .join('')
      var body = TEMPLATE
        .replace('{style}', STYLESHEET)
        .replace('{stack}', stackHtml)
        .replace('{title}', escapeHtml(exports.title))
        .replace('{statusCode}', res.statusCode)
        .replace(/\{error\}/g, errorHtml)
      res.setHeader('Content-Type', 'text/html; charset=utf-8')
      res.end(body)
    // json
    } else if (type === 'json') {
      var error = { message: err.message, stack: err.stack }
      for (var prop in err) error[prop] = err[prop]
      var json = JSON.stringify({ error: error }, null, 2)
      res.setHeader('Content-Type', 'application/json; charset=utf-8')
      res.end(json)
    // plain text
    } else {
      res.setHeader('Content-Type', 'text/plain; charset=utf-8')
      res.end(str)
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.errorhandler.toString"></a>[function <span class="apidocSignatureSpan">errorhandler.</span>toString ()](#apidoc.element.errorhandler.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
