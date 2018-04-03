### 1.下载ffmpeg
[下载地址](https://ffmpeg.org/download.html#build-linux)

### 2.解压

把下载的包先复制到`/usr/local`目录下，再解压
```
$ sudo cp Downloads/ffmpeg-3.3.3.tar.bz2 /usr/local
$ sudo tar -jxvf ffmpeg-3.3.3.tar.bz2
```

### 3.进入解压后的目录
`$ cd ffmpeg-3.3.3`

### 4.安装yasm
`$ sudo apt-get install yasm`

### 5.执行
`$ sudo ./configure --enable-shared --prefix=/usr/local`

### 6.编译（时间较长）
```
$ sudo make -j8
$ sudo make install
```

### 7.修改文件/etc/ld.so.conf 内容
`$ sudo vim /etc/ld.so.conf`

在include ld.so.conf.d/*.conf后追加

`$ /usr/local/lib/`

### 8.使修改生效
`$ sudo ldconfig`

### 9.配置环境变量
```
export PATH=/usr/local/bin/:$PATH
env
```
