# 个人主页

静态个人主页，零依赖、零构建。页面在 `index.html`，项目截图在 `assets/`。

- 线上地址：https://realchenchenluo.github.io/personal-site/
- 仓库：https://github.com/realchenchenluo/personal-site

## 页面结构

1. **Hero** — 名字、方向、抽象自画像
2. **About** — 在北京读书、人工智能专业、正在参与的 MOT 财务总助手（团队项目）
3. **Selected Work** — MOT 财务总助手（featured，团队项目，带公开演示链接）+ 6 个网页 / 本地工具项目，桌面端为横向滚动画廊
4. **More** — 数模 A 题、Suki 小程序、AI 漫画
5. **Note** — 滚动文字宣言与喜欢的一句话
6. **Contact** — 邮箱、GitHub、相关链接

## 本地预览

```bash
cd personal-site
python -m http.server 8000
```

然后打开 http://localhost:8000/ 。

直接双击 `index.html` 也可以；用本地服务器是为了更接近线上环境。

## 改哪里

| 内容 | 位置 / 关键词 |
| --- | --- |
| 姓名 | `Chen Chen` / `CHEN CHEN` |
| 自我介绍 | `intro-lead`、`hero-intro` |
| 邮箱（页面里有 3 处） | `realchenchenluo@gmail.com` |
| 作品 | `id="work"` 下的 `feature-card` 与 `project-grid` |
| 实验项目 | `id="experiments"` 下的 `experiments-grid` |
| 项目截图 | `assets/*.webp`，替换时保持文件名即可 |
| 此刻、工具箱、原则 | `about-bento` 里的三张卡片 |

几点说明：

- 所有项目图都是从线上页面或本地项目截图后压成 WebP，统一放在 `assets/`。
- 词声项目原来的标题含姓名缩写，已在 `cisheng` 仓库里去掉；个人页这边只保留「词声」。
- 银行 Agent 是团队项目，卡片明确标注「团队协作 · 我是队员」，并链接到公开演示：
  https://personal-ai-fund-manager-mot-staging.ai-banking-agent.workers.dev/app
  具体分工以团队为准，页面没有替本人展开未确认的职责。
- 默认跟随系统深浅色，右上角按钮可手动切换，选择会记在 localStorage。
- 没有外部字体、CDN、统计脚本。

## 动效

页面的动效语言参考 [motion-prompt](https://showheyohtaki.github.io/motion-prompt/)（MIT），按其编号规范实现为原生 CSS / JS，没有新增依赖：

| 编号 | 效果 | 用在哪 |
| --- | --- | --- |
| #083 | 光标跟随 | 全站，朱红圆环跟随指针（跟随系数 0.3，比原参数更跟手） |
| #084 | 磁吸按钮 | 首屏两个按钮、复制邮箱按钮 |
| #077 | 横向滚动 | 作品区 6 张卡片随页面纵向滚动横向移动；移动端与减少动效时回落为纵向网格 |
| #005 | 遮罩显现 | 章节标题与项目图片从遮罩后滑入 |
| #154 | 聚光灯悬停 | 作品卡片、银行 Agent 与深色实验卡片 |
| #146 | 滚动文字显现 | 「把想法做成能跑的东西」整段 |
| #149 | 滚动隐藏页头 | 向下滚动收起，向上滚动出现 |
| #150 | 滚动监听 | 导航高亮当前章节 |
| #153 | 3D 倾斜 | 首屏抽象自画像，随光标倾斜并有反光 |
| #167 | 向下滚动提示 | 首屏底部的 SCROLL 鼠标动画 |

触屏设备和开启「减少动效」的系统设置下，光标、磁吸、倾斜、滚动提示会自动关闭，文字直接完整显示。

## 更新线上版本

已经部署在 GitHub Pages。改完文件后：

```bash
git add -A
git commit -m "update homepage"
git push
```

等 20–30 秒，线上自动生效，不需要重新构建。

## 首次部署（换仓库时参考）

```bash
cd personal-site
git init -b main
git add -A
git commit -m "personal homepage"
gh repo create realchenchenluo/<repo> --public --source=. --push
gh api -X POST repos/realchenchenluo/<repo>/pages \
  -f "source[branch]=main" -f "source[path]=/"
gh api repos/realchenchenluo/<repo>/pages/builds/latest --jq .status
```

等状态变成 `built`（约 20–30 秒），访问：

```
https://realchenchenluo.github.io/<repo>/
```

免费版 GitHub Pages 要求仓库公开。`.nojekyll` 已经放好，用来跳过 Jekyll 处理。

## 文件

```
personal-site/
├── index.html      # 页面结构、样式与脚本
├── assets/         # 项目截图与封面（WebP）
├── .nojekyll       # GitHub Pages 跳过 Jekyll
└── README.md
```
