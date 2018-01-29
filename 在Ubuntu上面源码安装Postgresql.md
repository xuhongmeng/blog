## Ubuntu安装Postgresql数据库

---
版本：
Ubuntu：16.04
PostgreSQL：10

----

### 下载源码
1. 版本的源码下载[地址](https://www.postgresql.org/download/)
1. git方式下载的地址:如果采用这个方式下载，要切换到要安装的版本。
    ```
    git://git.postgresql.org/git/postgresql.git
    ```

### 安装到本用户(xhm)
1. 安装编译过程需要的依赖库，按照经验，需要安装如下的库
    ```
    sudo apt-get install bison zlib1g-dev libreadline6-dev libssl-dev libpam0g-dev libxml2-dev libxslt-dev libperl-dev libpython-dev flex bison
    ```
1. 生成Makefile,按照如下的方式配置
    ```
    ./configure --prefix=/home/xhm/pghome --with-pgport=5432  --with-perl --with-python --with-openssl --with-pam --without-ldap --with-libxml --with-libxslt --enable-thread-safety  
    ```
1. 配置PYTHON的环境变量, (可选,Python进行存储过程进行数据分析)
    ```
    eg: export PYTHON = /usr/bin/python3
    ```
    >参考资料: 官方文档 9.4  -> 43.1 python2 vs python3
    ``` 
    编译变量取决于在安装期间发现了哪个Python版本或使用PYTHON 环境变量明确设置了哪个版本，参见第 15.4 节。 要在一个安装中可用PL/Python的两个变量， 必须配置源代码树并编译两次。
    ```
1. make -j4

1. make install

### 初始化群集（也叫实例）
1. 使用initdb生成一个新的实例。主要pgdata的目录，输入要设置的密码
    ```
    initdb -D /database/pgdata -E UTF8 --locale=C -U postgres –W 初始化数据库实例
    ```
1. 设置环境变量，可以在如下的文件
    > ~/.bashrc  /etc/profile
    ```
    export PGPORT=5432
    export PGHOME=/home/xhm/pghome
    export PGDATA=/database/pgdata
    export PATH=$PGHOME/bin:$PATH
    export MANPATH=$PGHOME/share/man:$MANPATH
    export LANG=en_US.utf8
    export DATE=`date +"%Y-%m-%d %H:%M:%S"`
    export LD_LIBRARY_PATH=$PGHOME/lib:$LD_LIBRARY_PATH
    alias pg_stop='pg_ctl -D $PGDATA stop -m fast'   #这里是单引号
    alias pg_start='pg_ctl -D $PGDATA start'
    alias pg_reload='pg_ctl -D $PGDATA reload'
    ```

### 运行
1. pg_start
    > 实际上是运行了 pg_ctrl -D $PGDATA start

### 登录
    psql -U postgres