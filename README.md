# xwjiang2003.github.io

用户站点（User Site）仓库，发布在 <https://xwjiang2003.github.io/>。

## 这个仓库是干什么的

2026-09 起，**工具站已经迁到独立域名 <https://devtools.help/>**（CNAME 绑在 `tools` 仓库上，
由该仓库的 `docs/` 发布）。本仓库保留为：

- `https://xwjiang2003.github.io/` 上的一个**导航落地页**，直接指向 `devtools.help`；
- **本主机**（`xwjiang2003.github.io`）的 robots.txt 与 sitemap.xml 归属地。

> 注意：`robots.txt` 只认**主机根**。`xwjiang2003.github.io` 和 `devtools.help` 是**两个主机**，
> 各有各的 robots.txt，互不生效。工具站那份在 `tools` 仓库的 `docs/robots.txt`。

## 内容

| 文件 | 作用 |
|------|------|
| `index.html` | 单文件导航落地页，链接直接指向 `https://devtools.help/`（省掉一次 301） |
| `robots.txt` | 本主机根 robots.txt。放行搜索引擎与 18 个 AI 爬虫，声明两份 sitemap |
| `sitemap.xml` | 本落地页的站点地图 |
| `.nojekyll` | 跳过 Jekyll 处理 |

## IndexNow

IndexNow 的 key 文件**已迁到工具站**：<https://devtools.help/9f4c1d7a2e8b5306ac1f7d9e4b2a8c30.txt>。

因为提交的是 `devtools.help` 主机下的 URL，key 必须放在**那个主机**的根目录，
所以文件由 `tools` 仓库的 `build.py` 生成到 `docs/CNAME` 同级，本仓库不再承载。

```bash
cd ../tools && python3 submit.py
```

## 加搜索引擎验证文件

拿到验证码后二选一：

**方式 A：文件验证**（现在可行了）——把下载到的 `baidu_verify_xxxx.html`、
`googleXXXX.html` 等直接放到本仓库根目录，提交推送即可。

**方式 B：HTML 标记验证** ——把 `index.html` 里对应的注释行取消注释并填入验证码：

```html
<!-- <meta name="google-site-verification" content="..."> -->
<!-- <meta name="msvalidate.01" content="..."> -->
<!-- <meta name="baidu-site-verification" content="..."> -->
```

| 平台 | 入口 |
|------|------|
| Google Search Console | <https://search.google.com/search-console> |
| Bing 网站管理员工具 | <https://www.bing.com/webmasters> |
| 百度搜索资源平台 | <https://ziyuan.baidu.com> |

## 本地预览

```bash
python3 -m http.server 8080
# 打开 http://localhost:8080
```

## 注意

- 用户站点每个账号**只能有一个**，仓库名必须是 `<用户名>.github.io`，大小写需小写。
- 本仓库与 `tools` 项目站点互不影响，`/tools/` 照常发布。
- 改了 `index.html` 只要提交推送就会自动重新发布，无需构建步骤。
