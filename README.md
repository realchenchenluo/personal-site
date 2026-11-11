# 个人主页

单文件静态个人主页，零依赖、零构建。`index.html` 里包含全部 HTML / CSS / JS，直接双击就能打开。

- 线上地址：https://realchenchenluo.github.io/personal-site/
- 仓库：https://github.com/realchenchenluo/personal-site

## 本地预览

```bash
cd personal-site
python -m http.server 8000
```

然后打开 http://localhost:8000/ 。

直接双击 `index.html` 也可以；用本地服务器是为了更接近线上环境。

## 改哪里

全是静态文本，直接在 `index.html` 里搜索替换即可：

| 内容 | 搜索关键词 |
| --- | --- |
| 姓名、英文名 | 罗晨晨 / CHENCHEN LUO / CHENCHEN |
| 学校与自我介绍 | 北京语言大学 |
| 邮箱（页面里有 3 处） | `realchenchenluo@gmail.com` |
| 首页三行近况 | `Now` / `Learning` / `Playing` |
| 作品列表 | `01 / Selected Work` 下面的六个 `<a class="work-row">` |
| 关于、此刻、工具箱 | `card-about` / `card-now` / `card-tools` |

几点说明：

- 作品链接目前指向 GitHub Pages 上的线上地址，改成自己的即可。
- 头像是内联 SVG 的抽象画，不是照片；想换真人照片，可把 `<figure class="portrait">` 里的 `<svg>` 换成 `<img>`。
- 默认跟随系统深浅色，右上角按钮可手动切换，选择会记在 localStorage。
- 页面没有外部字体、CDN、统计脚本，断网也能完整显示。

## 动效

页面的动效语言参考 [motion-prompt](https://showheyohtaki.github.io/motion-prompt/)（MIT），按其编号规范实现为原生 CSS / JS，没有新增依赖：

| 编号 | 效果 | 用在哪 |
| --- | --- | --- |
| #083 | 光标跟随 | 全站，朱红圆环延迟跟随指针 |
| #084 | 磁吸按钮 | 首屏两个按钮、复制邮箱按钮 |
| #146 | 滚动文字显现 | 「把想法做成能跑的东西」整段 |
| #149 | 滚动隐藏页头 | 向下滚动收起，向上滚动出现 |
| #150 | 滚动监听 | 导航高亮当前章节 |
| #153 | 3D 倾斜 | 首屏抽象自画像，随光标倾斜并有反光 |
| #167 | 向下滚动提示 | 首屏底部的 SCROLL 鼠标动画 |

触屏设备和开启「减少动效」的系统设置下，光标、磁吸、倾斜、滚动提示会自动关闭，文字直接完整显示。

## 更新线上版本

已经部署在 GitHub Pages。改完 `index.html` 后：

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
├── index.html   # 全部内容
├── .nojekyll    # GitHub Pages 跳过 Jekyll
└── README.md
```
