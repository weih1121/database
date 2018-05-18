### redis安装

Redis项目不正式支持Windows。 但是，Microsoft开放技术小组开发和维护这个Windows端口针对Win64

下载链接：[redis下载地址](https://github.com/MSOpenTech/redis/releases)

# [3.2.100](https://github.com/MicrosoftArchive/redis/releases/tag/win-3.2.100)

![@enricogior](https://avatars0.githubusercontent.com/u/3206696?s=40&v=4) [enricogior](https://github.com/enricogior) released this Jul 1, 2016 · [1208 commits](https://github.com/MicrosoftArchive/redis/compare/win-3.2.100...3.0) to 3.0 since this release

## Assets

- [5.8 MB **Redis-x64-3.2.100.msi**](https://github.com/MicrosoftArchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.msi)
- [4.98 MB **Redis-x64-3.2.100.zip**](https://github.com/MicrosoftArchive/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.zip)
- [ **Source code** (zip)](https://github.com/MicrosoftArchive/redis/archive/win-3.2.100.zip)
- [ **Source code** (tar.gz)](https://github.com/MicrosoftArchive/redis/archive/win-3.2.100.tar.gz)

This is the first release of Redis on Windows 3.2.

This release is based on antirez/redis/3.2.1 plus some Windows specific fixes. It has passed all the standard tests but it hasn't been tested in a production environment.

Therefore, **before considering using this release in production, make sure to test it thoroughly in your own test environment.**

See the [release notes](https://github.com/MSOpenTech/redis/blob/win-3.2.100/Redis%20on%20Windows%20Release%20Notes.md) for details.

点击下载安装即可。

启动服务:

```powershell
.\redis-server.exe redis.windows.conf
```

安装服务项方便启动：

```powershell
.\redis-server.exe --service-install redis.windows-service.conf --loglevel verbose	#【在window服务里就能看到这个服务了】
```

*服务启动：*

```powershell
.\redis-server --service-start
```

*服务测试*:

```powershell
.\redis-cli.exe -h 127.0.0.1 -p 6379
```

### 其他命令

卸载服务:

```powershell
redis-server --service-uninstall
```

开启服务:

```powershell
redis-server --service-start
```

停止服务:

```powershell
redis-server --service-stop
```

---

windows上redis添加个人密码

打开项目路径，例如C:\Program Files\Redis

打开redis.windows.conf文件将第386行， #号去掉，将foobared改为自己喜欢的密码，例如root

```python
# requirepass foobared
```

验证密码是否修改成功

```powershell
redis-cli.exe -h 127.0.0.1 -p 6379 -a root
```



