### FFmpeg @3.4.13


```bash
rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
```

```bash
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
```

```bash
sudo yum install https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm
```

```bash
sudo yum install ffmpeg ffmpeg-devel -y
```

```bash
ffmpeg -version
```


### gifski

```bash
yum install snapd -y
```

```bash
systemctl enable --now snapd.socket
```

```bash
snap install pngquant
```

```bash
snap install gifski
```

需要将 /var/lib/snapd/snap/bin 添加到 PATH 环境变量中 .bash_profile 文件中

```bash
gifski --version
```

