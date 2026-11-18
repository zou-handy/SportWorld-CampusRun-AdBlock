# 运动世界校园 · 去广告规则

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Rules](https://img.shields.io/badge/rules-149-blue.svg)](#规则构成)
[![No Root](https://img.shields.io/badge/root-not%20required-green.svg)](#为什么不需要-root)

> 💡 **增强维护版说明（v1.2.0）**：本仓库基于 [@lukezzt8/SportWorld-CampusRun-AdBlock](https://github.com/lukezzt8/SportWorld-CampusRun-AdBlock) 深度改进（已提交上游 PR [#1](https://github.com/lukezzt8/SportWorld-CampusRun-AdBlock/pull/1)）：
> 1. **进程级防误伤隔离（`PROCESS-NAME`）**：彻底阻断运动世界开屏/摇一摇自动跳转**千问 Qwen、通义、夸克、UC 汇川、淘宝、抖音直播流、快手广告图床**，同时日常刷千问/夸克/淘宝/饿了么/抖音/快手 **100% 零误伤**；
> 2. **突破「自家服务器横幅不可拦」边界**：经 Mihomo `:9090` 实时进程连接取证，运动世界后端采用微服务子域拆分——外科手术级精准拦截自家发现流与轮播横幅子域（`discovery.gxapp.iydsj.com`、`swapp-image.gxapp.iydsj.com`、`fxzb.vip`），同时 **100% 放行**核心跑步、GPS 轨迹上传与极验防作弊子域（`run.gxapp.iydsj.com`、`datapoint.gxapp.iydsj.com`、`partner.iydsj.com`、`h5.gxapp.iydsj.com`）；
> 3. **FlClash / Clash Verge Rev 一键导入 `.js` 脚本**：
>    - 📦 **一键脚本直链下载（Release v1.2.0）**：[`campusrun_flclash_script.js`](https://github.com/zou-handy/SportWorld-CampusRun-AdBlock/releases/download/v1.2.0/campusrun_flclash_script.js)
>    - ⚡ **国内免翻墙 CDN 直链**：[`https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/scripts/campusrun_flclash_script.js`](https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/scripts/campusrun_flclash_script.js)


## 🎯 不懂技术?复制这段话给 AI 就行

打开任意 AI 助手(**豆包 / DeepSeek / 通义千问 / ChatGPT** 都行),把下面这段发给它:

```
我要给手机上的「运动世界校园」App 去掉广告。

我完全不懂技术,请你手把手教我:

1. 规则已经有人做好了,地址是:
   https://github.com/zou-handy/SportWorld-CampusRun-AdBlock

2. 每次只让我做一件事,我回复「好了」你再讲下一步

3. 告诉我每一步在手机上点哪里(具体到"打开设置 → 找到应用 → ...")

4. 不要说专业名词;必须说的,先用大白话解释一遍

5. 我不会或者找不到时,换个方式教我

6. 我发截图给你,你要能看懂

最后告诉我:怎么确认成功?万一坏了怎么恢复原样?
```

AI 会先问你几个问题,然后一步步带你做完。**卡住了就直接截图发给它。**

> 更详细的小白图文步骤 👉 [**docs/getting-started.md**](docs/getting-started.md)

---

针对 **运动世界校园**(`com.zjwh.android_wh_physicalfitness`)的广告域名拦截规则。

规则从 APK 静态逆向提取,并经手机实测日志验证。**不修改 APK、不需要 Root。**

---

## 规则构成

| 类型 | 条数 | 说明 |
|---|---|---|
| `AND` + `PROCESS-NAME` 进程级隔离规则 | 47 | 仅在运动世界校园进程内拦截 `qianwen.com` / `quark.cn` / `uc.cn` / `taobao.com` / `alicdn.com` / `snssdk.com` / `douyin.com` / `kuaishou.com` / `yximgs.com` 及非高德 HTTPDNS，**日常使用千问/夸克/淘宝/饿了么/抖音/快手零误伤** |
| 自家非核心推广与轮播横幅子域 | 3 | 精准拦截 `discovery.gxapp.iydsj.com`（发现页/活动流）、`swapp-image.gxapp.iydsj.com`（首页运营横幅图床）、`fxzb.vip`（内置商城），不影响核心跑步与成绩上传 |
| `DOMAIN-SUFFIX` 纯广告 SDK 父域规则 | 78 | 一条覆盖整棵子树，抗动态子域（`campusrun.yaml` 中已补齐 `+.` 通配） |
| `DOMAIN` 纯广告 SDK 精确规则 | 21 | 补齐父域规则未覆盖的独立广告主机 |
| **合计** | **149** | 纯域名规则集 `rules/campusrun.yaml` 含 102 条无副作用域名 |

覆盖的广告与跳转平台:

| 平台 | 归属 | 代表域名 |
|---|---|---|
| 阿里汇川 / 千问 / 夸克推广 | 阿里 | `qianwen.com`、`quark.cn`、`uc.cn`、`sm.cn`（进程级隔离） |
| 运动世界自家发现流与轮播横幅 | 浙江万航 | `discovery.gxapp.iydsj.com`、`swapp-image.gxapp.iydsj.com`、`fxzb.vip` |
| 腾讯优量汇 | 腾讯 | `gdt.qq.com`、`sdk.e.qq.com` |
| 快手磁力引擎 | 快手 | `kuaishou.com`、`kskwai.com`、`yximgs.com` |
| 穿山甲 / GroMore / 抖音流 | 字节跳动 | `snssdk.com`、`pstatp.com`、`douyin.com`、`bytescm.com` |
| 百度 Mobads | 百度 | `mobads.baidu.com`、`hmma.baidu.com`、`cpro.baidustatic.com` |
| 阿里天目 / 妈妈 | 阿里 | `tianmu.mobi`、`tanx.com`、`alimama.com` |
| 京东广告 | 京东 | `xlog.jd.com`、`dsp-x.jd.com` |
| YFAN AdX | 第三方 | `yfanads.com` |
| AdGain | 第三方 | `adgain.cn` |
| 友盟统计 | 阿里 | `umeng.com`、`umengcloud.com` |
| OTS 线下推广 | 第三方 | `zztfly.com`、`idazhe.net` |
| 厂商广告 SDK | 华为/荣耀/OPPO/小米 | `ads-adnet-drcn.cloud.honor.com` 等 |

---

## 快速开始

### 方式一（推荐已有代理用户）：JS 脚本一键覆写（保留原有机场订阅）

如果你平时已经在用 **FlClash（Android / 桌面端）**、**Clash Verge Rev** 或 **Mihomo Party**，直接导入 [`scripts/campusrun_flclash_script.js`](scripts/campusrun_flclash_script.js) 即可，**无需改动原有代理配置，跑完步也不用手动来回切配置**：

1. 下载 [`scripts/campusrun_flclash_script.js`](scripts/campusrun_flclash_script.js)（也可直接在 Release 页面下载单文件，或复制上方 jsDelivr 直链通过 URL 导入）
2. **第一步（导入脚本库）**：打开 **FlClash** → 底部「**工具**」→「**进阶配置**」→「**脚本**」→ 右上角「**添加**」导入该 `.js` 文件（注：本地文件每次更新需重新导入覆盖；若通过 URL 导入可直接点同步刷新）
3. **第二步（绑定当前订阅生效，必做！）**：点底部「**配置**」→ **长按**你当前正在使用的机场订阅卡片 → 点「**扩展**」→ 将扩展模式从「标准」切为「**脚本**」→ 勾选 `campusrun_flclash_script` → 点右上角「**立即应用**」，并确保主页开启 **VPN（TUN）模式** 与「**规则**」分流即可！

脚本会自动把 47 条 `PROCESS-NAME` 进程隔离规则 + 3 条自家横幅子域 + 99 条纯广告 SDK 规则（共 149 条）无损注入到你现有订阅 `rules` 的最前面（并自动去重），订阅自动更新也不会冲掉规则。

### 方式二：直接导入独立配置（不需要代理）

用 [`configs/standalone.yaml`](configs/standalone.yaml) —— 含一个直连占位节点,
导入后除广告域名被拦截外,其余流量全部直连。

适用于:只想屏蔽广告,不需要科学上网。

### 在线订阅地址(URL 方式)

仓库已托管在 GitHub,可以直接用 URL 引用,不用手动下载:

**Clash rule-provider 地址(GitHub 源):**

`
https://raw.githubusercontent.com/zou-handy/SportWorld-CampusRun-AdBlock/main/rules/campusrun.yaml
`

**国内推荐用 jsDelivr CDN 镜像**(GitHub raw 在国内经常无法访问,CDN 更快更稳):

`
https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/rules/campusrun.yaml
`

**hosts 文件地址:**

`
https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/rules/hosts.txt
`

使用 CDN 地址作为 rule-provider 的示例:

`yaml
rule-providers:
  campusrun:
    type: http
    behavior: domain
    format: yaml
    interval: 86400
    url: 'https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/rules/campusrun.yaml'
`

> 用 URL 方式的好处:规则更新后客户端会自动拉取,不用手动替换文件。

> **关于缓存**:jsDelivr 与 GitHub raw 都有 CDN 缓存(通常几分钟到几小时)。
> 如果想确保拿到最新版本,可以在 URL 后加一个查询参数强制刷新,例如:
> `
> https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@main/rules/campusrun.yaml?v=1
> `
> 或者直接按 commit 哈希引用(永久有效、无缓存延迟):
> `
> https://cdn.jsdelivr.net/gh/zou-handy/SportWorld-CampusRun-AdBlock@<commit>/rules/campusrun.yaml
> `

---

### 方式三:作为规则集叠加

用 [`rules/campusrun.yaml`](rules/campusrun.yaml) 作为 Clash 的 `rule-provider`（注：纯域名规则集含 102 条无副作用域名，已剔除千问/夸克/淘宝/抖音等日常共享域避免全局断网）：

```yaml
rule-providers:
  campusrun:
    type: file
    behavior: domain
    format: yaml
    path: ./ruleset/campusrun.yaml

rules:
  - 'RULE-SET,campusrun,REJECT'   # 必须放在 rules 最前面
  - 'MATCH,你的代理组'             # 你原有的兜底规则保持在最后
```

### 方式四:YAML 合并进现有配置

用 [`configs/prepend-rules.yaml`](configs/prepend-rules.yaml) ——
适合 Clash Verge Rev 的「规则覆写」、mihomo 的 mixin/patch 功能（含完整 149 条规则及进程级防误伤隔离）。

> **如果你用 AI 帮忙合并配置**,请参考 [`docs/ai-prompt.md`](docs/ai-prompt.md),
> 里面写了完整的约束条件(不改节点、不加 MATCH 兜底、不许改成关键词匹配等),
> 可以避免 AI 改坏你的配置。

### 其他格式

- [`rules/domains.txt`](rules/domains.txt) —— 纯域名清单,适合 AdGuard / 路由器 / Pi-hole
- [`rules/hosts.txt`](rules/hosts.txt) —— hosts 格式,适合 AdAway / NetGuard / RethinkDNS

---

## ⚠️ 使用须知

**1. 必须开启 TUN 或 VPN 模式**

只开「系统代理」时,App 的流量不经过 Clash,规则不会生效。这是最常见的失败原因。

**2. 规则必须放在最前面**

Clash 的规则是**按顺序匹配**的。如果广告规则排在后面,前面的规则先命中了,拦截就不会生效。

**3. 不要添加 `MATCH` 兜底规则**

如果你用叠加方式,`prepend` 里**不要**加 `MATCH,xxx`,否则会覆盖你自己配置的兜底规则,
导致所有流量直连、无法代理。本项目提供的 `prepend-rules.yaml` 已经刻意不含兜底规则。

**4. 已刻意剔除的内容(避免误伤)**

- **裸父域**:`baidu.com`、`qq.com`、`sogou.com`、`xiaomi.com` —— 只保留具体广告子域
- **共享基础设施域**:`tracking.miui.com`、`metrics*.data.hicloud.com` 等 10 个
  —— 这些在小米/华为手机上属于系统级上报通道,屏蔽可能连累系统推送
- **核心跑步与风控业务域**:`run.gxapp.iydsj.com`（跑步业务）、`datapoint.gxapp.iydsj.com`（轨迹/PV上报）、`partner.iydsj.com`（极验设备风控校验）、`h5.gxapp.iydsj.com`（成绩/规则 H5）、`gxapp-images.iydsj.com`（头像）、高德地图、个推推送、登录认证域名（注：切勿一刀切屏蔽 `iydsj.com` 根域，仅精准拦截 `discovery.gxapp.iydsj.com` 与 `swapp-image.gxapp.iydsj.com` 两个非核心推广/横幅子域）

---

## 实测效果

单次会话日志统计(31 秒):

| 指标 | 数值 |
|---|---|
| 被拦截的广告连接 | **459 次** |
| 被拦截的广告主机 | **41 个** |
| 放行的业务连接 | 80 次 |
| **拦截率** | **85%** |

被拦截的域名示例:

```
sdk.e.qq.com                            86 次   腾讯优量汇主接口
open.e.kuaishou.com                     57 次   快手磁力
tracker.yfanads.com                     42 次   YFAN 广告追踪
api-access.pangolin-sdk-toutiao.com     38 次   穿山甲
v2mi.gdt.qq.com / mi.gdt.qq.com         63 次   优量汇曝光监测
mobads.baidu.com                        18 次   百度 Mobads
```

---

## 为什么不需要 Root

Android 从 4.0 起提供 **`VpnService`** 机制,普通应用即可创建本地 VPN 接管全部流量,
无需 Root、无需解锁。Clash Meta for Android、Clash Verge Rev 等客户端都基于此机制运行。

本方案**不修改 APK 的任何字节**,因此:

- 应用签名不变,加固方案的完整性校验不会触发
- 可随时一键撤销,不留痕迹
- 应用升级后规则依然有效

---

## 规则是怎么来的

| 来源 | 性质 |
|---|---|
| `res/xml/network_security_config.xml` | 开发者自己明文放行的 10 个广告域名 |
| `res/values/arrays.xml` → `adBlockUrl` | **应用自带的广告黑名单** |
| `assets/gdt_plugin/gdtadv2.jar` | 腾讯优量汇 SDK 本体(未加密) |
| `assets/bdxadsdk.jar` | 百度 Mobads SDK 本体(未加密) |
| `assets/ksad_idc.json` | 快手磁力 SDK 的完整 IDC 域名表 |
| `classes.dex` 明文字符串表 | 其余 SDK 域名与 API 路径 |
| **手机实测日志** | 补充静态分析拿不到的域名(如京东广告链路) |

详细的逆向过程见 [`docs/analysis.md`](docs/analysis.md)。

---

## 技术边界与微服务子域精筛说明

1. **为什么不能一刀切封死 `iydsj.com` 根域，却能干掉自家横幅？**
   - 早期静态分析认为整个 `*.iydsj.com` 都不敢碰；但经真机 Mihomo `:9090` 实时进程连接取证，运动世界后端实际按**微服务子域**拆分：
     - **核心业务与风控（严禁屏蔽）**：`run.gxapp.iydsj.com`（跑步规则与结算）、`datapoint.gxapp.iydsj.com`（实时 GPS 轨迹点上报）、`partner.iydsj.com`（极验 Geetest 防作弊设备校验）、`h5.gxapp.iydsj.com`（成绩单与规则 H5）。
     - **发现流与运营轮播图床（v1.2.0 已精准拦截）**：`discovery.gxapp.iydsj.com`（发现页/社区活动流）、`swapp-image.gxapp.iydsj.com`（首页运营海报图床）、`fxzb.vip`（内置商城）。封禁这 3 个子域即可在不伤跑步和成绩上传的前提下，清空自家运营轮播图。
2. **仅剩的理论边界**：
   - 若未来某次版本把纯文字推广直接塞进 `run.gxapp.iydsj.com` 的同一个跑步配置 JSON 响应里（且不加载 `swapp-image` 外部海报图），网络层无法在不解密 HTTPS 的前提下剥离 JSON 字段，届时可配合界面层工具（如 [GKD](https://github.com/gkd-kit/gkd)）自动点击关闭。

---

## 免责声明

- 本项目仅提供域名拦截规则,用于个人减少广告干扰。
- 规则来源于对公开分发的 APK 包的静态分析,不包含任何反编译代码或 SDK 内容。
- 本项目不修改目标应用,不破解任何付费功能,不绕过任何账号或会员限制。
- 请遵守目标应用的服务条款。使用本规则产生的任何后果由使用者自行承担。

## License

[MIT](LICENSE)
