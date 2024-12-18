# CentOS 7.9 环境配置指南

## 更新YUM源

更新YUM源：

```bash
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/ChangeMirrors.sh)
```

## 安装NVM和Node.js

1. 安装NVM：

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
    source ~/.bashrc
    ```

2. 安装Node.js：

    ```bash
    nvm install 18
    nvm use 18
    ```

    如果输入`node -v`报错，可能是因为Node.js 18需要更高版本的GLIBC和GCC。

## 升级GCC到9.5.0

1. 下载GCC 9.5.0：

    [GCC 9.5.0 下载链接](https://ftp.gnu.org/gnu/gcc/gcc-9.5.0/gcc-9.5.0.tar.xz)

2. 解压并安装：

    ```bash
    tar -Jxvf gcc-9.5.0.tar.xz
    cd gcc-9.5.0
    yum install -y gmp-devel mpfr-devel libmpc-devel gcc gcc-c++ gcc-gfortran.x86_64 make
    ./configure --prefix=/usr --disable-multilib --enable-languages=c,c++,fortran
    make -j 8
    yum remove gcc -y
    make install
    gcc -v  # 显示9.5.0表示成功
    ```

## 升级Make到4.3

1. 下载Make 4.3：

    ```bash
    wget https://ftp.gnu.org/gnu/make/make-4.3.tar.gz
    ```

2. 解压并安装：

    ```bash
    tar zxvf make-4.3.tar.gz
    cd make-4.3
    ./configure --prefix=/usr/local/make4.3
    make && make install
    ln -s -f /usr/local/make4.3/bin/make /usr/bin/make
    ```

## 升级GLIBC到2.31

1. 查看当前版本：

    ```bash
    ldd --version
    ```

2. 下载GLIBC 2.31：

    [GLIBC 2.31 下载链接](https://ftp.gnu.org/gnu/glibc/glibc-2.31.tar.xz)

3. 解压并安装：

    ```bash
    tar -Jxvf glibc-2.31.tar.xz
    cd glibc-2.31
    mkdir build && cd build
    ../configure --prefix=/usr --disable-profile --enable-add-ons --enable-obsolete-nsl --with-headers=/usr/include --with-binutils=/usr/bin --disable-sanity-checks --disable-werror
    make -j 8
    make install
    ```

    完成后，`node -v`不再报错。

## 安装Nginx

```bash
yum install nginx -y
nginx -t
```

## 配置NPM

设置NPM镜像源：

```bash
npm config set registry https://registry.npmmirror.com
```

## 安装Yarn

```bash
npm install -g yarn
```

## 安装PM2

1. 安装PM2：

    ```bash
    npm install pm2 -g
    ```

2. 启动应用：

    ```bash
    pm2 start index.js
    ```

## 待安装软件

- MySQL
- Redis
- FFmpeg
