# 上线到公网 · 超详细中文步骤（含 GitHub 英文按钮对照）

**做完能达到什么效果**：得到一个网址，发给任何人打开都能用；新闻每天自动更新；**不用备案、不用你电脑开机、完全免费**。

---

## 📖 先看这张"英文按钮对照表"（操作时对着看）

GitHub 网站界面是英文的，下面是你**会遇到的按钮**和它们的中文意思：

| 界面上的英文 | 中文意思 | 出现在哪 |
|---|---|---|
| Sign in / Sign up | 登录 / 注册 | 打开 GitHub 首页右上角 |
| New repository | 新建仓库（仓库＝项目文件夹） | 右上角「+」号菜单里 |
| Repository name | 仓库名字（填 cet-workbench） | 新建仓库页面第一栏 |
| Public / Private | 公开 / 私有（选 **Public** 才免费用 Pages） | 新建仓库页面下方 |
| Create repository | 创建仓库 | 新建仓库页面最下方绿色按钮 |
| Add file | 添加文件 | 仓库页面右上方 |
| Upload files | 上传文件 | 点 Add file 后的菜单第二项 |
| Create new file | 新建文件（用来手动建目录） | 点 Add file 后的菜单第一项 |
| Commit changes | 提交更改（＝保存） | 上传/编辑完页面底部 |
| Commit directly to the main branch | 直接提交到主分支（默认选中即可） | 提交框里 |
| Settings | 设置 | 仓库页面上方标签栏最右侧 |
| Actions | 自动化任务（机器人） | 仓库页面上方标签栏 |
| General | 常规设置 | 点 Settings 后左侧菜单第一项 |
| Workflow permissions | 工作流（机器人）权限 | Actions → General 页面最下方 |
| Read and write permissions | 读写权限（**必须选这个**） | 上面那项里的单选项 |
| Run workflow | 立即运行这个任务 | Actions 页面右侧的下拉按钮 |
| Pages | 静态网页托管 | Settings 左侧菜单里 |
| Source / Deploy from a branch | 来源 / 从分支部署 | Pages 页面中间的下拉框 |
| Branch: main · /(root) | 分支：main · 根目录 | Pages 页面第二个下拉框 |
| Save | 保存 | 上面那项右边 |
| Deploy | 部署（发布） | Vercel 网站里的按钮 |

---

## 第 1 步 · 新建仓库

1. 打开 github.com 并登录；
2. 点右上角 **➕ → New repository**（新建仓库）；
3. **Repository name**（仓库名）填：`cet-workbench`
4. 下面选 **Public**（公开）；
5. 点最下方绿色按钮 **Create repository**（创建仓库）。

## 第 2 步 · 上传文件（两部分）

### 2.1 先上传普通文件（可拖拽）

1. 在仓库页面点 **Add file → Upload files**（添加文件 → 上传文件）；
2. 把下面这些文件**拖进上传框**（它们都在 `cet-workbench` 文件夹里）：
   - `index.html`
   - `content.js`
   - `grammar.js`
   - `words.js`
   - `README.md`
   - `使用说明.md`
   - `GitHub部署步骤.md`
3. 拉到页面底部，点绿色按钮 **Commit changes**（提交更改）。
   > 如果让你选，就保持默认的 **Commit directly to the main branch**，然后点 Commit changes。

> ❌ **不要传** `_backup` 文件夹（那是旧版备份，没用）。

### 2.2 再手动建两个文件（因为有子目录，拖拽传不了）

**第一个：机器人的配置**

1. 点 **Add file → Create new file**（添加文件 → 新建文件）；
2. 在最上面的文件名框里，**原样输入**（斜杠会自动创建目录）：
   ```
   .github/workflows/daily-news.yml
   ```
3. 把本机 `cet-workbench\.github\workflows\daily-news.yml` 里的**全部内容**复制粘贴到下面的大输入框；
4. 拉到最下点 **Commit changes**。

**第二个：抓新闻的脚本**

1. 再点 **Add file → Create new file**；
2. 文件名框输入：
   ```
   scripts/update_news.py
   ```
3. 把本机 `cet-workbench\scripts\update_news.py` 的**全部内容**复制粘贴进去；
4. 拉到最下点 **Commit changes**。

> 💡 复制 `.yml` 文件内容时**别改缩进**（YAML 格式对逗号前的空格敏感）。整段原样粘贴最保险。
> 💡 嫌麻烦也可以装 **GitHub Desktop**（图形软件），把整个 `cet-workbench` 文件夹拖进去，一键 **Publish repository**（发布仓库），子目录和隐藏目录会全部带上。

## 第 3 步 · 给机器人开权限（这一步漏了，后面就白做）

1. 在仓库页面点 **Settings**（设置）；
2. 左侧点 **Actions → General**（自动化 → 常规）；
3. 页面拉到**最下面**，找到 **Workflow permissions**（工作流权限）；
4. 选 **Read and write permissions**（读写权限）；
5. 点 **Save**（保存）。

## 第 4 步 · 手动跑一次，确认成功

1. 在仓库页面点 **Actions**（自动化）；
2. 左侧会看到任务名 **Daily News Update**，点它；
3. 右侧点 **Run workflow**（运行工作流）→ 弹窗里再点一次绿色 **Run workflow**；
4. 等 15～30 秒刷新页面：
   - 出现 **绿色 ✓** = 成功；
   - 点进这次运行记录，展开第三步，日志末尾会打印「已写入 15 条新闻」；
5. 回到仓库首页，能看到 `content.js` 的更新时间变成"几分钟前"。

**之后它每天北京时间早上 6:30 自动运行，你什么都不用做。**

## 第 5 步 · 生成公网网址（两种，选一个或都做）

### 方式一：GitHub Pages（最省事）

1. **Settings → Pages**（设置 → 静态网页托管）；
2. **Source** 选 **Deploy from a branch**（从分支部署）；
3. **Branch** 选 **main**，右边目录选 **/(root)**，点 **Save**；
4. 等 1～2 分钟刷新，页面顶部会出现网址：
   ```
   https://你的用户名.github.io/cet-workbench/
   ```
   这就是能发给别人的链接。

### 方式二：Vercel（国内访问通常更快更稳）

1. 打开 vercel.com，点 **Sign up / Log in with GitHub**（用 GitHub 登录，免费）；
2. 点 **Add New → Project**（新建 → 项目）；
3. 在列表里选你刚建的 `cet-workbench` 仓库，点 **Import**；
4. 什么都不用改，直接点 **Deploy**（部署）；
5. 等 30 秒左右，得到网址：
   ```
   https://cet-workbench-xxxx.vercel.app
   ```
6. 以后仓库每次更新，Vercel 会自动重新发布。

## 第 6 步 · 分享

把网址发给同学：手机、电脑浏览器直接打开就能用；手机上可以"添加到主屏幕"，跟 App 一样。

> 访问速度提示：`github.io` 有时慢、可能打不开；`vercel.app` 一般更顺。建议两个都做，发链接时优先给 Vercel 那个。本机的文件夹版（桌面图标）留着当备份。

---

## 你可能会问的

**Q：手机上能背单词、做听力吗？**
能，全部功能都能用；背单词进度存在各人自己的手机浏览器里。

**Q：为什么不用国内服务器？**
国内服务器要备案。境外托管免备案，代价是偶尔慢一点——学习工具可以接受。

**Q：每天只更新新闻，文章和听力会不会一直是旧的？**
新闻交给机器人天天更新；文章和听力材料由我批量生成后随仓库发布（会一次做好几个月的量）。想加新文章时，把新的 `content.js` 上传覆盖即可，网址立刻更新。

**Q：机器人抓不到新闻会把页面弄空吗？**
不会。脚本设定"抓不到就保持原内容不动"。

**Q：以后想改成每天更新两次？**
把 `.github/workflows/daily-news.yml` 里的 `- cron: '30 22 * * *'` 改成两行（例如再加一行 `- cron: '30 10 * * *'`，即北京 18:30），保存即可。

**Q：有费用吗？**
仓库、Actions（公开仓库不限时长）、Pages、Vercel 免费额度，对这个项目都是 0 元。
