# Email Proxy Rules (邮箱分流规则集)

专门整理整理的**国内与国外主流邮箱服务器、网页端及邮件收发协议（IMAP / POP3 / SMTP / Exchange）**分流规则集，专为 **Loon** 和 **Clash / Mihomo / OpenClash** 设计。

[![GitHub license](https://img.shields.io/github/license/zhousulong/mail-proxy-rules)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/zhousulong/mail-proxy-rules)](https://github.com/zhousulong/mail-proxy-rules/stargazers)

---

## 目录与文件结构

```text
mail-proxy-rules/
├── loon/
│   ├── Mail_CN.list       # Loon 规则：国内邮箱（网易/QQ/新浪/搜狐/阿里/运营商等）
│   ├── Mail_Global.list   # Loon 规则：国外邮箱（Gmail/Outlook/iCloud/Proton/Yahoo等）
│   └── Mail_All.list      # Loon 规则：国内 + 国外邮箱全集
├── clash/
│   ├── Mail_CN.yaml       # Clash Rule-Provider (YAML 格式)：国内邮箱
│   ├── Mail_Global.yaml   # Clash Rule-Provider (YAML 格式)：国外邮箱
│   ├── Mail_All.yaml      # Clash Rule-Provider (YAML 格式)：国内外邮箱全集
│   ├── Mail_CN.txt        # Clash / Classical 格式：国内邮箱
│   ├── Mail_Global.txt    # Clash / Classical 格式：国外邮箱
│   └── Mail_All.txt       # Clash / Classical 格式：国内外邮箱全集
└── README.md
```

---

## 包含的邮箱服务清单

### 1. 国内邮箱 (Mail CN)
- **网易邮箱**：163.com、126.com、yeah.net、网易企业邮箱 (qiye.163.com) 及对应 pop/imap/smtp 节点
- **腾讯邮箱**：QQ 邮箱 (qq.com)、Foxmail (foxmail.com)、腾讯企业邮 (exmail.qq.com)
- **新浪邮箱**：新浪免费/VIP邮箱 (sina.com, sina.cn, vip.sina.com)
- **搜狐邮箱**：搜狐免费/VIP邮箱 (sohu.com, vip.sohu.com)
- **阿里企业邮 / 钉邮**：aliyun.com、alimail.com、mxhichina.com、dingtalk.com
- **运营商邮箱**：中国移动 139 邮箱 (139.com)、中国电信 189 邮箱 (189.cn)、中国联通沃邮箱 (wo.cn)
- **其他知名邮箱**：263 企业邮箱、TOM 邮箱 (tom.com, 163.net)、21CN 邮箱、Coremail 节点

### 2. 国外邮箱 (Mail Global)
- **Google**：Gmail (gmail.com, googlemail.com)、imap/smtp/pop.gmail.com
- **Microsoft**：Outlook / Hotmail / Live / Office 365 (outlook.com, hotmail.com, office365.com, live.com)
- **Apple**：iCloud 邮件 (icloud.com, me.com, mac.com, mail.me.com)
- **Yahoo**：Yahoo Mail (yahoo.com, ymail.com, rocketmail.com)
- **Proton**：ProtonMail (proton.me, protonmail.com, pm.me)
- **Tuta**：Tutanota / Tuta Mail (tuta.com, tutanota.com, tutamail.com)
- **Zoho**：Zoho Mail 国际版 (zoho.com, zoho.eu)
- **Fastmail**：Fastmail (fastmail.com, messagingengine.com)
- **欧洲/德国**：Mail.com、GMX (gmx.com, gmx.net, gmx.de)、Mailbox.org、Posteo
- **俄罗斯**：Yandex Mail (yandex.com, yandex.ru)、Mail.ru
- **日韩及其他**：AOL (aol.com)、Naver Mail (naver.com)、Daum / Kakao、Hey.com、Runbox

---

## 订阅与配置方法

> **CDN 加速提示**：在国内网络环境下，你可以将 GitHub Raw 链接替换为 jsDelivr / Fastly 等加速链接，如：
> `https://fastly.jsdelivr.net/gh/zhousulong/mail-proxy-rules@main/clash/Mail_Global.yaml`

### 1. Loon 配置示例

在 Loon 的 `[Remote Rule]` 中添加：

```ini
[Remote Rule]
# 国内邮箱直连
https://raw.githubusercontent.com/zhousulong/mail-proxy-rules/main/loon/Mail_CN.list, policy=DIRECT, tag=Mail_CN, enabled=true

# 国外邮箱走节点/代理
https://raw.githubusercontent.com/zhousulong/mail-proxy-rules/main/loon/Mail_Global.list, policy=PROXY, tag=Mail_Global, enabled=true
```

---

### 2. Clash / Mihomo / OpenClash 配置示例

在配置文件的 `rule-providers` 与 `rules` 区域引用：

```yaml
rule-providers:
  Mail_CN:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/zhousulong/mail-proxy-rules/main/clash/Mail_CN.yaml"
    path: ./ruleset/Mail_CN.yaml
    interval: 86400

  Mail_Global:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/zhousulong/mail-proxy-rules/main/clash/Mail_Global.yaml"
    path: ./ruleset/Mail_Global.yaml
    interval: 86400

rules:
  - RULE-SET,Mail_CN,DIRECT
  - RULE-SET,Mail_Global,PROXY
  # 其他规则...
  - MATCH,DIRECT
```

---

## 协议与开源

本项目规则基于开源协议公开维护，欢迎提交 Issue 或 Pull Request 补充遗漏的邮箱服务或专用接入端点。
