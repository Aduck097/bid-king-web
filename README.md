# BidKing Web

BidKing Web 是一个纯前端的盲盒竞拍原型，用来验证地图产出、角色信息、五回合竞拍、结算和仓库循环。

## 项目类型

这是静态页面项目，不依赖 Python 作为运行时，也没有后端服务依赖。

现在可以直接双击 `index.html` 用 `file://` 打开。

项目里的静态种子数据已经改成通过脚本直载：

- `./data/bidking_items_seed_v1.js`

所以本地双击打开和通过 HTTP 服务访问都支持。

如果你仍然想通过服务访问，可以使用：

- `nginx`
- `python3 -m http.server`
- `npx serve`
- 任何别的静态文件服务器

Python 只是临时调试时最省事的一种方式，不是必须；正常使用也不再要求一定启动服务。

## 当前访问方式

当前环境已经接入 `nginx`，访问地址是：

- `http://127.0.0.1/bid-king/`

如果你从其他机器访问，改成：

- `http://服务器IP/bid-king/`

## 当前游戏默认值

- 起始资金：`100,000`
- 存档键：`bidking-web-prototype-v3`

这次把存档键升到了 `v3`，目的是让新的经济平衡和起始资金立即生效，避免继续读取旧存档里的高额资金。

## 功能范围

当前原型包含：

- 地图选择与资产门槛
- 地图独立底仓区间、整盒价值区间、盈利率区间
- 角色与道具配置
- 五回合竞拍
- AI 对手竞价
- 结算、快速卖出、跳过鉴定
- 仓库入库与出售
- 浏览器本地存档

暂不包含：

- 后端服务
- 数据库
- 多人联机
- 账号系统

## 目录说明

- `index.html`: 页面入口
- `app.js`: 核心玩法逻辑、数值、AI、结算、仓库
- `styles.css`: 页面样式
- `data/`: 静态种子数据
- `docs/`: 设计文档
- `openspec/`: 变更提案与规格记录

## 使用方法

### 1. 通过 nginx 访问

适合当前这台机器，已经配置完成。

直接打开：

```text
http://127.0.0.1/bid-king/
```

### 2. 本地使用

如果你把项目放到自己的电脑上，最简单的方式就是直接打开：

```text
index.html
```

或者：

```text
file:///.../index.html
```

现在页面初始化不再依赖 `fetch()` 读取本地 JSON，所以可以直接双击使用，浏览器本地存档仍然保存在当前浏览器里。

### 3. 本地临时启动方式

如果你不想走 nginx，也可以在项目目录起一个临时静态服务。

示例 1，使用 Python：

```bash
cd /opt/bid-king-web
python3 -m http.server 3000 --bind 127.0.0.1
```

然后访问：

```text
http://127.0.0.1:3000/
```

示例 2，使用 Node 工具：

```bash
cd /opt/bid-king-web
npx serve .
```

然后按命令行输出的地址访问，通常是：

```text
http://127.0.0.1:3000/
```

### 4. 本地系统示例

Windows：

```bash
cd D:\bid-king-web
python -m http.server 3000
```

macOS / Linux：

```bash
cd /path/to/bid-king-web
python3 -m http.server 3000
```

如果本地没有 Python，但有 Node，也可以：

```bash
npx serve .
```

### 5. 什么时候还需要 nginx

如果你有以下需求，仍然建议走 `nginx` 或其他静态服务：

- 想通过局域网给其他设备访问
- 想挂到固定路径，如 `/bid-king/`
- 想和其他站点统一放到一台服务器里
- 想避免不同浏览器对 `file://` 的细节差异

## nginx 配置说明

当前站点是通过 `nginx` 的路径代理方式挂载的：

- 路径：`/bid-king/`
- 配置文件：`/etc/nginx/default.d/bid_king_web.conf`

核心逻辑是把：

```text
/bid-king/
```

映射到：

```text
/opt/bid-king-web/
```

## 开发说明

如果你修改了前端文件：

- `app.js`
- `styles.css`
- `index.html`

通常不需要重启 `nginx`，浏览器刷新即可看到最新静态文件。

如果你修改的是 `nginx` 配置，则需要：

```bash
nginx -t
systemctl reload nginx
```

## 常见问题

### 这是静态页面，现在还必须要服务吗？

不是必须。现在已经支持直接双击 `index.html` 使用。只有在你需要远程访问、统一入口或服务器部署时，才建议继续走 `nginx`。

### 必须有 Python 环境吗？

不是。Python 只是一种临时起静态服务的办法。现在即使没有 Python，也可以直接打开 `index.html` 使用。

### 为什么起始资金没变？

如果浏览器还在读旧存档，就会继承旧数据。这次已经把存档键改成了 `bidking-web-prototype-v3`，正常刷新后会走新的默认档。
