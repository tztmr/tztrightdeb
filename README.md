# TzTRight Deb

这是 deb 源 demo

使用与刷新索引

```sh
# 生成 Packages（不需要 sudo，建议屏蔽警告）
dpkg-scanpackages -m ./debs > Packages 2>/dev/null

# 生成压缩索引
gzip -c Packages > Packages.gz
bzip2 -c Packages > Packages.bz2
# 可选：生成 xz 索引
xz -c Packages > Packages.xz
```

验证

```sh
wc -l Packages
gzip -t Packages.gz
bzip2 -t Packages.bz2
```

常见警告

- tar: Ignoring unknown extended header keyword 'LIBARCHIVE.xattr.com.apple.provenance'
- 产生原因：macOS 的 libarchive 读取 .deb 内部 tar 的扩展属性
- 影响：对索引与安装无影响，可忽略
- 规避：制作 .deb 或 tar 时设置环境变量 COPYFILE_DISABLE=1，或使用 GNU tar (gtar)

托管

- 将 Packages、Packages.gz（以及可选 Packages.bz2）放到源根目录
- 可选提供 Release 文件以增强客户端兼容性
