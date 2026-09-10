# xwjiang2003.github.io

用户站点（User Site）仓库，发布在 <https://xwjiang2003.github.io/>。

## 这个仓库是干什么的

GitHub Pages 有两种站点：

| 类型 | 仓库名 | 发布地址 |
|------|--------|----------|
| **用户站点**（本仓库） | `<用户名>.github.io` | `https://xwjiang2003.github.io/` |
| 项目站点 | 任意其他仓库（如 `tools`） | `https://xwjiang2003.github.io/tools/` |

建这个仓库的**主要目的不是放页面，而是拿回域名根目录的控制权**：

- 根目录可写之后，Google / Bing / 百度 的**文件验证**才能用
  （项目站点只能写 `/tools/`，根路径返回 404，文件方式验证不了）。
- 顺带让 `https://xwjiang2003.github.io/` 不再 404，成为一个导航入口。

## 内容

本仓库还是**主机级文件的唯一归属地**——这些文件只有放在根目录才生效：

| 文件 | 作用 |
|------|------|
| `index.html` | 手写单文件导航页，样式内联、无构建依赖、跟随系统亮暗主题 |
| `robots.txt` | **主机根 robots.txt 才被爬虫读取**。放行各搜索引擎与 18 个 AI 爬虫，声明两个 sitemap |
| `sitemap.xml` | 本根页面的站点地图；`/tools/sitemap.xml` 由 tools 仓库生成 |
| `<key>.txt` | IndexNow 归属校验文件，一份 key 覆盖整个主机 |
| `.nojekyll` | 跳过 Jekyll 处理，避免 GitHub Pages 对文件做多余转换 |

> `/tools/robots.txt` 那份爬虫不会读（robots.txt 只认主机根目录），
> 它的存在只是给审计工具看，两份放行清单需保持同步。

## IndexNow

```bash
cd ../tools && python3 submit.py
```

key 文件在本仓库根目录，因此可以提交**整个主机**的 URL（根页面 + `/tools/` 下全部页面），
不必受 key 文件所在目录的限制。

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
