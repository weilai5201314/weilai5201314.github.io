# mac连接数据库.clion(转载)

## 1.添加头文件

需要头文件

```c
#include <mysql.h>
```

头文件位置要添加到cmakelist.txt中

```c
include_directories("/usr/local/mysql-8.0.17-macos10.14-x86_64/include")
link_directories("/usr/local/mysql-8.0.17-macos10.14-x86_64/lib")
 
add_executable(experiment main.c)
 
target_link_libraries(experiment libmysqlclient.dylib)


```

- 需要根据自己电脑的mysql版本改写路径。

- 第一行加入的是include的目录，这个目录在mac上搜索mysql.h(首先你电脑上安装了mysql)

- 第二行的lib和include在同一级目录下

  最后一行必须在第三行之后



## 2.连接数据库

步骤： 

1. 安装MySQL数据库 
2. 项目属性页->C/C++->常规->附加包含目录：xxx\mysql Server 5.6\include 
3. 项目属性页->链接器->常规->附加库目录：xxx\MySQL Server 5.6\lib 
4. 项目属性页->链接器->输入->附加依赖项：libmysql.lib 将libmysql.dll拷贝到项目中 
5. 引入[头文件](https://so.csdn.net/so/search?q=头文件&spm=1001.2101.3001.7020):`#include<Windows.h> #include <mysql.h>` 
      测试代码：

```c
#include<iostream>
#include<Windows.h>
#include <mysql.h>
#include<string>


using namespace std;


int main()
{

    //必备的一个数据结构
    MYSQL mydata;

    //初始化数据库
    if (0 == mysql_library_init(0, NULL, NULL)) {
        cout << "mysql_library_init() succeed" << endl;
    }
    else {
        cout << "mysql_library_init() failed" << endl;
        return -1;
    }

    //初始化数据结构
    if (NULL != mysql_init(&mydata)) {
        cout << "mysql_init() succeed" << endl;
    }
    else {
        cout << "mysql_init() failed" << endl;
        return -1;
    }

    //在连接数据库之前，设置额外的连接选项
    //可以设置的选项很多，这里设置字符集，否则无法处理中文
    if (0 == mysql_options(&mydata, MYSQL_SET_CHARSET_NAME, "gbk")) {
        cout << "mysql_options() succeed" << endl;
    }
    else {
        cout << "mysql_options() failed" << endl;
        return -1;
    }

    //连接数据库
    if (NULL
        != mysql_real_connect(&mydata, "localhost", "root", "root", "test",
            3306, NULL, 0))
        //这里的地址，用户名，密码，端口可以根据自己本地的情况更改
    {
        cout << "mysql_real_connect() succeed" << endl;
    }
    else {
        cout << "mysql_real_connect() failed" << endl;
        return -1;
    }

    //sql字符串
    string sqlstr;

    //创建一个表
    sqlstr = "CREATE TABLE IF NOT EXISTS `new_paper` (";
    sqlstr += " `NewID` int(11) NOT NULL AUTO_INCREMENT,";

    sqlstr += " `NewCaption` varchar(40) NOT NULL,";

    sqlstr += " `NewContent` text,";

    sqlstr += " `NewTime` datetime DEFAULT NULL,";

    sqlstr += " PRIMARY KEY(`NewID`)";

    sqlstr += " ) ENGINE = InnoDB DEFAULT CHARSET = utf8";


    if (0 == mysql_query(&mydata, sqlstr.c_str())) {
        cout << "mysql_query() create table succeed" << endl;
    }
    else {
        cout << "mysql_query() create table failed" << endl;
        mysql_close(&mydata);
        return -1;
    }


    //向表中插入数据
    for (int i = 0;i < 100;i++)
    {
        sqlstr =
            "INSERT INTO `test`.`new_paper` (`NewID`, `NewCaption`, `NewContent`, `NewTime`) ";
        sqlstr += "VALUES (default, '组织者', '方提出更换存放骨灰存放', '2015-09-01 14:29:51');";
        if (0 == mysql_query(&mydata, sqlstr.c_str())) {
            cout << "mysql_query() insert data succeed" << endl;
        }
        else {
            cout << "mysql_query() insert data failed" << endl;
            mysql_close(&mydata);
            return -1;
        }
    }

    //显示刚才插入的数据
    sqlstr = "SELECT `NewID`,`NewCaption`,`NewContent`,`NewTime` FROM `test`.`new_paper`";
    MYSQL_RES *result = NULL;
    if (0 == mysql_query(&mydata, sqlstr.c_str())) {
        cout << "mysql_query() select data succeed" << endl;

        //一次性取得数据集
        result = mysql_store_result(&mydata);
        //取得并打印行数
        int rowcount = mysql_num_rows(result);
        cout << "row count: " << rowcount << endl;

        //取得并打印各字段的名称
        unsigned int fieldcount = mysql_num_fields(result);
        MYSQL_FIELD *field = NULL;
        for (unsigned int i = 0; i < fieldcount; i++) {
            field = mysql_fetch_field_direct(result, i);
            cout << field->name << "\t\t";
        }
        cout << endl;

        //打印各行
        MYSQL_ROW row = NULL;
        row = mysql_fetch_row(result);
        while (NULL != row) {
            for (int i = 0; i < fieldcount; i++) {
                cout << row[i] << "\t\t";
            }
            cout << endl;
            row = mysql_fetch_row(result);
        }

    }
    else {
        cout << "mysql_query() select data failed" << endl;
        mysql_close(&mydata);
        return -1;
    }


    //删除刚才建的表
    sqlstr = "DROP TABLE `test`.`new_paper`";
    if (0 == mysql_query(&mydata, sqlstr.c_str())) {
        cout << "mysql_query() drop table succeed" << endl;
    }
    else {
        cout << "mysql_query() drop table failed" << endl;
        mysql_close(&mydata);
        return -1;
    }
    mysql_free_result(result);
    mysql_close(&mydata);
    mysql_server_end();

    system("pause");
    return 0;
}
```

