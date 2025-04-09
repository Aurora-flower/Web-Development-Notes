# Git 配置

## 前言

---

### 查看当前配置项

```shell
# 查看整体配置
git config --list

# 查看具体配置项
git cofig [options]
```



### 配置用户信息

```shell
# 用户名
git config --global user.name "[Name]"

# 邮箱地址
git config --global user.email "[Email]"
```

## Meld 合并工具

Meld 可以提供一个直观的界面来合并代码。

```shell
git config --global merge.tool meld
```

### rebase 设置

```shell
git config pull.rebase true
```


### 换行符设置

```shell
# 提交时转换为 LF，检出时转换为 CRLF
git config --global core.autocrlf true

# 提交时转换为 LF，检出时不转换
git config --global core.autocrlf input

# 提交检出均不转换
git config --global core.autocrlf false
```
