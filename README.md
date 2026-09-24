# 中秋古风诗意海报生成器

创作与发布署名：**小小小书创作**。本仓库按 [MIT 许可证](LICENSE) 开放，保留版权与许可声明即可复制、修改和再分发。

给 Codex / ChatGPT Work 使用的中秋主题 Skill 与 Plugin 源码。输入“月满”“桂香”“归雁”等短词，就能得到同一视觉体系下的竖版海报、书签、可复制提示词或可编辑文字方案。

本仓库已包含 Plugin 清单和 Marketplace 清单。GitHub 地址：[wxf266629-hub/mid-autumn-poetic-poster-plugin](https://github.com/wxf266629-hub/mid-autumn-poetic-poster-plugin)。这个 GitHub 仓库并不等于 OpenAI 公共插件目录上架。

## 先看结果在哪里

```text
mid-autumn-poetic-poster-plugin/
├── README.md                         本指南
├── LICENSE                           MIT 开源许可
├── .agents/plugins/marketplace.json  仓库内插件目录
└── plugins/mid-autumn-poetic-poster/
    ├── plugin.json                   通用 Plugin 清单
    ├── .codex-plugin/plugin.json     Codex 兼容清单及展示文案
    └── skills/mid-autumn-poetic-poster/
        ├── SKILL.md                  核心生成规则
        ├── agents/openai.yaml        Skill 在界面中的名称与示例问法
        └── references/
            ├── theme-library.md     八个主题与示例
            ├── poetry-library.md    经原作核对的诗词候选
            ├── user-requests.md     用户常见问法
            ├── prompt-template.md   可复制的图像提示词
            ├── series-and-print.md  系列统一与书签印刷
            └── quality-checklist.md 成图检查与修正
```

只有 `SKILL.md` 是 Skill 的硬性必需文件；这里的参考文件负责让结果稳定。不要只上传 `SKILL.md` 而遗漏 `references/`。

## 普通用户怎么用

安装后可以直接说：

```text
做一张归雁主题的中秋手机海报
桂香，做成 50×150mm 书签
只给我月映的提示词，我自己生成
把团圆这张的月饼减到一个完整的和一个切开的，其他不要变
生成月满、桂香、望月、月映、灯火、归雁、团圆、共月八张一套
```

也可以明确写 `$mid-autumn-poetic-poster` 来调用 Skill。要真正出图，使用环境需有图像生成能力；若环境没有，Skill 会交付 Prompt 和排版方案，不能凭 Skill 文件自身画图。

## 一、在自己电脑上检查和试用

1. 解压或打开本文件夹，确认 `.agents`、`.codex-plugin` 两个以点开头的文件夹存在。Windows 资源管理器可能需要开启“显示隐藏的项目”。
2. 先试最简单的问法：“做一张归雁”。检查飞鸟是否是主视觉、月亮是否小而淡、诗句是否无标点、有没有红章。
3. 再试：“只给我月映提示词”。应得到正向 Prompt、负面约束、诗词和尺寸；不应假称已经生成图片。
4. 最后试：“桂香书签，要印刷”。应得到 50×150mm 的成品尺寸、1:3 构图、出血与安全区说明，并提示印厂规范需要确认。

想把它当单独 Skill 使用，可把 `plugins/mid-autumn-poetic-poster/skills/mid-autumn-poetic-poster` 整个文件夹复制到个人 Codex Skill 目录。Windows 常见位置是 `%USERPROFILE%\.codex\skills\mid-autumn-poetic-poster`；如果设置了 `CODEX_HOME`，则放到该目录下的 `skills` 文件夹。不要只复制 `SKILL.md`。

## 二、把这个文件夹打包成 ZIP

本仓库文件夹本身已经是 Plugin + Marketplace 包。若要通过微信、网盘或邮件分享文件，压缩**整个** `mid-autumn-poetic-poster-plugin` 文件夹，收件人解压后应仍有同名顶层文件夹。

Windows PowerShell 可在它的上一级文件夹运行：

```powershell
tar -a -c -f mid-autumn-poetic-poster-plugin.zip mid-autumn-poetic-poster-plugin
```

打开 ZIP 检查 `.agents/plugins/marketplace.json` 和 `plugins/mid-autumn-poetic-poster/.codex-plugin/plugin.json` 是否仍在。部分压缩工具会遗漏点开头的文件夹，因此检查很重要。ZIP 是便于传文件的方式；Codex 的插件发现依赖解压后的目录或 GitHub Marketplace 来源。

## 三、发布到 GitHub：最易操作的 GitHub Desktop 方式

这里发布的是源码仓库，GitHub 不会自动把它上架到 OpenAI 的公共插件目录。

1. 登录 GitHub，并安装 [GitHub Desktop](https://desktop.github.com/)。
2. 在 GitHub Desktop 选择 **File → Add local repository**，选中这个 `mid-autumn-poetic-poster-plugin` 文件夹。如果提示它还不是 Git 仓库，可按界面提示创建仓库；仓库根目录应是本文件夹，不能选到它的上一级 `outputs`。
3. 左侧更改列表应包含 `README.md`、`plugins/` 和 `.agents/`。如果缺少点开头文件夹，先检查它是否真实存在。
4. 在提交说明填“Initial Mid-Autumn poster plugin”，点击 **Commit to main**。
5. 点击 **Publish repository**。仓库名称可用 `mid-autumn-poetic-poster-plugin`。想让所有人能看到，取消勾选 **Keep this code private**；想先内部测试，就保留私有。
6. 发布完成后打开 GitHub 仓库页面，确认 `README.md`、`.agents/plugins/marketplace.json`、`plugins/mid-autumn-poetic-poster/plugin.json`、`skills/.../SKILL.md` 都能看到。

GitHub Desktop 的添加本地项目和发布流程见 [GitHub 官方指南](https://docs.github.com/en/desktop/adding-and-cloning-repositories/adding-an-existing-project-to-github-using-github-desktop)。

## 四、发布到 GitHub：命令行方式

适合已经安装 Git 的用户。先在 GitHub 网站新建一个**空仓库**，名称例如 `mid-autumn-poetic-poster-plugin`。如果准备把当前完整文件夹推上去，新仓库创建时不要再勾选“生成 README / .gitignore / License”，以免首次推送出现分叉。

打开 PowerShell，进入本文件夹所在位置。路径以你的实际位置为准：

```powershell
cd 'C:\你的文件夹\mid-autumn-poetic-poster-plugin'
git init -b main
git status
git add .
git status
git commit -m "Initial Mid-Autumn poster plugin"
git remote add origin https://github.com/YOUR-USERNAME/mid-autumn-poetic-poster-plugin.git
git remote -v
git push -u origin main
```

本仓库的 GitHub 用户名是 `wxf266629-hub`；上面的 `YOUR-USERNAME` 是给复制本仓库另行发布的人保留的示例占位符。若 `git status` 显示个人照片、密钥、临时文件或其他非插件内容，先从本仓库移除，再执行 `git add .`。本成品只含文字规范和配置，不包含原对话中的参考图。

成功后用浏览器打开 `https://github.com/YOUR-USERNAME/mid-autumn-poetic-poster-plugin`，检查目录。GitHub 官方的[本地代码上传步骤](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github)也采用 `git init`、`git remote add origin` 和 `git push` 流程。

## 五、别人怎样从 GitHub 安装

仓库公开后，使用者可在 Codex CLI 执行（将 `YOUR-USERNAME` 换成真实所有者）：

```text
codex plugin marketplace add YOUR-USERNAME/mid-autumn-poetic-poster-plugin
codex plugin marketplace list
```

若希望固定 `main` 分支，可使用：

```text
codex plugin marketplace add YOUR-USERNAME/mid-autumn-poetic-poster-plugin --ref main
```

随后在 Codex / ChatGPT 桌面应用的 **Plugins Directory** 中选择“中秋诗意海报”来源，安装“中秋古风诗意海报生成器”，再开启新对话测试。插件可用性会受客户端版本、账号和组织设置影响；如未显示，先检查 Marketplace 是否添加成功，再刷新或重启桌面应用。Marketplace 的命令、仓库结构和刷新方法见 [OpenAI 官方插件文档](https://developers.openai.com/plugins/build/plugins)。

不使用 Marketplace 的人也可以下载仓库 ZIP，解压后把 `plugins/mid-autumn-poetic-poster/skills/mid-autumn-poetic-poster` 复制到自己的 Skill 目录；这样是“安装 Skill”，不是“安装 Plugin”。

## 六、如何更新，以及别人何时能看到新版

1. 改动仓库内的 `plugins/mid-autumn-poetic-poster/skills/mid-autumn-poetic-poster/`。主题映射、诗词和质量规则分别在 `references/` 内，不要只改一份外部副本。
2. 修改 Plugin 的版本号：同步更新 `plugins/mid-autumn-poetic-poster/plugin.json` 和 `.codex-plugin/plugin.json`。例如从 `0.1.0` 升到 `0.2.0`。两处必须一致。
3. 本地用新对话测试“归雁”“月映提示词”“印刷桂香书签”和“只改一处”等典型请求。
4. 提交并推送到 GitHub。命令行方式：

   ```powershell
   git add .
   git commit -m "Improve poster skill"
   git push
   ```

5. 使用者在 CLI 中运行 `codex plugin marketplace upgrade`，或按客户端的插件更新入口刷新来源。安装后的插件通常使用缓存副本，单纯修改 GitHub 页面不会立即改变正在进行的旧对话；建议更新后开新对话验证。具体刷新方式以 [官方插件文档](https://developers.openai.com/plugins/build/plugins)为准。

## 七、发布前最后检查

- 插件名在三个位置一致：Marketplace 条目、两份 `plugin.json` 都是 `mid-autumn-poetic-poster`。
- 版本号在两份 `plugin.json` 一致。
- `.agents`、`.codex-plugin` 和所有 `references/` 文件都在 GitHub 页面可见。
- 输入“归雁”不会出现抢主体的大月；输入“月映”不会生成笔直白色月光柱。
- 诗词的作者和作品名能对上原作；终稿诗句默认无标点、无红色刻章。
- 若含参考图、人物照片、商标或字体文件，先确认它们能否随仓库公开；本版本没有打包任何参考图或字体文件。
- `LICENSE` 应为 MIT，版权署名为“小小小书创作”；两份 Plugin 清单也应标记 MIT。若今后更改许可证，先核对既有版本与外部贡献的许可约束；参见 [GitHub 许可说明](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/licensing-a-repository)。

## 常见问题

**别人只输入“归雁”，会自动使用吗？** Skill 的 `name` 和 `description` 支持自动发现，但具体是否调用取决于客户端与对话上下文。最稳妥的显式调用是“使用 `$mid-autumn-poetic-poster` 做一张归雁”。

**安装 Plugin 后一定能生成图片吗？** 不一定。Plugin 只提供创作规则和流程；需要当前产品/账号有图像工具。没有工具时仍能得到可复制 Prompt、诗句、排版建议。

**为何诗句有时不直接画在背景里？** 生成模型可能把汉字画错，特别是书法。默认把标题与诗句放在可编辑层，更适合核对和印刷。

**GitHub 仓库公开就等于进入官方插件商店吗？** 不等于。公开仓库可被他人通过 GitHub Marketplace 来源安装；提交公共插件目录是独立的审核/发布流程，参考 [OpenAI 插件提交文档](https://developers.openai.com/plugins/deploy/submission)。
