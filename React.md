# React

## Set up dev environment - Mosh React course

```
npm i -g create-react-app@1.5.2
```

VS Code extension by Burke Holland

```
Simple React Snippets
```

VS Code extension by Esben Petersen

```
Prettier - Code formatter

File -> Preferences -> Settings | CTRL ,

Text Editor -> Formatting -> check Format On Save
```

VS Code extension by Sergey Korenuk

```
Auto Import - ES6, TS, JSX, TSX
```

Chrome extension

```
React Developer Tools
```

Yarn

```
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update
sudo apt install --no-install-recommends yarn
```

Note: removing `--no-install-recommends` will install node js also.

## Clear an input field in react / next.js

```tsx
import { useRef } from 'react';

const inputRef = useRef(null);
const onCrossClick = () => {
    // @ts-ignore
    inputRef.current.value = '';
};

return (
    <div>
        <div className="item input-container">
            <span>🔍</span>
            <input
                className="input-jobtitle"
                type="text"
                placeholder="Search job title/skill"
                ref={inputRef}
                onChange={(e) => {
                    send({
                        type: 'Job title changed',
                        value: e.target.value,
                    });
                }}
            ></input>
            <span onClick={onCrossClick} className="cross">
                ❌
            </span>
        </div>
    </div>
);
```
