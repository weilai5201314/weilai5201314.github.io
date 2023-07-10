# Linux那些事

## Linux安装中文字体

### CentOS安装中文字体

```
yum -y install fontconfig
yum -y install mkfontscale

cd /usr/share/fonts/

wget https://hub.fastgit.org/adobe-fonts/source-han-sans/raw/release/Variable/TTF/Subset/SourceHanSansCN-VF.ttf

mkfontscale && mkfontdir
```

### Ubuntu安装中文字体

```
apt install -y --force-yes --no-install-recommends fonts-wqy-microhei
```


### 重建字体缓存

```
fc-cache -fv
```



## puppeteer问题

系统是ubuntu18, 所以需要安装他列举的所有依赖

网址：<https://github.com/puppeteer/puppeteer/issues/6922>

```
sudo apt-get install ca-certificates fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgbm1 libgcc1 libglib2.0-0 libgtk-3-0 libnspr4 libnss3 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 lsb-release wget xdg-utils -y

```

如果后续还有错误

```
(node:5267) UnhandledPromiseRejectionWarning: Error: Failed to launch the browser process!
[0308/163337.932654:ERROR:zygote_host_impl_linux.cc(90)] Running as root without --no-sandbox is not supported. See https://crbug.com/638180.

```

则需要

```
const browser = await puppeteer.launch({ args: ['--no-sandbox', '--disable-setuid-sandbox'] })

```

可以正常运行, 但是官方并不推荐我们这么做.