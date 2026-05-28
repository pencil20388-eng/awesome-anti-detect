# 🛡️ Awesome Anti-Detect & Browser Privacy

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

[English](./README.md) | [中文文档](./README_CN.md)

> A curated list of antidetect browsers, browser fingerprinting resources, multi-account tools, privacy research, and automation frameworks. Updated regularly.

Whether you manage multiple accounts for e-commerce, social media, ad operations, or web scraping — this is the reference guide for the tools, research, and best practices in the anti-detection space.

---

## Contents

- [Antidetect Browsers](#antidetect-browsers)
- [Browser Fingerprinting](#browser-fingerprinting)
- [Fingerprint Testing Tools](#fingerprint-testing-tools)
- [Proxy Services](#proxy-services)
- [Automation & API Integration](#automation--api-integration)
- [AI Agent Skills for Browser Automation](#ai-agent-skills-for-browser-automation)
- [Research & Papers](#research--papers)
- [Articles & Guides](#articles--guides)
- [Communities](#communities)
- [Related Awesome Lists](#related-awesome-lists)

---

## Antidetect Browsers

Browsers that create isolated profiles with unique fingerprints for each session.

| Browser | Engines | Free Tier | API | Highlights |
|---------|---------|-----------|-----|------------|
| [AdsPower](https://www.adspower.net/) | Chromium (Sun) + Firefox (Flower) | 5 profiles | ✅ Local API | 9M+ users, RPA builder, multi-window sync, team collaboration. Best automation API in the category. [API Docs](https://localapi-doc-en.adspower.com/) |
| [Multilogin](https://multilogin.com/) | Mimic (Chromium) + Stealthfox (Firefox) | No | ✅ | Built-in residential proxies, enterprise-grade fingerprinting |
| [GoLogin](https://gologin.com/) | Orbita (Chromium) | 3 profiles | ✅ | Built-in proxy traffic, mobile profiles, clean UI |
| [Dolphin Anty](https://dolphin-anty.com/) | Chromium | 10 profiles | ✅ | Popular with affiliate marketers, team features |
| [Octo Browser](https://octobrowser.net/) | Chromium | No | ✅ | Kernel-level fingerprint management, modern UI |
| [Incogniton](https://incogniton.com/) | Chromium + Firefox | 10 profiles | ✅ | Selenium/Puppeteer integration, cookie management |
| [Kameleo](https://kameleo.io/) | Chromium + Firefox + WebKit | No | ✅ | Mobile fingerprinting (Android/iOS), local proxy |
| [Linken Sphere](https://ls.tenebris.cc/) | Chromium | No | Limited | High-end, advanced config builder |
| [VMLogin](https://www.vmlogin.us/) | Chromium | 3 profiles | ✅ | Cloud profiles, Selenium/Puppeteer support |
| [BitBrowser](https://www.bitbrowser.net/) | Chromium | 10 profiles | ✅ | Budget option, RPA support |

## Browser Fingerprinting

Understanding what makes each browser unique.

### What Gets Fingerprinted

| Attribute | Uniqueness | Spoofable? |
|-----------|-----------|------------|
| Canvas rendering | High | Yes (noise injection) |
| WebGL parameters | High | Yes (parameter spoofing) |
| AudioContext | High | Yes |
| Installed fonts | High | Yes (font list override) |
| User-Agent string | Low | Yes |
| Screen resolution | Medium | Yes |
| WebRTC (real IP) | Critical | Yes (disable/mask) |
| Hardware concurrency (CPU cores) | Medium | Yes |
| Device memory | Medium | Yes |
| Timezone | Low | Yes (auto-match to proxy) |
| Language | Low | Yes |
| Platform / OS | Low | Yes |

### Key Concepts

**Fingerprint consistency** — A fingerprint must be internally coherent. A Windows User-Agent with macOS fonts will trigger detection. Timezone must match proxy geolocation. GPU reported in WebGL must match the claimed OS.

**Fingerprint uniqueness** — Each browser profile needs a unique fingerprint. If 50 accounts share the same canvas hash, they'll be linked and banned together.

**Session isolation** — Cookies, localStorage, IndexedDB, and service workers must be completely separate between profiles. Incognito mode does NOT achieve this.

**Behavioral fingerprinting** — Beyond static attributes, platforms track typing patterns, mouse movements, scroll behavior, and navigation timing. Advanced antidetect browsers simulate human-like behavioral patterns.

## Fingerprint Testing Tools

Test and verify your browser fingerprint configuration.

| Tool | What it checks | URL |
|------|---------------|-----|
| BrowserScan | Comprehensive fingerprint scan, leak detection | [browserscan.net](https://www.browserscan.net/) |
| BrowserLeaks | Canvas, WebGL, WebRTC, fonts, audio | [browserleaks.com](https://browserleaks.com/) |
| AmIUnique | Fingerprint uniqueness comparison | [amiunique.org](https://amiunique.org/) |
| Cover Your Tracks (EFF) | Tracking protection assessment | [coveryourtracks.eff.org](https://coveryourtracks.eff.org/) |
| CreepJS | Advanced fingerprint detection | [abrahamjuliot.github.io/creepjs](https://abrahamjuliot.github.io/creepjs/) |
| Pixelscan | Bot detection and fingerprint analysis | [pixelscan.net](https://pixelscan.net/) |
| IPHey | IP, DNS leak, WebRTC leak check | [iphey.com](https://iphey.com/) |

## Proxy Services

Proxies are essential — your fingerprint is only half the equation without a clean IP.

### Proxy Types

| Type | Speed | Cost | Detection Risk | Best For |
|------|-------|------|----------------|----------|
| Datacenter | Fast | Low | High | Scraping, testing |
| Residential (rotating) | Medium | Medium | Low | Multi-account, ads |
| Residential (static/ISP) | Fast | Higher | Very Low | Long-lived accounts |
| Mobile (4G/5G) | Variable | Highest | Lowest | Social media, high-security platforms |

### Choosing Proxies for Multi-Account

- One IP per account (never share IPs between accounts)
- Match proxy geolocation to the account's claimed location
- Residential or mobile for platforms with strict detection (Facebook, Google, Amazon)
- Static/ISP proxies for accounts that need consistent IP over time
- Test proxy quality before binding: check for blacklists, previous abuse, subnet diversity

## Automation & API Integration

Connect automation frameworks to antidetect browsers.

### AdsPower Local API

The most complete API in the antidetect browser space. Full documentation: [localapi-doc-en.adspower.com](https://localapi-doc-en.adspower.com/)

```python
import requests

API_KEY = "your_key"
BASE = "http://local.adspower.net:50325"
HEADERS = {"Authorization": f"Bearer {API_KEY}"}

# Open a profile
resp = requests.get(f"{BASE}/api/v1/browser/start?user_id=PROFILE_ID", headers=HEADERS).json()
ws_puppeteer = resp["data"]["ws"]["puppeteer"]       # For Playwright
selenium_addr = resp["data"]["ws"]["selenium"]        # For Selenium
webdriver_path = resp["data"]["webdriver"]             # ChromeDriver path
```

Ready-to-use scripts: [awesome-adspower-automation](https://github.com/pencil20388-eng/awesome-adspower-automation)

### Framework Compatibility

| Framework | AdsPower | Multilogin | GoLogin | Dolphin Anty |
|-----------|----------|------------|---------|-------------|
| Selenium | ✅ | ✅ | ✅ | ✅ |
| Playwright | ✅ | ✅ | ✅ | ✅ |
| Puppeteer | ✅ | ✅ | ✅ | ✅ |
| Chrome DevTools MCP | ✅ | ✅ | ❓ | ❓ |

### AI Agent Skills

| Skill | What it does | Repo |
|-------|-------------|------|
| AdsPower Skill | Manage profiles, proxies, cookies via natural language | [adspower-skill](https://github.com/pencil20388-eng/adspower-skill) |
| Browser Automation Skills | Playwright, Selenium, Puppeteer, scraping, fingerprinting skills | [browser-automation-skills](https://github.com/pencil20388-eng/browser-automation-skills) |
| Chrome DevTools MCP + AdsPower | AI-powered browser debugging across antidetect profiles | [Guide](https://github.com/pencil20388-eng/browser-automation-skills) |

## Research & Papers

Academic and industry research on browser fingerprinting and anti-detection.

- [FPDetective: Dusting the Web for Fingerprinters](https://dl.acm.org/doi/10.1145/2508859.2516674) — CCS 2013, first large-scale study of web fingerprinting
- [How Unique Is Your Web Browser?](https://www.eff.org/files/2024/02/27/browser-uniqueness.pdf) — EFF Panopticlick study on browser uniqueness
- [FP-Inspector: Browser Fingerprinting Detection](https://arxiv.org/abs/2003.04281) — Machine learning approach to detecting fingerprinting scripts
- [Browser Fingerprinting: A Survey](https://arxiv.org/abs/1905.01051) — Comprehensive survey of fingerprinting techniques
- [Hiding in the Crowd: Browser Fingerprint Evasion](https://dl.acm.org/doi/10.1145/3485832.3485889) — Analysis of how antidetect tools work
- [IMC '24: Antidetect Browser Consistency Study](https://www.adspower.com/blog/imc-antidetect-research) — ASU & Amazon research, AdsPower was the only browser to pass kernel-level consistency tests

## Articles & Guides

Practical guides for multi-account management and anti-detection.

### Getting Started
- [What is an Antidetect Browser and Why Do You Need One?](https://www.adspower.net/blog/what-is-antidetect-browser)
- [Browser Fingerprinting Explained](https://browserleaks.com/canvas)
- [Multi-Account Management Best Practices](https://www.adspower.net/blog)

### Technical Deep Dives
- [Canvas Fingerprinting: How It Works](https://browserleaks.com/canvas)
- [WebRTC Leak Prevention](https://browserleaks.com/webrtc)
- [How Platforms Detect Multiple Accounts](https://www.adspower.net/blog)

### Automation
- [AdsPower API: Getting Started (Zero to Hero)](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/getting-started.md)
- [Selenium + AdsPower Integration](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/selenium-integration.md)
- [Playwright + AdsPower Integration](https://github.com/pencil20388-eng/awesome-adspower-automation/blob/main/guides/playwright-integration.md)

## Communities

Where practitioners discuss anti-detection techniques and multi-account management.

- [r/antidetect](https://www.reddit.com/r/antidetect/) — Reddit community
- [r/webscraping](https://www.reddit.com/r/webscraping/) — Web scraping community (overlapping audience)
- [BlackHatWorld](https://www.blackhatworld.com/) — Digital marketing forum with antidetect discussions
- [AdsPower Community](https://community.adspower.com/) — Official AdsPower user community
- [Affiliate Fix](https://affiliatefix.com/) — Affiliate marketing forum

## Related Awesome Lists

- [awesome-web-scraping](https://github.com/lorien/awesome-web-scraping) — Web scraping tools and resources
- [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) — Self-hosted alternatives
- [awesome-privacy](https://github.com/pluja/awesome-privacy) — Privacy-focused tools
- [awesome-adspower-automation](https://github.com/pencil20388-eng/awesome-adspower-automation) — AdsPower automation scripts and guides

---

## Contributing

Found a missing tool, paper, or resource? PRs welcome!

1. Fork this repo
2. Add your resource to the relevant section
3. Open a Pull Request

Please keep entries factual and avoid promotional language.

## About the Maintainer

Maintained by the content team at [AdsPower](https://www.adspower.net/) — the antidetect browser for multi-account management. We track this space professionally and update this list regularly.

## License

[MIT](LICENSE)

---

**⭐ Star this repo to stay updated — new resources added regularly.**
