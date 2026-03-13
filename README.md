# BidKing Web

BidKing Web 是一个纯前端的盲盒竞拍原型，用来验证地图产出、角色信息、五回合竞拍、结算和仓库循环。

## 项目类型

这是静态页面项目，不依赖 Python 作为运行时，也没有后端服务依赖。

但它不能直接双击 `index.html` 用 `file://` 打开，原因是前端启动时会请求本地 JSON 数据文件：

- `./data/bidking_items_seed_v1.json`

浏览器在 `file://` 模式下对 `fetch()` 本地文件通常会有限制，所以必须通过 HTTP 服务访问。这个 HTTP 服务可以是：

- `nginx`
- `python3 -m http.server`
- `npx serve`
- 任何别的静态文件服务器

Python 只是临时调试时最省事的一种方式，不是必须。

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

如果你把项目放到自己的电脑上，本地使用方式也是一样的：需要先起一个静态文件服务，再用浏览器访问对应的 `http://` 地址。

不要直接双击：

```text
index.html
```

也不要直接用：

```text
file:///.../index.html
```

因为页面启动时会请求：

```text
./data/bidking_items_seed_v1.json
```

浏览器在 `file://` 模式下通常会拦截这类请求。

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

### 5. 不要直接双击 HTML

以下方式不正确：

```text
file:///opt/bid-king-web/index.html
```

这样打开时，页面里的 `fetch('./data/bidking_items_seed_v1.json')` 很可能失败，导致页面初始化异常。

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

### 这是静态页面，为什么还要服务？

因为“静态页面”只代表没有后端业务逻辑，不代表可以直接用 `file://` 访问。只要前端里用了 `fetch()` 去读本地 JSON，就应该通过 HTTP 服务访问。

### 必须有 Python 环境吗？

不是。Python 只是一种临时起静态服务的办法。你现在已经在用 `nginx`，所以正常使用并不需要 Python。

### 为什么起始资金没变？

如果浏览器还在读旧存档，就会继承旧数据。这次已经把存档键改成了 `bidking-web-prototype-v3`，正常刷新后会走新的默认档。
