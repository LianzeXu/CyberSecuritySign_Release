# CyberSecuritySign

**CyberSecuritySign** is a Python-based cybersecurity utility for **RSA2048-PSS-SHA256 key generation, public key parsing, XML-driven S19 signing, XML-driven public key patching/verification, and XML-driven signature verification**.

**CyberSecuritySign** 是一个基于 Python 的网络安全工具，用于 **RSA2048-PSS-SHA256 密钥生成、公钥解析、基于 XML 配置的 S19 签名、公钥补丁/校验，以及签名验证**。

---

## 📌 Project Information / 项目信息

| Item | Value |
|---|---|
| Tool Name / 工具名称 | `CyberSecuritySign.py` / `CyberSecuritySign.exe` |
| Author / 作者 | `XU LIANZE` |
| Version / 版本 | `V2.0` |
| Main Algorithm / 主算法 | `RSA2048-PSS-SHA256` |
| Key Length / 密钥长度 | `2048 bit` |
| Hash / 哈希算法 | `SHA256` |
| MGF / 掩码生成函数 | `MGF1-SHA256` |
| PSS Salt Length / PSS 盐长度 | `32 bytes` |
| Public Exponent / 公钥指数 | `0x10001 / 65537` |
| Main Input Format / 主要输入格式 | `Motorola S-record / S19` |
| Configuration Format / 配置格式 | `XML` |

---

## 📖 Table of Contents / 目录

- [CyberSecuritySign](#cybersecuritysign)
  - [📌 Project Information / 项目信息](#-project-information--项目信息)
  - [🔎 Overview / 工具概述](#-overview--工具概述)
  - [🆕 V2.0 Major Changes / V2.0 主要变化](#-v20-major-changes--v20-主要变化)
  - [✨ Main Features / 主要功能](#-main-features--主要功能)
  - [🖥 GUI Layout / 图形界面布局](#-gui-layout--图形界面布局)
  - [⚙️ Installation / 安装](#️-installation--安装)
  - [🚀 Quick Start / 快速开始](#-quick-start--快速开始)
  - [💻 CLI Usage / 命令行用法](#-cli-usage--命令行用法)
  - [🔐 RSA2048-PSS-SHA256 Signing Principle / 签名原理](#-rsa2048-pss-sha256-signing-principle--签名原理)
  - [🧩 XML Configuration Overview / XML 配置总览](#-xml-configuration-overview--xml-配置总览)
  - [📝 XML Format and How to Fill It / XML 格式与填写方法](#-xml-format-and-how-to-fill-it--xml-格式与填写方法)
  - [🧭 ID2 XML Signing Configuration / ID2 XML 签名配置](#-id2-xml-signing-configuration--id2-xml-签名配置)
  - [🔑 ID3 XML Public Key Verification Configuration / ID3 XML 公钥校验配置](#-id3-xml-public-key-verification-configuration--id3-xml-公钥校验配置)
  - [🩹 ID4 XML Public Key Patch Configuration / ID4 XML 公钥补丁配置](#-id4-xml-public-key-patch-configuration--id4-xml-公钥补丁配置)
  - [✅ ID5 XML Signature Verification Configuration / ID5 XML 签名验证配置](#-id5-xml-signature-verification-configuration--id5-xml-签名验证配置)
  - [🗂 HM0 Public Key Storage in S19 / HM0 公钥在 S19 中的存储格式](#-hm0-public-key-storage-in-s19--hm0-公钥在-s19-中的存储格式)
  - [🔁 ARXML and S19 Key Mapping / ARXML 与 S19 公钥映射关系](#-arxml-and-s19-key-mapping--arxml-与-s19-公钥映射关系)
  - [🔑 Public Key Formats / 公钥格式说明](#-public-key-formats--公钥格式说明)
  - [✅ Signature Verification Flow / 签名验证流程](#-signature-verification-flow--签名验证流程)
  - [🧪 Troubleshooting / 常见问题](#-troubleshooting--常见问题)
  - [📦 Packaging to EXE / 打包为 EXE](#-packaging-to-exe--打包为-exe)
  - [📁 Suggested Repository Structure / 推荐仓库结构](#-suggested-repository-structure--推荐仓库结构)
  - [⚠️ Encryption vs Signing / 加密与签名说明](#️-encryption-vs-signing--加密与签名说明)
  - [🛡 Security Notes / 安全注意事项](#-security-notes--安全注意事项)
  - [📜 Disclaimer / 免责声明](#-disclaimer--免责声明)

---

## 🔎 Overview / 工具概述

### English

`CyberSecuritySign` is designed for automotive ECU cybersecurity workflows where firmware images are stored as **Motorola S-record / S19** files.

It supports:

- Generating RSA2048 key pairs
- Parsing public keys
- Signing S19 firmware images based on XML configuration
- Verifying signed S19 files based on XML configuration
- Checking whether a public key stored in S19 matches a private key
- Patching public key storage in S19
- Mapping public key data between PEM, DER HEX, ARXML-style values, and S19 memory layout

In V2.0, project-specific addresses and layouts are no longer hard-coded in Python.  
They are moved into XML configuration.

### 中文

`CyberSecuritySign` 面向汽车 ECU 网络安全刷写场景，主要处理 **Motorola S-record / S19** 格式固件文件。

它支持：

- 生成 RSA2048 密钥对
- 解析公钥
- 根据 XML 配置对 S19 固件进行签名
- 根据 XML 配置验证已签名 S19 文件
- 校验 S19 中存储的公钥是否与某个私钥匹配
- 修补 / 替换 S19 中存储的公钥
- 在 PEM、DER HEX、ARXML 数组格式、S19 内存布局之间转换公钥格式

在 V2.0 中，项目相关地址和布局不再写死在 Python 代码中。  
它们被移动到了 XML 配置文件中。

---

## 🆕 V2.0 Major Changes / V2.0 主要变化

| Item | V1.x | V2.0 |
|---|---|---|
| Signing address / 签名地址 | Hard-coded in Python / 写死在代码中 | Loaded from XML / 从 XML 加载 |
| Signature sections / 签名区域 | Fixed | XML configurable |
| Signature outputs / 签名输出 | Fixed | XML configurable |
| Public key storage / 公钥存储布局 | Fixed | XML configurable |
| ID2 / 签名 | Fixed address signing | XML-driven signing |
| ID3 / 公钥匹配校验 | Fixed public key address | XML-driven public key storage |
| ID4 / 公钥 patch | Fixed public key address | XML-driven public key storage |
| ID5 / 签名验证 | Fixed signature layout | XML-driven verification |

---

## ✨ Main Features / 主要功能

| Feature | English | 中文 |
|---|---|---|
| `RSA2048_KEY_GEN` | Generate RSA2048 private/public key pair | 生成 RSA2048 私钥/公钥对 |
| `0U0_SIGN` | XML-driven S19 signing | 基于 XML 的 S19 签名 |
| `0U0_SIGN_VERIFY` | XML-driven signed S19 verification | 基于 XML 的 S19 签名验证 |
| `PUBLIC_KEY_PARSER` | Parse public key PEM or DER HEX | 解析公钥 PEM 或 DER HEX |
| `HM0_PUB_KEY_PATCH` | XML-driven public key storage patch | 基于 XML 的公钥存储补丁 |
| `HM0_PUB_KEY_VERIFY` | XML-driven public key/private key matching check | 基于 XML 的公钥/私钥匹配校验 |
| `Log` | View and save operation logs | 查看并保存日志 |
| `HELP_AND_VERSION` | Show help and version information | 查看帮助和版本信息 |

---

## 🖥 GUI Layout / 图形界面布局

```text
CyberSecuritySign
├─ RSA2048_KEY_GEN
├─ 0U0_SIGN
├─ 0U0_SIGN_VERIFY
├─ OTHER_TOOLS
│  ├─ PUBLIC_KEY_PARSER
│  ├─ HM0_PUB_KEY_PATCH
│  ├─ HM0_PUB_KEY_VERIFY
│  └─ Log
└─ HELP_AND_VERSION
```

---

## ⚙️ Installation / 安装

### Requirements / 环境要求

- Python `3.8+`
- `cryptography`
- Tkinter
  - Windows Python usually includes Tkinter by default.
  - Linux may require installing `python3-tk`.

### Install dependency / 安装依赖

```bash
pip install cryptography
```

For Linux, if Tkinter is missing:

```bash
sudo apt-get install python3-tk
```

---

## 🚀 Quick Start / 快速开始

### Start GUI / 启动图形界面

```bash
python CyberSecuritySign.py
```

or:

```bash
python CyberSecuritySign.py -g
```

If packaged as EXE:

```bash
CyberSecuritySign.exe
```

### Show version / 查看版本

```bash
python CyberSecuritySign.py -v
```

Output:

```text
CyberSecuritySign
Author : XU LIANZE
Version: V2.0
```

### Show help / 查看帮助

```bash
python CyberSecuritySign.py -h
```

---

## 💻 CLI Usage / 命令行用法

### Strict CLI Rules / 严格命令行规则

English:

- `-h` must be used alone.
- `-g` must be used alone.
- `-v` must be used alone.
- If no argument is provided, GUI mode starts by default.
- Unknown parameters are not allowed.
- CLI parameter names must exactly match the documented format.

中文：

- `-h` 必须单独使用。
- `-g` 必须单独使用。
- `-v` 必须单独使用。
- 不带参数时默认启动 GUI。
- 不允许使用未知参数。
- 命令行参数名称必须与文档完全一致。

---

### ID 0 - Generate RSA2048 Key Pair / 生成 RSA2048 密钥对

```bash
python CyberSecuritySign.py -id=0 -opub=public_key.pem -opri=private_key.pem
```

Output:

```text
public_key.pem
private_key.pem
```

---

### ID 1 - Parse Public Key PEM / 解析公钥 PEM

```bash
python CyberSecuritySign.py -id=1 -ipub=public_key.pem
```

Prints:

- `public_key_hex`
- `public_key_mod`
- `public_key_mod_bg`
- `public_key_mod_lt`
- `public_key_mod_jf_lt`

---

### ID 2 - XML-driven S19 Signing / 基于 XML 的 S19 签名

```bash
python CyberSecuritySign.py -id=2 -ixml=config.xml -is19=input.s19 -os19=output_signed.s19 -ipri=private_key.pem
```

---

### ID 3 - XML-driven Public Key Verification / 基于 XML 的公钥匹配校验

```bash
python CyberSecuritySign.py -id=3 -ixml=config.xml -is19=input_key.s19 -ipri=private_key.pem
```

This checks whether:

```text
public key stored in S19 == public key derived from private key PEM
```

即检查：

```text
S19 中存储的公钥 == 私钥 PEM 推导出的公钥
```

---

### ID 4 - XML-driven Public Key Patch / 基于 XML 的公钥补丁

```bash
python CyberSecuritySign.py -id=4 -ixml=config.xml -is19=input_key.s19 -ipub=public_key.pem -os19=output_key_patched.s19
```

---

### ID 5 - XML-driven Signed S19 Verification / 基于 XML 的签名验证

```bash
python CyberSecuritySign.py -id=5 -ixml=config.xml -is19key=key.s19 -is19sign=signed.s19
```

---

## 🔐 RSA2048-PSS-SHA256 Signing Principle / 签名原理

### English

The signing process is:

```text
Read XML configuration
        ↓
Read required S19 data ranges
        ↓
Build XML-defined sign source
        ↓
Calculate SHA256 for logging/debugging
        ↓
Sign using RSA2048-PSS-SHA256 private key
        ↓
Write fixed outputs and signature outputs
        ↓
Save new signed S19
```

Algorithm details:

| Item | Value |
|---|---|
| RSA key length | 2048 bit |
| Signature length | 256 bytes / `0x100` |
| Padding | RSA-PSS |
| Hash | SHA256 |
| MGF | MGF1-SHA256 |
| Salt length | 32 bytes |

The cryptographic call is equivalent to:

```python
private_key.sign(
    sign_source,
    padding.PSS(
        mgf=padding.MGF1(hashes.SHA256()),
        salt_length=32
    ),
    hashes.SHA256()
)
```

Because RSA-PSS uses random salt, signing the same data multiple times may produce different signatures. This is normal.

### 中文

签名流程如下：

```text
读取 XML 配置
        ↓
读取 S19 中指定地址范围的数据
        ↓
构造 XML 定义的签名源数据
        ↓
计算 SHA256 供日志和调试使用
        ↓
使用 RSA2048-PSS-SHA256 私钥签名
        ↓
写入固定输出和签名输出
        ↓
保存新的已签名 S19
```

算法参数：

| 项目 | 值 |
|---|---|
| RSA 密钥长度 | 2048 bit |
| 签名长度 | 256 bytes / `0x100` |
| 填充方式 | RSA-PSS |
| 哈希算法 | SHA256 |
| MGF | MGF1-SHA256 |
| Salt length | 32 bytes |

由于 RSA-PSS 使用随机 salt，因此同一个文件、同一个私钥，多次签名的签名值可能不同，这是正常现象。

---

## 🧩 XML Configuration Overview / XML 配置总览

### English

V2.0 uses one XML file to configure different operations.

Recommended structure:

```xml
<CYBER_SECURITY_SIGN_CONFIG>
    <ID2>
        <!-- S19 signing configuration -->
    </ID2>

    <ID3>
        <!-- Public key verification configuration -->
    </ID3>

    <ID4>
        <!-- Public key patch configuration -->
    </ID4>

    <ID5>
        <!-- Signed S19 verification configuration -->
    </ID5>
</CYBER_SECURITY_SIGN_CONFIG>
```

The tool searches the required root node by operation ID:

| CLI ID | Required XML Node | Purpose |
|---|---|---|
| `-id=2` | `<ID2>` | Signing |
| `-id=3` | `<ID3>` | Public key/private key matching check |
| `-id=4` | `<ID4>` | Public key patch |
| `-id=5` | `<ID5>` | Signed S19 verification |

### 中文

V2.0 使用一个 XML 文件配置不同操作。

推荐结构：

```xml
<CYBER_SECURITY_SIGN_CONFIG>
    <ID2>
        <!-- S19 签名配置 -->
    </ID2>

    <ID3>
        <!-- 公钥匹配校验配置 -->
    </ID3>

    <ID4>
        <!-- 公钥补丁配置 -->
    </ID4>

    <ID5>
        <!-- 已签名 S19 验证配置 -->
    </ID5>
</CYBER_SECURITY_SIGN_CONFIG>
```

工具会根据操作 ID 搜索对应 XML 节点：

| CLI ID | 需要的 XML 节点 | 用途 |
|---|---|---|
| `-id=2` | `<ID2>` | 签名 |
| `-id=3` | `<ID3>` | 公钥/私钥匹配校验 |
| `-id=4` | `<ID4>` | 公钥补丁 |
| `-id=5` | `<ID5>` | 已签名 S19 验证 |

---

## 📝 XML Format and How to Fill It / XML 格式与填写方法

### 1. Integer Format / 整数格式

All addresses and sizes can be written as hexadecimal:

```xml
<SIGNATURE_ADDR>0X80040000</SIGNATURE_ADDR>
<SIGNATURE_SIZE>0X00003900</SIGNATURE_SIZE>
```

or decimal:

```xml
<SIGNATURE_SIZE>14592</SIGNATURE_SIZE>
```

Recommended: use hexadecimal with `0X`.

推荐使用 `0X` 十六进制格式。

---

### 2. Section Definition / 区域定义

A section defines one continuous S19 address range.

一个 section 表示一段连续的 S19 地址范围。

```xml
<SIGNATURE_SECTION>
    <SIGNATURE_SECTION_NAME>MM0</SIGNATURE_SECTION_NAME>
    <SIGNATURE_ADDR>0X80040000</SIGNATURE_ADDR>
    <SIGNATURE_SIZE>0X00003900</SIGNATURE_SIZE>
</SIGNATURE_SECTION>
```

| XML Tag | Required | Meaning / 含义 |
|---|---|---|
| `SIGNATURE_SECTION_NAME` | Yes | Section name, referenced by output / 区域名称，供输出引用 |
| `SIGNATURE_ADDR` | Yes | Start address / 起始地址 |
| `SIGNATURE_SIZE` | Yes if no end address | Data length / 数据长度 |
| `SIGNATURE_END_ADDR` | Optional alternative | End address, can replace size / 结束地址，可替代 size |

You may use either:

```xml
<SIGNATURE_SIZE>0X100</SIGNATURE_SIZE>
```

or:

```xml
<SIGNATURE_END_ADDR>0X80043FFF</SIGNATURE_END_ADDR>
```

If both are present, `SIGNATURE_SIZE` is used.

如果两者都存在，优先使用 `SIGNATURE_SIZE`。

---

### 3. Output Definition / 输出定义

An output tells the tool what to write into S19.

输出定义告诉工具向 S19 写入什么内容。

There are two supported output methods:

| Method | Meaning |
|---|---|
| `FIX` | Write fixed bytes |
| `RSA2048-PSS-SHA256` | Generate and write RSA-PSS signature |

---

### 4. FIX Output / 固定字节输出

```xml
<SIGNATURE_OUTPUT>
    <SIGNATURE_OUTPUT_NAME>HEADER</SIGNATURE_OUTPUT_NAME>
    <SIGNATURE_OUTPUT_METHOD>FIX</SIGNATURE_OUTPUT_METHOD>
    <SIGNATURE_OUTPUT_SECTON>NONE</SIGNATURE_OUTPUT_SECTON>
    <SIGNATURE_OUTPUT_TEXT>00,00,01,00</SIGNATURE_OUTPUT_TEXT>
    <SIGNATURE_OUTPUT_ADDR>0X80043900</SIGNATURE_OUTPUT_ADDR>
    <SIGNATURE_OUTPUT_SIZE>0X04</SIGNATURE_OUTPUT_SIZE>
</SIGNATURE_OUTPUT>
```

| XML Tag | Meaning / 含义 |
|---|---|
| `SIGNATURE_OUTPUT_NAME` | Output name, only for logging / 输出名称，仅用于日志 |
| `SIGNATURE_OUTPUT_METHOD` | `FIX` |
| `SIGNATURE_OUTPUT_SECTON` | `NONE` |
| `SIGNATURE_OUTPUT_TEXT` | Fixed bytes / 固定字节 |
| `SIGNATURE_OUTPUT_ADDR` | Write address / 写入地址 |
| `SIGNATURE_OUTPUT_SIZE` | Write size / 写入长度 |

Supported fixed byte formats:

```xml
<SIGNATURE_OUTPUT_TEXT>00,00,01,00</SIGNATURE_OUTPUT_TEXT>
```

```xml
<SIGNATURE_OUTPUT_TEXT>0x00,0x00,0x01,0x00</SIGNATURE_OUTPUT_TEXT>
```

```xml
<SIGNATURE_OUTPUT_TEXT>00000100</SIGNATURE_OUTPUT_TEXT>
```

---

### 5. RSA Signature Output / RSA 签名输出

```xml
<SIGNATURE_OUTPUT>
    <SIGNATURE_OUTPUT_NAME>ASW_SIGNATURE</SIGNATURE_OUTPUT_NAME>
    <SIGNATURE_OUTPUT_METHOD>RSA2048-PSS-SHA256</SIGNATURE_OUTPUT_METHOD>
    <SIGNATURE_OUTPUT_SECTON>MM0,ASW,MM0_Vkey_OVkey,ASW_Vkey_OVkey</SIGNATURE_OUTPUT_SECTON>
    <SIGNATURE_OUTPUT_TEXT>NONE</SIGNATURE_OUTPUT_TEXT>
    <SIGNATURE_OUTPUT_ADDR>0X80043904</SIGNATURE_OUTPUT_ADDR>
    <SIGNATURE_OUTPUT_SIZE>0X100</SIGNATURE_OUTPUT_SIZE>
</SIGNATURE_OUTPUT>
```

| XML Tag | Meaning / 含义 |
|---|---|
| `SIGNATURE_OUTPUT_METHOD` | Must be `RSA2048-PSS-SHA256` |
| `SIGNATURE_OUTPUT_SECTON` | Section names used for signing / 参与签名的 section 名称 |
| `SIGNATURE_OUTPUT_ADDR` | Signature write address / 签名写入地址 |
| `SIGNATURE_OUTPUT_SIZE` | Signature size, RSA2048 should be `0X100` |

> Note: The tag name `SIGNATURE_OUTPUT_SECTON` contains a typo from the original requirement.  
> The tool supports both `SIGNATURE_OUTPUT_SECTON` and `SIGNATURE_OUTPUT_SECTION`.

> 注意：`SIGNATURE_OUTPUT_SECTON` 是原始需求中的拼写。  
> 工具同时兼容 `SIGNATURE_OUTPUT_SECTON` 和 `SIGNATURE_OUTPUT_SECTION`。

---

### 6. Signing Source Construction / 签名源构造

For each section listed in `SIGNATURE_OUTPUT_SECTON`, the tool appends:

```text
startAddr(4 bytes, big-endian)
+ dataLength(4 bytes, big-endian)
+ data bytes
```

Example:

```xml
<SIGNATURE_OUTPUT_SECTON>MM0,ASW</SIGNATURE_OUTPUT_SECTON>
```

means:

```text
sign_source =
    MM0.startAddr(4B) + MM0.size(4B) + MM0.data
  + ASW.startAddr(4B) + ASW.size(4B) + ASW.data
```

---

## 🧭 ID2 XML Signing Configuration / ID2 XML 签名配置

`ID2` is used by:

```bash
python CyberSecuritySign.py -id=2 -ixml=config.xml -is19=input.s19 -os19=output_signed.s19 -ipri=private_key.pem
```

### Minimal structure / 最小结构

```xml
<ID2>
    <SIGNATURES>
        <SIGNATURE>
            <SIGNATURE_NAME>Application-ASW</SIGNATURE_NAME>

            <SIGNATURE_SECTIONS>
                ...
            </SIGNATURE_SECTIONS>

            <SIGNATURE_OUTPUTS>
                ...
            </SIGNATURE_OUTPUTS>
        </SIGNATURE>
    </SIGNATURES>
</ID2>
```

### Complete example / 完整示例

```xml
<ID2>
    <SIGNATURES>
        <SIGNATURE>
            <SIGNATURE_NAME>Application-ASW</SIGNATURE_NAME>

            <SIGNATURE_SECTIONS>
                <SIGNATURE_SECTION>
                    <SIGNATURE_SECTION_NAME>MM0</SIGNATURE_SECTION_NAME>
                    <SIGNATURE_ADDR>0X80040000</SIGNATURE_ADDR>
                    <SIGNATURE_SIZE>0X00003900</SIGNATURE_SIZE>
                </SIGNATURE_SECTION>

                <SIGNATURE_SECTION>
                    <SIGNATURE_SECTION_NAME>ASW</SIGNATURE_SECTION_NAME>
                    <SIGNATURE_ADDR>0X80044000</SIGNATURE_ADDR>
                    <SIGNATURE_SIZE>0X00777900</SIGNATURE_SIZE>
                </SIGNATURE_SECTION>
            </SIGNATURE_SECTIONS>

            <SIGNATURE_OUTPUTS>
                <SIGNATURE_OUTPUT>
                    <SIGNATURE_OUTPUT_NAME>HEADER</SIGNATURE_OUTPUT_NAME>
                    <SIGNATURE_OUTPUT_METHOD>FIX</SIGNATURE_OUTPUT_METHOD>
                    <SIGNATURE_OUTPUT_SECTON>NONE</SIGNATURE_OUTPUT_SECTON>
                    <SIGNATURE_OUTPUT_TEXT>00,00,01,00</SIGNATURE_OUTPUT_TEXT>
                    <SIGNATURE_OUTPUT_ADDR>0X80043900</SIGNATURE_OUTPUT_ADDR>
                    <SIGNATURE_OUTPUT_SIZE>0X04</SIGNATURE_OUTPUT_SIZE>
                </SIGNATURE_OUTPUT>

                <SIGNATURE_OUTPUT>
                    <SIGNATURE_OUTPUT_NAME>ASW_SIGNATURE</SIGNATURE_OUTPUT_NAME>
                    <SIGNATURE_OUTPUT_METHOD>RSA2048-PSS-SHA256</SIGNATURE_OUTPUT_METHOD>
                    <SIGNATURE_OUTPUT_SECTON>MM0,ASW</SIGNATURE_OUTPUT_SECTON>
                    <SIGNATURE_OUTPUT_TEXT>NONE</SIGNATURE_OUTPUT_TEXT>
                    <SIGNATURE_OUTPUT_ADDR>0X80043904</SIGNATURE_OUTPUT_ADDR>
                    <SIGNATURE_OUTPUT_SIZE>0X100</SIGNATURE_OUTPUT_SIZE>
                </SIGNATURE_OUTPUT>
            </SIGNATURE_OUTPUTS>
        </SIGNATURE>
    </SIGNATURES>
</ID2>
```

---

## 🔑 ID3 XML Public Key Verification Configuration / ID3 XML 公钥校验配置

`ID3` is used by:

```bash
python CyberSecuritySign.py -id=3 -ixml=config.xml -is19=input_key.s19 -ipri=private_key.pem
```

It checks whether the public key stored in S19 matches the public key derived from private key PEM.

它用于检查 S19 中存储的公钥是否与私钥 PEM 推导出的公钥一致。

### XML format / XML 格式

```xml
<ID3>
    <PUBLIC_KEY_STORAGE>
        <BASE_ADDR>0X80003D00</BASE_ADDR>
        <TOTAL_SIZE>0X120</TOTAL_SIZE>

        <MODULUS_WORD_COUNT_OFFSET>0X008</MODULUS_WORD_COUNT_OFFSET>
        <MODULUS_WORD_COUNT>0X40</MODULUS_WORD_COUNT>

        <MODULUS_OFFSET>0X00C</MODULUS_OFFSET>
        <MODULUS_SIZE>0X100</MODULUS_SIZE>

        <EXPONENT_WORD_COUNT_OFFSET>0X10C</EXPONENT_WORD_COUNT_OFFSET>
        <EXPONENT_WORD_COUNT>0X01</EXPONENT_WORD_COUNT>

        <EXPONENT_OFFSET>0X110</EXPONENT_OFFSET>
        <EXPONENT_VALUE>0X00010001</EXPONENT_VALUE>

        <WORD_ENDIAN>LITTLE</WORD_ENDIAN>
    </PUBLIC_KEY_STORAGE>
</ID3>
```

### Field description / 字段说明

| XML Tag | Meaning / 含义 |
|---|---|
| `BASE_ADDR` | Start address of public key storage / 公钥存储起始地址 |
| `TOTAL_SIZE` | Total storage size / 公钥存储总长度 |
| `MODULUS_WORD_COUNT_OFFSET` | Offset of modulus word count / modulus word count 偏移 |
| `MODULUS_WORD_COUNT` | Expected modulus word count, RSA2048 = `0X40` |
| `MODULUS_OFFSET` | Offset of modulus bytes / modulus 偏移 |
| `MODULUS_SIZE` | Modulus size, RSA2048 = `0X100` |
| `EXPONENT_WORD_COUNT_OFFSET` | Offset of exponent word count |
| `EXPONENT_WORD_COUNT` | Usually `0X01` |
| `EXPONENT_OFFSET` | Offset of exponent |
| `EXPONENT_VALUE` | Usually `0X00010001` |
| `WORD_ENDIAN` | Endian of uint32 fields, usually `LITTLE` |

---

## 🩹 ID4 XML Public Key Patch Configuration / ID4 XML 公钥补丁配置

`ID4` is used by:

```bash
python CyberSecuritySign.py -id=4 -ixml=config.xml -is19=input_key.s19 -ipub=public_key.pem -os19=output_key_patched.s19
```

It patches/replaces the public key stored in S19.

它用于替换 S19 中存储的公钥。

`ID4` uses the same `PUBLIC_KEY_STORAGE` format as `ID3`.

`ID4` 使用与 `ID3` 相同的 `PUBLIC_KEY_STORAGE` 格式。

```xml
<ID4>
    <PUBLIC_KEY_STORAGE>
        <BASE_ADDR>0X80003D00</BASE_ADDR>
        <TOTAL_SIZE>0X120</TOTAL_SIZE>
        <MODULUS_WORD_COUNT_OFFSET>0X008</MODULUS_WORD_COUNT_OFFSET>
        <MODULUS_WORD_COUNT>0X40</MODULUS_WORD_COUNT>
        <MODULUS_OFFSET>0X00C</MODULUS_OFFSET>
        <MODULUS_SIZE>0X100</MODULUS_SIZE>
        <EXPONENT_WORD_COUNT_OFFSET>0X10C</EXPONENT_WORD_COUNT_OFFSET>
        <EXPONENT_WORD_COUNT>0X01</EXPONENT_WORD_COUNT>
        <EXPONENT_OFFSET>0X110</EXPONENT_OFFSET>
        <EXPONENT_VALUE>0X00010001</EXPONENT_VALUE>
        <WORD_ENDIAN>LITTLE</WORD_ENDIAN>
    </PUBLIC_KEY_STORAGE>
</ID4>
```

---

## ✅ ID5 XML Signature Verification Configuration / ID5 XML 签名验证配置

`ID5` is used by:

```bash
python CyberSecuritySign.py -id=5 -ixml=config.xml -is19key=key.s19 -is19sign=signed.s19
```

It requires both:

- `PUBLIC_KEY_STORAGE`
- `SIGNATURES`

它需要同时包含：

- `PUBLIC_KEY_STORAGE`
- `SIGNATURES`

### XML structure / XML 结构

```xml
<ID5>
    <PUBLIC_KEY_STORAGE>
        ...
    </PUBLIC_KEY_STORAGE>

    <SIGNATURES>
        ...
    </SIGNATURES>
</ID5>
```

### Verification process / 验证流程

For each output:

- If method is `FIX`, compare actual bytes in S19 with `SIGNATURE_OUTPUT_TEXT`.
- If method is `RSA2048-PSS-SHA256`, read signature from `SIGNATURE_OUTPUT_ADDR`, rebuild sign source, and verify.

对于每个输出：

- 如果 method 是 `FIX`，则比较 S19 实际字节与 `SIGNATURE_OUTPUT_TEXT` 是否一致。
- 如果 method 是 `RSA2048-PSS-SHA256`，则从 `SIGNATURE_OUTPUT_ADDR` 读取签名，重建签名源并验签。

---

## 🗂 HM0 Public Key Storage in S19 / HM0 公钥在 S19 中的存储格式

A typical public key storage layout:

```text
Start Address : 0x80003D00
Total Length  : 0x120 bytes
Used Length   : 0x114 bytes
```

### Memory Layout / 内存布局

| Offset | Address | Size | Description |
|---:|---:|---:|---|
| `0x000` | `0x80003D00` | 4 | Header word 0 |
| `0x004` | `0x80003D04` | 4 | Header word 1 |
| `0x008` | `0x80003D08` | 4 | Modulus word count = `0x40` |
| `0x00C` | `0x80003D0C` | 256 | RSA2048 modulus |
| `0x10C` | `0x80003E0C` | 4 | Exponent word count = `0x01` |
| `0x110` | `0x80003E10` | 4 | Exponent = `0x00010001` |
| `0x114` | `0x80003E14` | 12 | Padding |

### Stored Values / 存储值

| Field | Logical Value | S19 Byte Order |
|---|---:|---|
| Header0 | `0x00000000` | Little-endian |
| Header1 | `0x00000000` | Little-endian |
| Modulus word count | `0x00000040` | Little-endian |
| Modulus | 256 bytes | Big-endian modulus byte stream |
| Exponent word count | `0x00000001` | Little-endian |
| Exponent | `0x00010001` | Little-endian |
| Padding | `0x00` | bytes |

---

## 🔁 ARXML and S19 Key Mapping / ARXML 与 S19 公钥映射关系

### English

In ARXML, the public key may appear as a list of 32-bit words:

```xml
<VALUE>
0x0, 0x0, 0x40,
0x377046B0,0xF718308F,...
0x01,0x010001
</VALUE>
```

This is logically:

```c
uint32_t key[] = {
    0x00000000,
    0x00000000,
    0x00000040,

    // 64 modulus words
    0x377046B0,
    0xF718308F,
    ...

    0x00000001,
    0x00010001
};
```

When compiled into S19 for a little-endian MCU, each 32-bit word is stored little-endian.

Example:

```text
ARXML word : 0x377046B0
S19 bytes  : B0 46 70 37
```

### 中文

在 ARXML 中，公钥可能以 32-bit word 数组形式出现：

```xml
<VALUE>
0x0, 0x0, 0x40,
0x377046B0,0xF718308F,...
0x01,0x010001
</VALUE>
```

逻辑上等价于：

```c
uint32_t key[] = {
    0x00000000,
    0x00000000,
    0x00000040,

    // 64 个 modulus word
    0x377046B0,
    0xF718308F,
    ...

    0x00000001,
    0x00010001
};
```

编译到小端 MCU 的 S19 后，每个 32-bit word 会按 little-endian 存储。

例如：

```text
ARXML word : 0x377046B0
S19 bytes  : B0 46 70 37
```

---

## 🔑 Public Key Formats / 公钥格式说明

The tool can display several public key formats.

工具可以显示多种公钥格式。

| Field | Meaning / 含义 |
|---|---|
| `public_key_hex` | DER SubjectPublicKeyInfo HEX，完整 DER 公钥 |
| `public_key_mod` | RSA modulus, big-endian，标准大端模数 |
| `public_key_mod_bg` | Same as `public_key_mod`，与 `public_key_mod` 相同 |
| `public_key_mod_lt` | Full byte-reversed modulus，整个 modulus 字节反转 |
| `public_key_mod_jf_lt` | 32-bit little-endian word representation，32-bit 小端 word 表示 |

---

## ✅ Signature Verification Flow / 签名验证流程

For XML-driven ID5:

```text
Key S19
    ↓
Parse public key according to <PUBLIC_KEY_STORAGE>
    ↓
Load signed S19
    ↓
For each XML SIGNATURE_OUTPUT:
    - FIX: compare fixed bytes
    - RSA2048-PSS-SHA256: rebuild sign source and verify signature
    ↓
All checks PASS → Verification successful
```

基于 XML 的 ID5 流程：

```text
Key S19
    ↓
根据 <PUBLIC_KEY_STORAGE> 解析公钥
    ↓
加载 signed S19
    ↓
对每个 XML SIGNATURE_OUTPUT:
    - FIX: 比较固定字节
    - RSA2048-PSS-SHA256: 重建签名源并验签
    ↓
全部通过 → 验证成功
```

---

## 🧪 Troubleshooting / 常见问题

### 1. Signature verification failed / 签名验证失败

Possible causes:

| Cause | Explanation |
|---|---|
| Public/private key mismatch | S19 public key does not match signing private key |
| Wrong XML configuration | XML addresses or sizes are incorrect |
| Wrong sign source | Section order or section list is different |
| PSS parameter mismatch | Salt length or MGF1 differs |
| S19 data modified after signing | Signed data changed |
| Wrong signature address | Signature not written to expected address |
| Wrong header | Fixed header bytes do not match |

---

### 2. Required S19 address range is incomplete

The tool uses strict address validation.

工具使用严格地址校验。

If any required address is missing, the operation fails.

如果任何需求地址缺失，操作会失败。

Example:

```text
Required S19 address range is incomplete.
first_missing=0x80040010
```

---

### 3. Cannot find `<ID2>` / `<ID3>` / `<ID4>` / `<ID5>`

Check whether the XML contains the required root node.

检查 XML 是否包含对应的节点。

Example:

```xml
<CYBER_SECURITY_SIGN_CONFIG>
    <ID2>
        ...
    </ID2>
</CYBER_SECURITY_SIGN_CONFIG>
```

---

### 4. `SIGNATURE_OUTPUT_SECTON` spelling

The tool supports both:

```xml
<SIGNATURE_OUTPUT_SECTON>
```

and:

```xml
<SIGNATURE_OUTPUT_SECTION>
```

工具同时支持拼写错误版本和正确版本。

---

## 📦 Packaging to EXE / 打包为 EXE

Install PyInstaller:

```bash
pip install pyinstaller
```

Build GUI EXE:

```bash
pyinstaller --onefile --windowed CyberSecuritySign.py
```

Output:

```text
dist/CyberSecuritySign.exe
```

For CLI mode:

```bash
pyinstaller --onefile CyberSecuritySign.py
```

---

## 📁 Suggested Repository Structure / 推荐仓库结构

```text
CyberSecuritySign/
├─ CyberSecuritySign.py
├─ CyberSecuritySign_Config.xml
├─ README.md
├─ requirements.txt
├─ examples/
│  ├─ public_key.pem
│  ├─ private_key.pem
│  ├─ key_input.s19
│  ├─ unsigned_input.s19
│  └─ signed_output.s19
└─ docs/
   └─ xml_configuration.md
```

---

## 📄 requirements.txt

```text
cryptography
```

---

## ⚠️ Encryption vs Signing / 加密与签名说明

### English

This tool does **not encrypt** the S19 firmware.

It performs **digital signing**:

- Signing proves authenticity and integrity.
- Signing does not hide firmware content.
- Anyone can still read the S19 content.
- Only the matching private key can create a valid signature.
- The ECU or verifier uses the public key to verify the signature.

### 中文

本工具**不对 S19 固件进行加密**。

它执行的是**数字签名**：

- 签名用于证明数据来源可信以及数据未被篡改。
- 签名不会隐藏固件内容。
- 任何人仍然可以读取 S19 内容。
- 只有匹配的私钥才能生成有效签名。
- ECU 或验签工具使用公钥验证签名。

---

## 🛡 Security Notes / 安全注意事项

### English

- Private keys must be protected carefully.
- Do not commit private keys into GitHub.
- Do not share production private keys.
- RSA-PSS signatures are randomized; different signatures for the same file are normal.
- A signature only verifies if:
  - The public key matches the private key
  - The XML configuration is correct
  - The sign source construction is identical
  - The PSS parameters are identical
  - The signed data has not changed

### 中文

- 私钥必须严格保护。
- 不要将私钥提交到 GitHub。
- 不要共享生产私钥。
- RSA-PSS 签名具有随机性，同一个文件多次签名结果不同是正常现象。
- 验签成功必须满足：
  - 公钥与私钥匹配
  - XML 配置正确
  - 签名源数据构造规则一致
  - PSS 参数一致
  - 签名后的数据没有被修改

---

## 📜 Disclaimer / 免责声明

### English

This tool is intended for engineering, validation, and controlled production support scenarios.

Users are responsible for validating all cryptographic parameters, XML configurations, memory addresses, key materials, and OEM/project-specific requirements before production use.

Do not use this tool with production private keys unless proper key management, access control, and audit procedures are in place.

### 中文

本工具用于工程开发、验证以及受控生产支持场景。

在生产使用前，用户必须自行确认所有密码学参数、XML 配置、内存地址、密钥材料以及 OEM/项目特定要求。

如无完善的密钥管理、访问控制和审计流程，请勿直接使用生产私钥。
