# TypeScript

```sh
npm install -g typescript
tsc -v
.
Version 4.7.3
```

```sh
tsc index.ts
```

```sh
tsc --init
.
Created a new tsconfig.json with:
                                                                                                                     TS
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true


You can learn more at https://aka.ms/tsconfig
```

In tsconfig.json, you can remove target and hit `CTRL+SPACE` to see the available options

```sh
    "target": "ES2016",
```

Suggested config

```json
{
    "compilerOptions": {
        "target": "ES2016",
        "module": "commonjs",
        "rootDir": "./src",
        "outDir": "./dist",
        "removeComments": true,
        "noEmitOnError": true,
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "strict": true,
        "skipLibCheck": true
    }
}
```

Once setup, it is possible to compile the code with just `tsc`.

## Debugger

Set debug points.

Click Run and Debug icon on LHS.

Create a launch.json file selecting node.js as the runtime.

Add a preLaunchTask as follows

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "pwa-node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": ["<node_internals>/**"],
            "program": "${workspaceFolder}/src/index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": ["${workspaceFolder}/**/*.js"]
        }
    ]
}
```

Press `Launch Program` or `F5` to start debugging.
