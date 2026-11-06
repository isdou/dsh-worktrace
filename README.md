# Worktrace · 本机职业证据工作台

保留原版黑白画布、经历卡片、岗位对照、简历篮子和预览。**资料保存在用户本机；本插件不把资料提交到 Harness 聊天模型或远程 API。**

## 支持与安装

此版本为 **0.3.0，macOS 14 或更新版本的 Apple 芯片 Mac**，实测宿主 **DeepSeek Harness Desktop 0.2.2-rc.1**。其他平台尚未提供本地核心产物，安装会拒绝。

发布包只包含已编译的本地核心、界面运行产物、图标和说明，不包含原始 Swift/JSX 工程或 source map。本地核心是真正的 Mach-O 可执行文件，承担存储、事实校验、审核、岗位匹配、版本和导出。界面 JavaScript 仍可被检查；编译不等于保证无法逆向。

### 直接安装（推荐）

在官方 DeepSeek Harness 中打开 **插件 → 添加插件 → 安装第三方插件**，粘贴：

```text
github:isdou/dsh-worktrace#v0.3.0
```

也可从 [v0.3.0 发布页](https://github.com/isdou/dsh-worktrace/releases/tag/v0.3.0) 下载安装包，选择本地文件安装。

```bash
dsh plugin --profile desktop add github:isdou/dsh-worktrace#v0.3.0
```

### 在“发现”页搜索

启用“自定义插件索引”，打开 **发现 → 索引菜单 → 管理索引源…**，添加：

```text
https://raw.githubusercontent.com/isdou/dsh-worktrace/main/index.json
```

选择 Worktrace 插件索引，搜索 `Worktrace` 后安装。每个用户需要自行添加一次，官方没有默认统一索引。

从旧版升级后重启 Harness。此版本只提供 macOS Apple 芯片核心，其他系统会拒绝安装；仅声明实测宿主版本的兼容性。

安装后重新启动 Harness，点击聊天上方 **Worktrace**。工作台不依赖当前聊天的模型。

## 本地 AI

安装官方 Ollama，并事先下载模型：

```bash
ollama pull qwen3:4b
```

模型下载需要联网，但不含任何个人材料。安装完成后，处理材料无需互联网。用户可继续手动编辑、预览和导出，不必先下载模型。

插件会自行启动专用的本机模型进程：仅绑定回环地址，禁用云推理和云搜索，移除代理配置，并使用 macOS 网络沙箱阻止外连。它不会连接用户另行配置的云模型，也不会在模型缺失时回退云端。模型进程随工作台停用而退出。

## 使用

1. 点击“导入”，手动保存原文，或用本机模型整理成待核对卡片。
2. 核对公司、时间、行动、成果及来源，确认事实。
3. 粘贴岗位原文，逐条保留要求，由本机模型提议并由原文引用及本地词项校验约束匹配。可迁移关系保留待核对，缺乏直接证据的要求保留为缺口。
4. 将确认的经历加入简历篮子，打开原版预览，编辑个人信息，导出 Word、PDF、Markdown。
5. 在“本地 → 简历历史”导出固定版本；在恢复记录中恢复旧快照。

## 数据边界

- 默认工作区在 `~/.dsh/integrations/worktrace/Worktrace.json`，已有自定义资料文件继续使用；没有自动同步或云备份。
- 主资料与导出文件权限为 0600；目录为 0700。每次修改保留有界本地快照，并校验修订号和跨进程文件锁。
- 本版本不注册资料读取/修改 MCP 工具，不向 Harness 模型提供简历内容。内置 Skill 仅说明打开工作台，不读取资料。
- 本插件不能约束宿主中用户另外运行的其他工具、插件或主动上传行为。不要把材料粘贴到云端聊天，也不要授权其他工具读取资料文件。
- 不执行自动投递、发信或联系招聘方；内容不代表雇主验证。

## 分发与许可

原始 Worktrace 代码和美术保留权利，第三方组件依其原许可证使用，见 LICENSE 和 THIRD_PARTY_NOTICES.md。本地模型和 Ollama 需用户另行安装，不包含在本插件包中。

## English

Worktrace 0.3.0 keeps the original canvas UI and moves the workspace core into a compiled macOS arm64 executable. The plugin exposes no workspace tools to Harness models. Import and job analysis use only a dedicated, cloud-disabled, network-sandboxed local Ollama process with `qwen3:4b`; missing models fail closed. Download the model before using AI. Editing, review, resume versions, Word/PDF/Markdown export and recovery remain local. Other host plugins and user-initiated sharing are outside this plugin's control. The UI runtime remains inspectable; native compilation does not guarantee resistance to reverse engineering.
