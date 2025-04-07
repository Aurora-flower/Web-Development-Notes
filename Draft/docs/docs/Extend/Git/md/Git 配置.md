# Git 配置

## 前言

---

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
