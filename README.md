# namoey

> The Yeoman generators tester

Namoey runs your generator and some additional shell scripts in a sandbox to make sure your generated projects won't fail at start.

## Install

```console
npm install namoey --save
```

## Simple usage

```javascript
const namoey = require('namoey');
const generatorWebapp = require('./generators/app');

// Basic settings
const test = namoey()
              .setGenerator(generatorWebapp)
              .setPrompts({name: 'my-cool-project', description: 'awesome stuff'})
              .setOptions({coffescript: true});

// After every step this callback will be called
test.setStepCallback((err, stdout) => { ... });

// Those shell commands will be run after yeoman is done
test.setShellCommands([
  'npm install',
  'npm run build && npm run test'
]);
test.addShellCommand('echo done');

// Setting sandbox dir
test.setSandboxPath(process.cwd());

// Start the madness
test.run().then((stdout) => { ... }).catch((stdout) => { ... });
```
