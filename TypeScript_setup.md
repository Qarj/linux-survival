# TypeScript setup

## Example of tsconfig.json

```json
{
    "compilerOptions": {
        "outDir": "./dist",
        "baseUrl": "./src",
        "module": "ESNext",
        "target": "es6",
        "moduleResolution": "node",
        "strict": true,
        "jsx": "react",
        "rootDir": ".",
        "sourceMap": false,
        "noImplicitAny": false,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "resolveJsonModule": true,
        "allowJs": true
    },
    "files": [],
    "include": ["src/**/*"],
    "exclude": ["node_modules", "**/*.test.ts*", "**/*.spec.ts", "tests/playwright"]
}
```
