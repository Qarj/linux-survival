# NPM Command line options

https://docs.npmjs.com/cli-documentation/

## Install a package globally

```
npm --global install yarn
```

## Save a package in `package.json`as a dependency

```
npm install underscore
```

Normal dependencies are required for runtime.

## Save a package in `package.json` as a dev dependency

```
npm install --save-dev jest-puppeteer puppeteer jest
```

Dev dependencies are not required for runtime.

## nodemon
```
npm --global install nodemon
```
Start program with nodemon instead of mode and changes will be automatically applied.

## Publish app
```
npm login
```

```
npm publish
```

```
npm major|minor|patch
```

## link

Windows
```
type NUL > .npmignore
```

```
npm cache verify
```

In sub package called `wonder-lib`
```
npm link
```

In master package `bloggy`
```
npm link ../wonder-lib
```

## view

See repository connected to
```
npm view connect
```

Sample output
```
connect@3.7.0 | MIT | deps: 4 | versions: 234
High performance middleware framework
https://github.com/senchalabs/connect#readme

keywords: framework, web, middleware, connect, rack

dist
.tarball: https://registry.npmjs.org/connect/-/connect-3.7.0.tgz
.shasum: 5d49348910caa5e07a01800b030d0c35f20484f8
.integrity: sha512-ZqRXc+tZukToSNmh5C2iWMSoV3X1YUcPbqEM4DkEG5tNQXrQUZCNVGGv3IuicnkMtPfGf3Xtp8WCXs295iQ1pQ==
.unpackedSize: 95.2 kB

dependencies:
debug: 2.6.9        finalhandler: 1.1.2 parseurl: ~1.3.3    utils-merge: 1.0.1

maintainers:
- dougwilson <doug@somethingdoug.com>
- tjholowaychuk <tj@vision-media.ca>

dist-tags:
1.8: 1.9.0     latest: 3.7.0

published a month ago by dougwilson <doug@somethingdoug.com>
```