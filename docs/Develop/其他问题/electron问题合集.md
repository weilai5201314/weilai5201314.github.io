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

- 但是这只是问题其一,不是真正的问题所在
- 真正的解决办法是,使用es引入,而不是commondjs方式引入
- 在electron里要注意这两种代码格式

```javascript
// 正确的
export function getAuthKey() {}
import { getAuthKey } from './getAuthKey'

// 错误的
module.exports = { getAuthKey };
const {getAuthKey} = require('./getAuthKey');
```

- 如果不看代码格式,单从代码本身的对错来说,这两种写法都是没错的,甚至在nodejs里平时用的更多的是commonjs方法
- 在写代码之前最好还是看看使用的框架或者环境的代码格式
- 最后将引入改为 import 之后,代码运行无误