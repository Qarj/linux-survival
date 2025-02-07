# Node.js

## Ubuntu 24.04

Check latest script here: https://github.com/nvm-sh/nvm#installing-and-updating

```sh
sudo apt install curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

Restart bash.

```sh
nvm ls-remote --lts
nvm install 22
.
Computing checksum with sha256sum
Checksums matched!
Now using node v22.13.1 (npm v10.9.2)
Creating default alias: default -> 22 (-> v22.13.1)
```

Then add the following to the middle of `.bashrc`, also moving up the nvm code appended to the end.

```sh
nvm use 22
```

Caution - version of npm will be changed, might need to reinstall it - `NPM.md`.

Some npm packages require `build-essential` to work so install it now.

```sh
sudo apt install build-essential
```

## Windows Install - via Choco

Open up an administrator command prompt and install Chocolatey

```batch
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Install node.js

```sh
choco install nodejs --version=12.13.0
choco install nodejs --version=14.19.0
choco install nodejs-lts

or for latest

choco install nodejs
```

Current lts is `16.15.0` https://community.chocolatey.org/packages/nodejs-lts

Close command prompt and open another one. Then check the versions.

```sh
npm --version
node --version
```

Might have to reorder Windows path (check user as well as system path).

Finally, go to `NPM.md` and install the required NPM version.

## Windows Install - NVM - DO NOT USE, BUGGED!

This does not survive opening another command prompt, use the choco method.

https://github.com/coreybutler/nvm-windows

```
choco install nvm
```

From new command prompt

```
nvm list available
```

Must install specific version, do not do `nvm install 16`

```
nvm install 16.15.0
nvm use 16.15.0
```

## Debugging uncaught exceptions

```js
process.on('uncaughtException', (err) => {
    console.log('Caught uncaught exception: ', err);
    fs.writeFileSync(
        '/Users/tim.buckland/stacks/unhandled_exception.log',
        `Caught exception: ${err}\n${err.stack}`,
        'utf8',
    );
    process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
    console.log('Unhandled Rejection at:', promise, 'reason:', reason);
    fs.writeFileSync(
        '/Users/tim.buckland/stacks/unhandled_rejection.log',
        `Unhandled Rejection at: ${promise}\nReason: ${reason}`,
        'utf8',
    );
    process.exit(1);
});
```

## trap SIGINT & SIGTERM

```js
process.on('SIGINT', () => {
    console.log('SIGINT signal received.');
    process.exit(0);
});

process.on('SIGTERM', () => {
    console.log('SIGTERM signal received.');
    process.exit(0);
});
```

## Rest client extension for vscode

Install

```sh
code --install-extension humao.rest-client
```

```sh
# Get all books
GET http://localhost:3001/books HTTP/1.1
Content-Type: application/json

###

# Add new book
POST http://localhost:3001/books HTTP/1.1
Content-Type: application/json

{
  "title": "The Lord of the Rings"
}

###

# Update book by id
PUT http://localhost:3001/books/1 HTTP/1.1
Content-Type: application/json

{
  "title": "Dark rings of the lord"
}

###

# Delete book by id
DELETE http://localhost:3001/books/1 HTTP/1.1
```

## Running npm scripts in parallel

```json
    "start:dev": "cross-env NODE_ENV=development npm-run-all --parallel watch:client watch:server",
```

## Readline to go back to previous line and write over it

```js
import chalk from 'chalk';
import readline from 'readline';

// Write a line to the console
process.stdout.write('This is a line\n');

// Move the cursor up one line and to the start of the line
readline.cursorTo(process.stdout, 0, process.stdout.rows - 2);

// Clear the line the cursor is currently on
readline.clearLine(process.stdout, 0);

process.stdout.write(chalk.yellow(`...\n`));
```

With chalk you can use `\b` to go back one character and write over it. But it will not go back to the previous line.
