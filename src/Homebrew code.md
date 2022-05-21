# Brew
[toc]
## 安装
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
## 卸载
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
(下载卸载脚本并运行 /bin/bash uninstall.sh --help 查看更多卸载选项。)


## 1.信息查询
### 查看 Homebrew 版本
➜  ~ brew -v
###  列出已安装的软件
➜  ~ brew list
### 使用浏览器打开 brew 官网
➜  ~ brew home
### 查看包的详细信息
➜  ~ brew info 包名
### 检测系统中与brew 有关的潜在问题
➜  ~ brew doctor
### 查看包的所有版本
➜  ~ brew list --versions | grep 包名
### 以树形展示所有已安装包的依赖
➜  ~ brew deps --installed --tree

## 2.查找包
➜  ~ brew search git
➜  ~ brew search /^git$/

## 3.安装包
➜  ~ brew install 包名

## 4.卸载
➜  ~ brew uninstall 包名

## 5.自身更新
➜  ~ brew update

## 6.更新包
### 查看哪些包有新版本可更新
➜  ~ brew outdated
### 更新所有包
➜  ~ brew upgrade
### 更新指定包
➜  ~ brew upgrade 包名

## 7.清理旧包
⚠️ 注意：如果一个包当前有可更新的版本没有更新，执行清理时候只会提示一个警告，而不会执行清理操作。
⚠️ 需要先升级到最新版本，值执行清理。 
### 查看哪些包可清理
➜  ~ brew cleanup -n
### 清理所有
➜  ~ brew cleanup
### 清理指定包
➜  ~ brew cleanup 包名

## 8.锁定不想更新的包
### 锁定
➜  ~ brew pin 包名
### 解锁
➜  ~ brew unpin 包名

## 9.关联包
### 清理无效的关联，且清理与之相关的位于/Applications和~/Applications中的无用App链接
➜  ~ brew prune
### 将指定软件的安装文件symlink到Homebrew上
➜  ~ brew link 包名




## 其他指令
 brew help
Example usage:
  brew search TEXT|/REGEX/
  brew info [FORMULA|CASK...]
  brew install FORMULA|CASK...
  brew update
  brew upgrade [FORMULA|CASK...]
  brew uninstall FORMULA|CASK...
  brew list [FORMULA|CASK...]

Troubleshooting:
  brew config
  brew doctor
  brew install --verbose --debug FORMULA|CASK

Contributing:
  brew create URL [--no-fetch]
  brew edit [FORMULA|CASK...]

Further help:
  brew commands
  brew help [COMMAND]
  man brew
  https://docs.brew.sh