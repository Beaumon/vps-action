# Get VPS 

通过 GitHub Action 白嫖国外主机。

## 使用方式

1. 注册百川-使用牧云主机管理助手

![](https://cdn.dvkunion.cn/tricker/46fd1775808c4411b8c2f1225641289f.png)

2. 点击绑定主机

![](https://cdn.dvkunion.cn/tricker/b61fa3cb6f0f4069b60c99a48be599aa.png)

3. 获取token

![](https://cdn.dvkunion.cn/tricker/09d9e9ee0809482faf54b491e42ae7d8.png)


4. 在github创建一个空的仓库，clone到本地，并创建`.github/workflows/workflow.yml`文件，写入一下参考内容：

```yml
name: example
on: [ push, pull_request ]

jobs:
  runner:
    runs-on: ubuntu-latest # 选择你想要的主机系统如：ubuntu:20.04
    steps:
      - uses: actions/checkout@v3
      - name: vps
        uses: Beaumon/vps-action@master
        with:
          token: xxxxxx  # your token,  It will be safer to use ${{ secrets.token }}, see [https://docs.github.com/actions/security-guides/encrypted-secrets] 
```

5. git push 上去代码，触发action。

6. 返回百川界面，已获取到主机。

![](https://cdn.dvkunion.cn/tricker/4f8e7c5ea2234135b6f57de12a115f30.png)

7. 后续使用时可以通过手动触发action的方式。

## 一些更有趣的玩法

一些更便捷的方式，如果需求的人多会逐步加入到demo。

+ 可以使用github action 的`on:workflow_dispatch`，通过http请求触发ci，来实现主机上线控制。
+ 也可以将token参数作为input。在每次http请求时动态带上token, 方便操作。