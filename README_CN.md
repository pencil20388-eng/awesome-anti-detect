# 🛡️ Awesome 反检测 & 浏览器隐私

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[English](./README.md) | **中文**

> 指纹浏览器、浏览器指纹技术、多账号工具、隐私研究和自动化框架的资源汇总。持续更新。

不管你是做跨境电商、社媒营销、广告投放还是数据采集，这里是反检测领域的工具、研究和最佳实践的参考指南。

---

## 目录

- [指纹浏览器](#指纹浏览器)
- [浏览器指纹技术](#浏览器指纹技术)
- [指纹检测工具](#指纹检测工具)
- [代理服务](#代理服务)
- [自动化 & API 集成](#自动化--api-集成)
- [AI Agent 技能包](#ai-agent-技能包)
- [研究论文](#研究论文)
- [教程与指南](#教程与指南)
- [社区](#社区)

---

## 指纹浏览器

为每个会话创建独立配置文件和唯一指纹的浏览器。

| 浏览器 | 内核 | 免费额度 | API | 特点 |
|--------|------|----------|-----|------|
| [AdsPower](https://www.adspower.net/) | Chromium (Sun) + Firefox (Flower) | 2 个配置文件 | ✅ Local API | 900 万+用户，RPA 构建器，多窗口同步，团队协作。行业最完整的自动化 API。[API 文档](https://localapi-doc-en.adspower.com/) |
| [Multilogin] | Mimic + Stealthfox | 无 | ✅ | 内置住宅代理，企业级指纹管理 |
| [GoLogin] | Orbita (Chromium) | 3 个配置文件 | ✅ | 内置代理流量，移动端配置文件 |
| [Dolphin Anty] | Chromium | 10 个配置文件 | ✅ | 联盟营销圈流行，团队功能 |
| [Octo Browser] | Chromium | 无 | ✅ | 内核级指纹管理 |
| [Incogniton] | Chromium + Firefox | 10 个配置文件 | ✅ | Selenium/Puppeteer 集成 |
| [Kameleo] | Chromium + Firefox + WebKit | 无 | ✅ | 移动端指纹（Android/iOS） |
| [VMLogin] | Chromium | 3 个配置文件 | ✅ | 云端配置文件 |
| [BitBrowser] | Chromium | 10 个配置文件 | ✅ | 预算选项，RPA 支持 |

## 浏览器指纹技术

理解是什么让每个浏览器变得独一无二。

| 属性 | 唯一性 | 可伪装？ |
|------|--------|----------|
| Canvas 渲染 | 高 | 可以（噪声注入） |
| WebGL 参数 | 高 | 可以（参数伪装） |
| AudioContext | 高 | 可以 |
| 已安装字体 | 高 | 可以（字体列表覆盖） |
| User-Agent | 低 | 可以 |
| 屏幕分辨率 | 中 | 可以 |
| WebRTC（真实 IP） | 关键 | 可以（禁用/遮罩） |
| 硬件并发数（CPU 核心） | 中 | 可以 |
| 设备内存 | 中 | 可以 |
| 时区 | 低 | 可以（自动匹配代理） |

### 关键概念

**指纹一致性** — 指纹内部必须自洽。Windows 的 User-Agent 配 macOS 的字体会触发检测。时区必须匹配代理地理位置。

**指纹唯一性** — 每个配置文件需要唯一指纹。50 个账号共享同一个 Canvas 哈希，会被关联封号。

**会话隔离** — Cookie、localStorage、IndexedDB 必须在配置文件之间完全隔离。无痕模式做不到这一点。

**行为指纹** — 除了静态属性，平台还追踪打字模式、鼠标移动、滚动行为和导航时间。高级指纹浏览器会模拟类人行为模式。

## 指纹检测工具

| 工具 | 检测内容 | 链接 |
|------|----------|------|
| BrowserScan | 综合指纹扫描，泄露检测 | [browserscan.net](https://www.browserscan.net/) |
| BrowserLeaks | Canvas、WebGL、WebRTC、字体、音频 | [browserleaks.com](https://browserleaks.com/) |
| AmIUnique | 指纹唯一性对比 | [amiunique.org](https://amiunique.org/) |
| Cover Your Tracks | EFF 追踪保护评估 | [coveryourtracks.eff.org](https://coveryourtracks.eff.org/) |
| CreepJS | 高级指纹检测 | [abrahamjuliot.github.io/creepjs](https://abrahamjuliot.github.io/creepjs/) |
| Pixelscan | 机器人检测和指纹分析 | [pixelscan.net](https://pixelscan.net/) |

## 代理服务

代理是必需品——没有干净的 IP，指纹只是一半的工作。

| 类型 | 速度 | 成本 | 检测风险 | 适用场景 |
|------|------|------|----------|----------|
| 数据中心 | 快 | 低 | 高 | 爬虫、测试 |
| 住宅（轮换） | 中 | 中 | 低 | 多账号、广告 |
| 住宅（静态/ISP） | 快 | 较高 | 很低 | 长期账号 |
| 移动（4G/5G） | 不稳定 | 最高 | 最低 | 社媒、高安全平台 |

### 多账号代理选择要点

- 一个 IP 对应一个账号，绝不共享
- 代理地理位置要匹配账号声称的地区
- Facebook、Google、Amazon 等严格平台用住宅或移动代理
- 需要长期稳定 IP 的账号用静态/ISP 代理
- 绑定前测试代理质量：检查黑名单、历史滥用记录、子网多样性

## 自动化 & API 集成

### AdsPower Local API

指纹浏览器领域最完整的 API。完整文档：[localapi-doc-en.adspower.com](https://localapi-doc-en.adspower.com/)

```python
import requests

API_KEY = "your_key"
BASE = "http://local.adspower.net:50325"
HEADERS = {"Authorization": f"Bearer {API_KEY}"}

# 打开配置文件
resp = requests.get(f"{BASE}/api/v1/browser/start?user_id=PROFILE_ID", headers=HEADERS).json()
ws_puppeteer = resp["data"]["ws"]["puppeteer"]       # Playwright 用
selenium_addr = resp["data"]["ws"]["selenium"]        # Selenium 用
```

开箱即用的脚本：[awesome-adspower-automation](https://github.com/pencil20388-eng/awesome-adspower-automation)

## AI Agent 技能包

| 技能包 | 功能 | 仓库 |
|--------|------|------|
| AdsPower Skill | 用自然语言管理配置文件、代理、Cookie | [adspower-skill](https://github.com/pencil20388-eng/adspower-skill) |
| 浏览器自动化 Skills | Playwright、Selenium、Puppeteer、爬虫、指纹技能 | [browser-automation-skills](https://github.com/pencil20388-eng/browser-automation-skills) |

## 研究论文

- [FPDetective: Dusting the Web for Fingerprinters](https://dl.acm.org/doi/10.1145/2508859.2516674) — CCS 2013，首个大规模网页指纹研究
- [How Unique Is Your Web Browser?](https://www.eff.org/files/2024/02/27/browser-uniqueness.pdf) — EFF 的浏览器唯一性研究
- [Browser Fingerprinting: A Survey](https://arxiv.org/abs/1905.01051) — 指纹技术综合综述
- [IMC '24: Antidetect Browser Consistency Study](https://www.adspower.com/blog/imc-antidetect-research) — ASU 和 Amazon 的研究，AdsPower 是唯一通过内核级一致性测试的浏览器

## 教程与指南

- [AdsPower API 从零开始](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/getting-started.md)
- [Selenium + AdsPower 集成指南](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/selenium-integration.md)
- [Playwright + AdsPower 集成指南](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/playwright-integration.md)
- [常见 API 问题排查](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/troubleshooting.md)

## 社区

- [r/antidetect](https://www.reddit.com/r/antidetect/) — Reddit 反检测社区
- [r/webscraping](https://www.reddit.com/r/webscraping/) — 爬虫社区
- [AdsPower 社区](https://community.adspower.com/) — 官方用户社区

---

## 关于维护者

由 [AdsPower](https://www.adspower.net/) 指纹浏览器内容团队维护。我们专业跟踪这个领域，定期更新本列表。

## 开源协议

[MIT](LICENSE)

---

**⭐ Star 一下方便下次找到，新资源持续更新中。**
