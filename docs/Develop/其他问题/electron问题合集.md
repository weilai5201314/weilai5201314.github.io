# electron问题合集

## electron在main/index.js导入自己的js文件失败,找不到module

记录一次超级无语的bug,废话不多说直接上bug展示:

```shell
App threw an error during load
Error: Cannot find module './getAuthKey'
```

接下来的是main/index.js头部展示
```shell
import { app, BrowserWindow, ipcMain, shell } from "electron";
import { join } from "path";
import { electronApp, is, optimizer } from "@electron-toolkit/utils";
import icon from "../../resources/icon.png?asset";

# 在这一行引入
const getAuthKey = require("./getAuthKey");


const { execSync } = require("child_process");
const iconv = require("iconv-lite");

```
项目是用`electron-vite`直接生成的,部分目录如下:
```shell
├───out
│   ├───main
│   │       index.js
│   ├───preload
│   │       index.js
│   └───renderer
│       
└───src
    ├───getGacha
    │       getAuthKey.js
    ├───main
    │       index.js
    ├───preload
    │       index.js
    └───renderer
        
```

然后package.json部分内容如下(这一行是关键):

```json
{
  "main": "./out/main/index.js",
  "dependencies": {
  }
}
```

- 直接说原因,electron它只认编译后生成的out目录里面的main/index.js文件
- 写在src/main/index.js里面的代码实际上只是蓝图
- 所以,实际上导入的js文件,路径应该是相对于`out/main/index.js`,而不是你原本的index.js位置
- 附上stackflow对于其他问题的解答
```json
Thanks to and Electron's expert I discovered two errors which caused that issue:

    I modified the main's path in package.json

    "main": "./src/main/main.ts" ---> "main": "./dist/main/main.js"

    because electron can understand only the compiled file     <----------重点

    I removed in package.js on

    "type": "module"

    which otherwise wuold require to change .js  to .cjs files


```