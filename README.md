### WSL2 + ROCm + ROCDXG

[![WSL2](https://img.shields.io/badge/WSL2-Supported-blue.svg?logo=windows)](https://learn.microsoft.com/ja-jp/windows/wsl/)
[![Adrenalin](https://img.shields.io/badge/Adrenalin-26.2.2-red.svg?logo=amd)](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2.1/docs/install/installrad/wsl/howto_wsl.html)
[![ROCm](https://img.shields.io/badge/ROCm-7.2.1-orange.svg?logo=amd)](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2.1/docs/install/installrad/wsl/howto_wsl.html)
[![PyTorch](https://img.shields.io/badge/PyTorch-ROCm_2.10-EE4C2C.svg?logo=pytorch)](https://pytorch.org/)
[![License: MIT](https://img.shields.io/badge/Code%20License-MIT-green.svg)](LICENSE)

AMD Radeon GPU（ROCm + ROCDXG）向けの WSL2環境を自動で構築します。

---

# 🚀 Quick Start

Windows で `setup.bat` を実行するだけで、
環境構築〜Docker 起動までをすべて自動化できます。

---

# 🧰 事前準備（setup.bat 実行前）

Windows 側で以下を済ませてください。
---

## ✔ 1. AMD Software: Adrenalin Editionをインストール
必ず以下のリンク先にあるインストーラでインストールしてください。

Adrenalin 26.5.2以降はプレビュー版であるROCm 7.13.0が使用できます。

- [AMD Software: Adrenalin Edition 26.2.2](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-2-2.html)
- [AMD Software: Adrenalin Edition 26.3.1](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-3-1.html)
- [AMD Software: Adrenalin Edition 26.5.1](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-5-1.html)
- [AMD Software: Adrenalin Edition 26.5.2](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-5-2.html)
- [AMD Software: Adrenalin Edition 26.6.1](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-6-1.html)
- [AMD Software: Adrenalin Edition 26.6.2](https://www.amd.com/ja/resources/support-articles/release-notes/RN-RAD-WIN-26-6-2.html)
- [AMD Software: Adrenalin Edition 26.6.4](https://www.amd.com/en/resources/support-articles/release-notes/RN-RAD-WIN-26-6-4.html)

---

## ✔ 2. WSL2 を有効化

PowerShell（管理者）で実行：

```powershell
wsl --install
```

再起動後：

```powershell
wsl --set-default-version 2
```

---

## ✔ 3. Ubuntu 24.04 をインストール（必須）

公式で最も確実な方法：

```powershell
wsl --install -d Ubuntu-24.04
```

インストール後、Ubuntu を起動してユーザー名とパスワードを設定してください。

---

## ✔ 4. Windows SDK 10.0.26100.0 をインストール

[https://learn.microsoft.com/ja-jp/windows/apps/windows-sdk/downloads#windows-11--26100-versions](https://learn.microsoft.com/ja-jp/windows/apps/windows-sdk/downloads#windows-11--26100-versions)

`librocdxg` のビルドに必要です。

---

# 🧱 setup.bat が行うこと

`setup.bat` は以下を自動実行します。

---

## 🟦 Windows 側（WSL2 VM 最適化）

`.wslconfig` を生成：

```ini
[wsl2]
memory=16GB
processors=8
swap=0
localhostForwarding=true
```

---

## 🟩 WSL 側（Ubuntu 24.04）

### ROCm for WSL のインストール

### librocdxg のビルド & インストール

### `/etc/environment` に ROCm 最適化を追加

```bash
HSA_FORCE_FINE_GRAIN_PCIE=1
HSA_ENABLE_SDMA=0
HSA_ENABLE_DXG_DETECTION=1
MIOPEN_FIND_MODE=FAST
PYTORCH_HIP_ALLOC_CONF=...
```

### GPU 認識テスト

```bash
rocminfo
```

---

# 📚 References

## ROCm for WSL（公式ドキュメント）

[https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2.1/docs/install/installrad/wsl/howto_wsl.html](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2.1/docs/install/installrad/wsl/howto_wsl.html)

## AMD ROCDXG library

[https://github.com/ROCm/librocdxg](https://github.com/ROCm/librocdxg)

## ROCm Linux Install Guide

[https://rocm.docs.amd.com/projects/install-on-linux/en/docs-7.2.1/install/quick-start.html](https://rocm.docs.amd.com/projects/install-on-linux/en/docs-7.2.1/install/quick-start.html)

## ROCm PyTorch Install Guide

[https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2/docs/install/installrad/wsl/install-pytorch.html](https://rocm.docs.amd.com/projects/radeon-ryzen/en/docs-7.2/docs/install/installrad/wsl/install-pytorch.html)

---

