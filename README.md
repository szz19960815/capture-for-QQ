## 前言
聊天软件需要截图功能。我们找到了一个方法，QQ dll，包装一下生成 exe 文件，我用 Node.js 去调用完成截图。

1. 第一步先用 Node 执行微信封装的 exe，然后会把截图复制到剪切板
2. 然后调用浏览把剪切板的内容复制出来
```
    var screen_window = execFile(__dirname + '/screen/PrintScr.exe')
    screen_window.on('exit', function (code) {
      // 执行成功返回 1，返回 0 没有截图
      if (code) mainWindow.webContents.paste()
    })
```

```
electron出现打包后没有正常调用或者返回正常结果的情况下,查看是否是在electron打包后也对该exe进行了二次打包,针对这个情况我的做法是放到static目录下,使用__static路径访问,避免打包,当然也可以使用process.cwd()判断工作区,然后拼接打包后的目录
```
