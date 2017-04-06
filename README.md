# api documentation for  [gh-pages-deploy (v0.4.2)](https://github.com/meandavejustice/gh-pages-deploy)  [![npm package](https://img.shields.io/npm/v/npmdoc-gh-pages-deploy.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gh-pages-deploy) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gh-pages-deploy.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gh-pages-deploy)
#### deploy to gh-pages with one command

[![NPM](https://nodei.co/npm/gh-pages-deploy.png?downloads=true)](https://www.npmjs.com/package/gh-pages-deploy)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gh-pages-deploy/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gh-pages-deploy_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gh-pages-deploy/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gh-pages-deploy/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gh-pages-deploy/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "meandave"
    },
    "bin": {
        "gh-pages-deploy": "./bin/gh-pages-deploy"
    },
    "bugs": {
        "url": "https://github.com/meandavejustice/gh-pages-deploy.git"
    },
    "dependencies": {
        "chalk": "^1.1.1",
        "gasket": "^2.0.0",
        "prompt": "1.0.0",
        "require-module": "^0.1.0"
    },
    "description": "deploy to gh-pages with one command",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "2aed1887f1de9bdc6917b9dc9f3e68c86ac688a6",
        "tarball": "https://registry.npmjs.org/gh-pages-deploy/-/gh-pages-deploy-0.4.2.tgz"
    },
    "gh-pages-deploy": {
        "staticpath": "example"
    },
    "gitHead": "291fe6764b615a1ef55251a786f9d2a3f51575d1",
    "homepage": "https://github.com/meandavejustice/gh-pages-deploy",
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "meandave",
            "email": "davejustishh@gmail.com"
        }
    ],
    "name": "gh-pages-deploy",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/meandavejustice/gh-pages-deploy.git"
    },
    "scripts": {
        "deploy": "./bin/gh-pages-deploy",
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "version": "0.4.2"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gh-pages-deploy](#apidoc.module.gh-pages-deploy)
1.  [function <span class="apidocSignatureSpan">gh-pages-deploy.</span>displayCmds (cmd)](#apidoc.element.gh-pages-deploy.displayCmds)
1.  [function <span class="apidocSignatureSpan">gh-pages-deploy.</span>execBuild (buildCmd, cfg)](#apidoc.element.gh-pages-deploy.execBuild)
1.  [function <span class="apidocSignatureSpan">gh-pages-deploy.</span>getFullCmd (cfg)](#apidoc.element.gh-pages-deploy.getFullCmd)



# <a name="apidoc.module.gh-pages-deploy"></a>[module gh-pages-deploy](#apidoc.module.gh-pages-deploy)

#### <a name="apidoc.element.gh-pages-deploy.displayCmds"></a>[function <span class="apidocSignatureSpan">gh-pages-deploy.</span>displayCmds (cmd)](#apidoc.element.gh-pages-deploy.displayCmds)
- description and source-code
```javascript
function displayCmds(cmd) {
  console.log(chalk.gray('Preparing to deploy to gh-pages with these commands: \n'));
  cmd.forEach(function(script, idx) {
    if (script !== null) {
      if (idx === 0) {
        console.log(chalk.blue(' '+ script + '\n'));
      } else {
        console.log(chalk.blue(script + '\n'));
      }
    }
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gh-pages-deploy.execBuild"></a>[function <span class="apidocSignatureSpan">gh-pages-deploy.</span>execBuild (buildCmd, cfg)](#apidoc.element.gh-pages-deploy.execBuild)
- description and source-code
```javascript
function execBuild(buildCmd, cfg) {
  exec(getcurrentbranch, function (error, stdout, stderr) {
    var currentBranch = stdout;

    var pipelines = gasket({
      build: buildCmd,
      recover: prepBuild(getRecoverCmd(currentBranch))
    });
    pipelines.run('build').on('error', function(err) {
      if (!cfg.noprompt) {
        prompt.start();
        prompt.get(question, function(err,result) {
          if (result.recover.toLowerCase() === 'n') process.exit(0);
          pipelines.run('recover').pipe(process.stdout);
        });
      } else {
        pipelines.run('recover').pipe(process.stdout);
      }

    }).pipe(process.stdout)
  });
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gh-pages-deploy.getFullCmd"></a>[function <span class="apidocSignatureSpan">gh-pages-deploy.</span>getFullCmd (cfg)](#apidoc.element.gh-pages-deploy.getFullCmd)
- description and source-code
```javascript
function getFullCmd(cfg) {
  return prepBuild(getBuildCmd(getPrepCmd(cfg), getPostCmd(cfg)));
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
