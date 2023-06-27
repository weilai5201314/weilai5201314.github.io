
# conda command

[toc]

## 创建、查看、删除环境
```
create $    conda create -n <name> python=x.x
check  $    conda env list 
delete $    conda remove -n <name> --all
```
- 在`create`中，可以在名字后面添加python的指定版本

## *基础管理命令*

### 1.查看版本信息

**查看当前版本**

```
conda --version
conda -V
```

**更新到当前版本**
  
`conda update conda`




### 2.管理环境

#### **2.1创建一个新环境**

`conda create --name <xxx>`

#### **2.2使用或激活新环境**

`conda activate <xxx>`

#### **2.3查看所有环境列表**

`conda info --envs`

#### **2.4将当前环境改为默认环境（base）**

`conda activate`





### 3.管理Python

#### **3.1创建新环境并包含自定义Python版本**

- 创建一个名为“蛇”的新环境，其中包含Python 3.9

 `conda create --name snakes python=3.9`
 
#### **3.2验证当前环境Python的版本**

`python --version`

#### **3.3停用当前环境，返回默认环境**

`conda activate`





### 4.管理软件包

#### **4.1激活要搜索的环境**

`conda activate <xxx>`

#### **4.2搜索软件包**

- 检查您尚未安装的名为“beautifulsoup4”的软件包是否可以从Anaconda存储库中获取

`conda search beautifulsoup4`

#### **4.3安装到当前环境**

`conda install beautifulsoup4`

#### **4.4检查是否安装**

`conda list`

#### **4.5搜索当前环境中某个特定包**

`conda list <xxx>`




## *命令参考*

### 基础命令

#### **1.查看所有帮助**

```
conda --help
conda install --helo
```

#### **2.conda clean**
 **删除未使用的软件包和缓存**



- -a,--all

删除索引缓存、锁定文件、未使用的缓存包和tarballs.

- -i,--index-cache

删除索引缓存。

- -p,--pachages

从可写包缓存中删除未使用的软件包。警告：这不会检查使用符号链接安装到软件包缓存的软件包。

- -t,--tarballs

删除缓存包裹，压缩包。


#### **3.conda cpmoare**

#### **4.conda config**

#### **5.conda create**

#### **6.conda info**

#### **7.conda install**

#### **8.conda list**

#### **9.conda package**

#### **10.conda remove**

#### **11.conda run**

#### **12.conda search**

#### **13.conda update**

### Conda vs.pip vs.virtualenv







