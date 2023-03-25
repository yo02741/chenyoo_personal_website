---
title: 透過 ESLint 與 Prettier 規範團隊合作的專案
date: 2023-03-25 22:59:48
tags:
---


> 每個工程師都有自己的 Coding Style，不同的語言也有建議的 Coding Style。
> 
> 當專案為團隊合作開發時，建議事先擬定團隊的規範。
> 
> 那通常會使用 Linter 來進行程式碼品質的規範，並使用 Formatter 規範程式碼風格。


- Linter 使用 `ESLint` 規範程式碼品質
- Formatter 使用 `Prettier` 規範程式碼風格

<!--more-->

### Install VSCode extensions
- ESLint
> ![](https://i.imgur.com/WEhJUbQ.png)

- Prettier
> ![](https://i.imgur.com/Pzv5ARc.png)

### IDE Settings

> File > Preferences > Settings > Workspace

請將設定改在 Workspace 內，單獨的為此專案進行設定 ; 反之，若改在 User 則會影響每個 Project。


> ![](https://i.imgur.com/0pmyf78.png)

> ![](https://i.imgur.com/psPmq0h.png)

> ![](https://i.imgur.com/Fzf30i5.png)

設定完之後，會多一個檔案如下:
```json
// .vscode/settings.json

{
    "editor.tabSize": 2,
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

之後再補上針對 `.js`、`.json` 副檔名也預設使用 prettier
```json
// .vscode/settings.json

{
    "editor.tabSize": 2,
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[json]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    }
}
```
之後就可以在 `.js`、`.json` 文件中，點擊右鍵 > `Format Document With ...`，就可以看到預設的 formatter 是 prettier 了！

![](https://i.imgur.com/qW1MFAz.png)


### ESLint Settings

查看 `package.json` 中 `eslintConfig` 的 `extends` 

```json
// package.json


"extends": [
    "plugin:vue/recommended", // 這邊將 essential 改成 recommended
    "eslint:recommended",
    "@vue/prettier"
]
```
> https://eslint.vuejs.org/rules/


### Prettier Settings

查看 `package.json` 中 `prettier`

```json
// package.json


"prettier": {
    "trailingComma": "es5", // 尾隨逗號
    "tabWidth": 2, // 縮排
    "semi": true, // 結束是否加分號
    "singleQuote": false // 使用單引號
}
```

> https://prettier.io/

