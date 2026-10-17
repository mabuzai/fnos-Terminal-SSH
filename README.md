# 终端SSH（fnwebssh）

飞牛 fnOS 原生 WebSSH 终端。装上是桌面里的一个图标，点开就是一台真终端——能敲命令、能改配置、能翻远端文件、能看资源占用，手机和电脑都能用。

`platform` 飞牛 fnOS　·　`arch` x86 / ARM　·　`license` MIT

---

## 它解决什么问题

飞牛自带的应用里没有趁手的 SSH 客户端。用浏览器开第三方 WebSSH，要么要单独部署、占端口，要么手机上没法用。

这个应用是原生 FPK 包：装完在飞牛桌面就是一个图标，点开在桌面窗口内打开，走飞牛统一网关，不占任何端口，也不用额外记一个地址。SSH 会话跑在飞牛本机，密码不落盘、只在本次会话使用。

---

## 功能一览

| 功能 | 手机 | 电脑 |
|---|:---:|:---:|
| 真交互式终端 | ✅ | ✅ |
| 系统监控（CPU / 内存） | ✅ | ✅ |
| 网络流量监控 | ✅ | ✅ |
| 远端音频播放 | ✅ | — |
| 远端文件浏览与操作 | ✅ | ✅ |
| 常用命令库（296 条） | ✅ | ✅ |
| 内置文本编辑器 | ✅ | ✅ |
| 连接管理 | ✅ | ✅ |

---

## 真交互式终端

基于真实 PTY，vim / top / less 这类全屏程序都能正常跑，不是那种只能一条条发命令的"伪终端"。支持 ANSI 颜色、光标定位、窗口尺寸自适应。

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-01-mobile-terminal.png" width="45%">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-07-desktop-overview.png" width="50%">
</p>

<p align="center">左：手机端终端主界面　·　右：电脑端三栏完整界面（连接管理 · 终端 · 远端文件）</p>

---

## 系统监控

实时看远端机器的资源占用——CPU、内存、负载，不用再敲 `top` 盯着一个刷新的终端看。

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-02-mobile-monitor-cpu.png" width="45%">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-08-desktop-monitor.png" width="50%">
</p>

<p align="center">左：手机端 CPU / 内存监控　·　右：电脑端系统监控面板</p>

### 网络流量监控

单独一块看实时上下行速率、连接数，排查"到底是哪个服务在吃带宽"时很省事。

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-03-mobile-monitor-network.png" width="45%">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-09-desktop-monitor-network.png" width="50%">
</p>

<p align="center">左：手机端网络监控　·　右：电脑端网络监控</p>

---

## 远端音频播放

直接在远端文件列表里播放音频文件，不用先下载到本地再找播放器。手机上尤其方便——NAS 里的音乐点开就听。

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-04-mobile-audio-player.png" width="45%">
</p>

<p align="center">手机端远端音频播放</p>

---

## 远端文件浏览

浏览远端目录、下载文件、重命名、删除、新建文件夹、查看属性、复制粘贴路径。手机上是独立的一个「文件」页签。

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-06-mobile-files.png" width="45%">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-05-mobile-file-actions.png" width="45%">
</p>

<p align="center">左：手机端远端文件浏览　·　右：长按文件弹出的操作菜单</p>

---

## 内置常用命令库（296 条）

这可能是最省事的部分。内置 296 条常用命令，分 11 组，覆盖两套系统：

| 分类 | 分组 | 命令数 |
|---|---|---|
| OpenWrt | 配置修改（uci）· 系统与服务 · 软件与文件 · 网络诊断 · 监控与防火墙 | 143 |
| 飞牛 fnOS | 存储与阵列 · Docker · 系统与服务 · 网络与文件 · 监控与备份 · 用户与权限 | 153 |

- 分组横向排列在顶部，点一下就切，不用从头往下滚
- 查看命令和修改命令成对出现：*查看网络配置* 下面紧跟 *修改网络配置*，改完就有得看
- 点条目填入输入框（可以再改改），点 ▶ 立即执行

<p align="center">
  <img src="https://raw.githubusercontent.com/mabuzai/fnos-Terminal-SSH/main/screenshot-10-desktop-commands.png" width="80%">
</p>

<p align="center">电脑端常用命令面板（OpenWrt · 配置修改）</p>

---

## 命令自动分流：查看走终端，编辑走编辑器

不用记什么时候该用 cat、什么时候该用 vi，应用自己判断：

- 只读查看类（cat / less / more / head / tail）→ 结果直接在终端显示
- 可编辑类（vi / vim / nano）→ 自动用内置编辑器打开远端文件

改完点「保存」，会通过已建立的 SSH 会话写回（走 heredoc 覆盖写），不用再手动 scp 传文件。

### 内置文本编辑器

不是把 vi 塞进网页里硬跑，而是读文件 → 编辑 → 写回的模式，所以：

- 打开快，没有 vi 的模态困惑
- 支持大文件（多帧分片，实测 400 行无压力）
- 保存时自动补末尾换行——不补的话 heredoc 结束标记会粘在末行，shell 会卡死、文件根本不生成
- 编辑器打开时命令输入框不消失，可以随时敲命令

---

## 连接管理

- 保存多个连接（如 openwrt、飞牛），点一下切换
- 密码 / 私钥两种认证
- 兼容旧设备开关：放开 ssh-rsa / ssh-dss 和 diffie-hellman-group1-sha1 等老算法，连得上那些年头较久的交换机和路由器

### 主机密钥自愈

OpenWrt 刷机、重置、升级 dropbear 后会重新生成 ED25519 主机密钥，普通 SSH 客户端会报：

```
The fingerprint for the ED25519 key sent by the remote host is ...
Host key verification failed.
```

无人值守环境下没人能点 "yes"，就一直连不上。这个应用会自动清除冲突的旧记录并重新接受，装上就能连。

---

## 手机 / 电脑双端

同一套前端，布局自动适配：

- **电脑**：三栏（连接管理 · 终端 · 远端文件），侧栏文字随窗口大小缩放
- **手机**：底部页签切换（终端 / 文件 / 连接），命令条跟随输入法，全屏模式下也贴在键盘上沿

### 其它

- 命令记录：发过的命令都能翻
- 终端字号 A- / A+ 调节
- 会话保持：关掉界面再回来能接回原来的会话
- 可选 AI 辅助：把自然语言转成命令并给出风险评级（需在高级设置里自行配置 OpenAI 兼容接口，默认不启用）

---

## 安装

到 Releases 下载对应架构的包：

- x86 版 —— x86 机器（大部分 NAS / 迷你主机）
- ARM 版 —— ARM 机器（ARM 版内置 Python 3.9，包约 7.9 MB）

飞牛桌面 → 应用中心 → 手动安装 → 选中 .fpk

装完桌面出现「终端SSH」图标，点开即用

架构不确定的话，SSH 进飞牛执行 `uname -m`：看到 `x86_64` 选 x86，看到 `aarch64` / `armv7l` 选 ARM。

---

## 快速上手

1. 左侧「连接管理」填主机 / 端口 / 用户名 / 密码，点「连接到 SSH」
2. 想改 OpenWrt 配置：底部「⚡ 常用命令」→ 选 OpenWrt → 找 *修改网络配置* → 点 ▶
3. 编辑器打开后直接改，点「保存」写回
4. 想看结果：点 *查看网络配置*，输出直接显示在终端

---

## 技术实现

| | x86 | ARM |
|---|---|---|
| 运行时 | Go 二进制 | 内置 Python 3.9（22 MB，随包携带） |
| 前端 | 单文件 HTML（内联 CSS / JS，无外部依赖） | 同左 |
| 通信 | WebSocket + Unix Socket，走飞牛统一网关 | 同左 |
| 包体 | 约 2.5 MB | 约 7.9 MB |

两端共用同一份前后端代码，只有运行时不同。

SSH 连接调用系统 ssh 客户端（`-tt` 强制分配 PTY），所以 SSH 的能力取决于飞牛上装的 OpenSSH 版本。

---

## 常见问题

**连不上，提示 Host key verification failed**

升级到较新版本。旧版本对主机密钥变更会直接拒绝，新版本会自动清除旧记录重新接受。

**能装但打不开（白屏 / 一直转圈）**

大概率是运行时没起来。SSH 进飞牛看应用日志：

```
cat /vol1/@appcenter/fnwebssh/app.log
```

日志里有启动自检，会打出 uname、$PATH、应用目录清单，基本一眼能定位。

**ARM 版特别大**

正常。ARM 版内置了 Python 3.9（22 MB），这样机器上没装 python3 也能跑，不用联网装依赖。

**桌面图标没刷新**

覆盖安装后如果图标或入口没变，SSH 进飞牛重启应用中心服务：

```
sudo systemctl restart trim_app_center.service
```

---

## 说明与免责

- 主机密钥校验设为宽松模式，面向家庭内网自有设备。若在不信任的网络中使用，请自行评估风险。
- 常用命令库中的部分命令（尤其是 reboot / poweroff / mkfs / 重置配置类）具有破坏性，点 ▶ 会直接执行，没有二次确认，使用前请确认。
- 飞牛特有的工具名（如部分存储管理命令）可能需要你的系统上确实安装了对应工具，不存在时点 ▶ 会回落到终端执行并报错。

---

## 许可

MIT
