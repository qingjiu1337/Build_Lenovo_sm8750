# AOSP_REBUILD_AVB_BOOT ⚙️

> 用 **AOSP 公共测试密钥** 给 `boot.img` 重新签名的仓库。  
> 适用于 **联想拯救者Y700四/三/二代**等由AOSP公钥签名的镜像
---

## ✨ 特性

- 🔐 **AOSP testkey 重签**：可将没签/错签的 `boot.img` 拉进来，用 AOSP 提供的公测密钥重做 AVB header。
- 🧰 **自带工具**：仓库内置环境/脚本/工具（`rebuild_avb.py`、`magiskboot`、`tools/`）。
- 📦 **CI 友好**：可直接在 GitHub Actions 中用 `+archive/refs/heads/main.tar.gz` 拉快照使用

---

## 📁 目录结构

```text
AOSP_REBUILD_AVB_BOOT/
├── rebuild_avb.py        # 主脚本：拆 boot → 重签 → 封回去
├── magiskboot            # 解/打包 boot.img
├── tools/                # 签名用的辅助文件、key、脚本
└── README.md
```

## 🚀 快速开始

### 1. 下载仓库快照（示例）

```bash
curl -L https://github.com/showdo/AOSP_REBUILD_AVB_BOOT/archive/refs/heads/main.tar.gz -o avb_boot.tar.gz
mkdir avb_boot && tar -xzf avb_boot.tar.gz -C avb_boot
cd avb_boot/AOSP_REBUILD_AVB_BOOT-main
```

### 2. 放入要重签的 boot

```bash
cp /path/to/your/boot.img ./boot.img
```
#### boot.img名称不能变

### 3. 执行重签

```bash
rebuild_avb.py --chained-mode
```

脚本会在当前目录生成一个**已经用 AOSP 公测 key 签过**的 boot.img从而替换原boot.img
<br>原boot将自动移动至backup*开头目录中

---
### 4. 最后导出签名后boot.img即可直接刷入使用


## ❗注意事项

- 这是 **用 AOSP 公共测试密钥签名**，非特定设备厂商的私钥。仅适用于调试、CI、魔改、封装。
- 用前请确认 `boot.img` 是标准 Android boot.img

## 🫡 Credits

- AOSP / Android Verified Boot
- magisk
