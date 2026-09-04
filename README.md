<div align="center">

<img src="assets/brand/zus_mark.svg" alt="ZUS" width="84">

# ZUS

**A fast, lightweight AI IDE — the full VS Code workbench with a built-in AI agent, in a ~22 MB installer.**

[![Latest release](https://img.shields.io/github/v/release/8syncdev/zus-releases?label=latest&color=4F7CFF)](https://github.com/8syncdev/zus-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/8syncdev/zus-releases/total?color=22D3EE)](https://github.com/8syncdev/zus-releases/releases)
![Platforms](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-0A0A0B)

*by [8 Sync Dev](https://8syncdev.com) — sync is a loop: two systems, one link.*

*English below · [Tiếng Việt bên dưới](#-tiếng-việt)*

<img src="assets/editor-agent-chat.jpg" alt="ZUS — editor with AI chat panel" width="880">

</div>

---

## 🇬🇧 English

This repository is the **official distribution hub** for ZUS by [8 Sync Dev](https://8syncdev.com) ([@8syncdev](https://github.com/8syncdev)): release binaries, checksums, and the auto-update manifest. Source code is developed in a private repository — every public build lands here.

### Why ZUS

- **Lightweight by architecture** — Tauri 2 (OS WebView + Rust core), no bundled Chromium. Windows installer ≈ 22 MB vs ≈ 200 MB for Electron-based IDEs.
- **AI agent built in** — self-planning, self-executing, self-verifying, with three autonomy levels (Ask first / Edits / Autopilot) and per-command allowlists. Free tier with daily quota, zero API-key setup.
- **Local-first privacy** — your codebase is indexed (embeddings + vector search) **on your machine**. The backend only manages accounts and quotas.
- **Familiar** — full VS Code workbench: Monaco editor, terminal, Git graph, search, and extensions via Open VSX.

<div align="center">
<img src="assets/agent-conversations.jpg" alt="AI agent conversations" width="430"> <img src="assets/dashboard-settings-themes.jpg" alt="Themes and autonomy settings" width="430">
</div>

### Install

#### Windows

```powershell
winget install 8syncdev.ZUS
```

```powershell
scoop bucket add zus https://github.com/8syncdev/scoop-zus
scoop install zus
```

Or download `ZUS_x.y.z_x64-setup.exe` from the [latest release](https://github.com/8syncdev/zus-releases/releases/latest).

> **SmartScreen note:** installers are not yet code-signed. Installing via **winget or scoop avoids the prompt**. For a manually downloaded `.exe`, verify its minisign signature (see [Verify a download](#verify-a-download)), then click **More info → Run anyway**.

#### macOS (Apple Silicon)

Download `ZUS_x.y.z_aarch64.dmg`. The app is unsigned — on first open: right-click the app → **Open** → **Open**, or run:

```bash
xattr -dr com.apple.quarantine /Applications/ZUS.app
```

#### Linux

| Distro | Command |
|---|---|
| Debian / Ubuntu | `sudo apt install ./ZUS_x.y.z_amd64.deb` |
| Fedora / RHEL | `sudo dnf install ./ZUS-x.y.z-1.x86_64.rpm` |
| Any | `chmod +x ZUS_x.y.z_amd64.AppImage && ./ZUS_x.y.z_amd64.AppImage` |

### Verify a download

The real trust anchor is the **minisign signature** (`.sig`) shipped next to every artifact,
made with the ZUS updater key `1c2f579d3d50beda`. The app verifies these signatures
**automatically** against the key compiled into it before installing or updating anything —
a tampered artifact is rejected fail-closed. This is the signature you should rely on.

`SHA256SUMS.txt` is a **convenience for spotting corrupted downloads only — not a trust anchor
on its own**: anyone who can edit a release can rewrite both the artifacts and `SHA256SUMS.txt`
in one go. From the next release onward it ships alongside `SHA256SUMS.txt.sig` (signed with the
same updater key); when that file is present, verify it too.

```bash
# Quick integrity check (detects corrupted downloads, NOT tampering):
sha256sum -c --ignore-missing SHA256SUMS.txt
# From the next release on, also verify the sums file is authentic:
minisign -Vm SHA256SUMS.txt -x SHA256SUMS.txt.sig \
  -P RWQcL1edPVC+2lpQSHFmsRXjz8wl4PI2PNpttRs7zZ7lqAvtNZU18tho
```

To verify an individual artifact by hand (e.g. `ZUS_x.y.z_amd64.AppImage` + its `.sig`), the
updater signature is a base64-wrapped minisign signature (Tauri format), so decode one layer
first, then verify with the pubkey above:

```bash
base64 -d ZUS_x.y.z_amd64.AppImage.sig > artifact.minisig
minisign -Vm ZUS_x.y.z_amd64.AppImage -x artifact.minisig \
  -P RWQcL1edPVC+2lpQSHFmsRXjz8wl4PI2PNpttRs7zZ7lqAvtNZU18tho
```

### Auto-updates

Install once — the app checks `latest.json` in the latest release here on startup and updates itself in place. Every update is **signature-verified before install**. Works for all channels (winget, scoop, direct download); scoop users can also run `scoop update zus`.

---

## 🇻🇳 Tiếng Việt

Đây là **kênh phát hành chính thức** của ZUS: binary, checksum và manifest auto-update. Mã nguồn phát triển ở repo private — mọi bản build công khai đều đưa về đây.

### Vì sao chọn ZUS

- **Nhẹ từ kiến trúc** — Tauri 2 (WebView hệ điều hành + core Rust), không chở Chromium. Installer Windows ≈ 22 MB, so với ≈ 200 MB của các IDE nền Electron.
- **AI agent có sẵn** — tự lập kế hoạch, tự thực thi, tự kiểm chứng; 3 mức tự chủ (Hỏi trước / Sửa file / Autopilot) + allowlist lệnh. Miễn phí theo quota ngày, không cần API key.
- **Local-first, riêng tư** — codebase được index (embedding + vector search) **ngay trên máy bạn**; backend chỉ quản tài khoản và quota.
- **Quen tay** — đầy đủ workbench VS Code: Monaco, terminal, Git graph, search, extensions qua Open VSX. UI tiếng Việt first.

### Cài đặt

**Windows** — copy 1 lệnh vào PowerShell (không dính cảnh báo SmartScreen):

```powershell
winget install 8syncdev.ZUS
```

hoặc qua Scoop:

```powershell
scoop bucket add zus https://github.com/8syncdev/scoop-zus
scoop install zus
```

Hoặc tải `ZUS_x.y.z_x64-setup.exe` từ [bản mới nhất](https://github.com/8syncdev/zus-releases/releases/latest). File tải tay chưa ký cert nên SmartScreen sẽ hỏi — verify chữ ký minisign (xem [Verify a download](#verify-a-download)) trước, rồi **More info → Run anyway**.

**macOS (Apple Silicon)** — tải `.dmg`, lần đầu mở: chuột phải app → **Open** → **Open**.

**Linux** — `.deb` / `.rpm` / `.AppImage` như bảng tiếng Anh phía trên.

### Auto-update

Cài 1 lần là xong — app tự kiểm tra `latest.json` ở release mới nhất tại đây mỗi lần mở, tự tải và tự cài bản mới. **Mọi bản update đều được xác thực chữ ký số (minisign) trước khi cài** — không sợ giả mạo. Cài qua winget/scoop/tải tay đều auto-update như nhau.

---

<div align="center">

<img src="assets/brand/n1_interlock.svg" alt="8 Sync" width="26">

**8 Sync Dev** — Nguyễn Phương Anh Tú (Alex Dev / Kevin Nguyễn) · [8syncdev.com](https://8syncdev.com) · atus@8syncdev.com
*Sync is a loop — two systems, one link.*

</div>
