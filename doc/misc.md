[HTML5 Boilerplate homepage](http://html5boilerplate.com) | [Documentation table of contents](README.md)

# 杂项

## .gitignore

HTML5 Boilerplate 中包含了一个项目文件 `.gitignore`，该文件主要用来忽略文档或者目录，将其排除在版本控制外。针对不同的开发环境，忽略项也不同。

与操作系统以及编辑器相关的文档可以通过使用 "global 
ignore" 来指定忽略。

举例来说，如果你想将 HOME 目录下的文件以及子目录加入全局忽略 globally ignore ，可以增加以下代码到你的 `~/.gitconfig` 中：

```gitignore
[core]
    excludesfile = ~/.gitignore
```

* 更多关于全局忽略 (global ignores) 的信息： http://help.github.com/ignore-files/
* 更多忽略 (ignores) 配置： https://github.com/github/gitignore
