
# Dify 胜算云插件使用指南

> Dify 胜算云插件，是为Dify提供胜算云大语言模型，嵌入模型和TTS模型的开源扩展。 本文介绍如何安装、调试和使用胜算云维护的 Dify 官方插件仓库。

适用于：

* Dify Cloud
* Dify 社区版
* Dify 企业版

插件仓库：

* [shengsuan/dify-official-plugins](https://github.com/shengsuan/dify-official-plugins)

官方插件开发文档：

* [Dify Plugin Documentation](https://docs.dify.ai/en/develop-plugin/publishing/marketplace-listing/release-overview)

---

# 目录

1. 插件仓库介绍
2. 环境要求
3. 方法一：从 GitHub 安装插件（推荐）
4. 方法二：从本地集成包安装（.difypkg）
5. 方法三：下载源码进行开发调试
6. 调试插件
7. 更新插件
8. 常见问题 FAQ

---

# 一、插件仓库介绍

Dify 从 **1.0** 开始，将原来内置的：

* Model Provider
* Tool
* Extension
* Datasource
* Trigger
* Agent Strategy

全部改成插件形式。

官方插件已经迁移到独立仓库维护。

胜算云同步维护了官方插件仓库，可以直接作为 GitHub 安装源。

例如：

```
https://github.com/shengsuan/dify-official-plugins
```

---

# 二、环境要求

建议版本

| 软件     | 推荐版本 |
| ------ | ---- |
| Dify   | ≥1.0 |
| Docker | 最新   |
| Git    | 最新   |

---

# 三、方式一：GitHub 安装（推荐）

这是最方便的方法。需要先等你你的Dify 账户，在控制面板选择：

## 第一步

打开

```
集成
```

点击

```
安装
```

选择

```
GitHub
```

（这里放第一张截图）

---

## 第二步

输入仓库地址

```
https://github.com/shengsuan/dify-official-plugins
```
![选择要安装的版本](https://raw.githubusercontent.com/shengsuan/dify-official-plugins/pub/.assets/github.png)

点击

```
下一步
```
![选择要安装的版本](https://raw.githubusercontent.com/shengsuan/dify-official-plugins/pub/.assets/github2.png)
---

## 第三步

等待 Dify 拉取仓库。

拉取完成以后即可看到所有插件。

包括：

* 模型
* Tool
* Extension
* Datasource
* Trigger
* Agent Strategy

---

## 第四步

点击

```
Install
```

安装需要的插件即可。
按装后，需要先配置你的 胜算云API Key 
```
集成 > 模型供应商 > 胜算云 > 添加 API 密钥
```
![setting](https://raw.githubusercontent.com/shengsuan/dify-official-plugins/pub/.assets/setting.png)

[输入你的 API Key](https://console.shengsuanyun.com/user/keys)
配置完成后可以直接在：

* Workflow
* Chatflow
* Agent

中使用。

---

# 四、方式二：本地安装 .difypkg

如果已经下载了插件包，也可以直接导入。

例如：

```
openai.difypkg
```

进入

```
集成

↓

安装

↓

本地集成包
```

选择：

```
xxx.difypkg
```

点击安装。

官方说明支持直接上传 `.difypkg` 文件进行安装。

---

## 如何制作 .difypkg

安装 CLI

```
dify version
```

进入插件目录：

```
dify plugin package .
```

生成：

```
plugin-name.difypkg
```

然后即可分享给其他人安装。

---

# 五、方式三：下载源码调试

如果需要开发插件，建议直接 Clone 仓库。

```
git clone https://github.com/shengsuan/dify-official-plugins.git
```

进入插件目录：

```
extensions/

tools/

models/

datasources/
```

每个目录就是一个插件。

例如：

```
tools/

    google

    github

    jina

    ...
```

官方插件仓库中包含：

* Models
* Tools
* Datasources
* Extensions
* Triggers
* Agent Strategies 等插件源码。([GitHub][1])

---

# 六、配置开发环境

安装 Dify CLI

Mac

```
brew tap langgenius/dify

brew install dify
```

Linux / Windows

下载官方 CLI。

官方要求：

* Python 3.12
* Dify CLI([Dify Docs][3])

---

# 七、本地调试插件

进入插件目录：

```
cd tools/github
```

安装依赖：

```
uv sync
```

或者

```
pip install -r requirements.txt
```

启动调试：

```
dify plugin daemon
```

或者

```
dify plugin debug
```

根据插件类型进行远程调试。

调试完成以后：

```
dify plugin package .
```

生成新的

```
.difypkg
```

重新安装即可。[或选择现在调试](https://docs.dify.ai/zh/develop-plugin/features-and-specs/plugin-types/remote-debug-a-plugin)

![debug](https://raw.githubusercontent.com/shengsuan/dify-official-plugins/pub/.assets/debug.png)
---

# 八、插件目录结构

典型插件结构：

```
plugin/

├── manifest.yaml
├── provider.py
├── tools/
├── README.md
├── pyproject.toml
└── uv.lock
```

其中：

```
manifest.yaml
```

定义：

* 名称
* 作者
* 图标
* 权限
* 入口

---

# 九、插件更新

GitHub 安装：

点击：

```
更新
```

即可同步仓库最新版本。

本地安装：

重新生成：

```
.difypkg
```

再次上传即可。

---

# 十、常见问题

## GitHub 无法安装？

检查：

* GitHub 是否可以访问
* 仓库地址是否正确
* Dify 是否支持 GitHub 插件安装

---

## 插件没有显示？

检查：

* manifest.yaml
* 插件版本
* Dify 版本

---

## 本地安装失败？

检查：

* 是否为 `.difypkg`
* 是否打包成功
* 是否开启第三方插件签名验证（自托管默认会校验签名）

---

# 参考资料

* [胜算云插件仓库](https://github.com/shengsuan/dify-official-plugins?utm_source=chatgpt.com)
* [Dify 官方插件仓库](https://github.com/langgenius/dify-official-plugins?utm_source=chatgpt.com)
* [Dify 插件发布文档](https://docs.dify.ai/en/develop-plugin/publishing/marketplace-listing/release-overview?utm_source=chatgpt.com)
* [Dify CLI 文档](https://docs.dify.ai/en/develop-plugin/getting-started/cli?utm_source=chatgpt.com)
* [本地插件安装文档](https://docs.dify.ai/en/develop-plugin/publishing/marketplace-listing/release-by-file?utm_source=chatgpt.com)