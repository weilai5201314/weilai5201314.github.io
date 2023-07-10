# Mac使用常见问题

> 列举一些使用时候遇到的问题。

## 软件损坏，无法安装

记得替换软件名字

```shell
sudo xattr -r -d com.apple.quarantine /Applications/<xxx.app>
```

## 指纹解锁失败

非常罕见的遇到了这个问题。

![Alt text](img/mac常见问题/指纹无效.png)