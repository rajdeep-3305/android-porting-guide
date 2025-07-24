# 🧰 What You Need

Before you begin porting a custom ROM or recovery, you need to prepare your system with the required tools.

---

## 📦 Required Tools

- **CRB Kitchen** – main tool for unpacking and repacking images  
  👉 [Download CRB Kitchen](https://forum.xda-developers.com/t/kitchen-windows-tool-crb-v3-2-5.3947779/)

- **Android Image Kitchen (AIK)** – unpack boot/recovery images  
  👉 [AIK GitHub](https://github.com/osm0sis/AIK-Linux)

- **7Zip ZS** – extract `.img`, `.lz4`, `.cpio.gz` files

- **simg2img.exe** – convert sparse `.img` to raw

- **MixPlorer (Android app)** – inspect partitions on rooted phones

- **Notepad++** or any XML/PROP editor – edit config files like `build.prop`, `fstab`, etc.

- **WinMerge** – compare and patch `.rc`, `.xml`, and vendor files

---

## 🖥️ System Requirements

| Requirement     | Minimum          |
|-----------------|------------------|
| RAM             | 8GB+             |
| OS              | Windows 10/11 OR Linux |
| Disk Space      | 20GB+            |
| Linux Distro    | Fedora or Arch (for F2FS unpacking) |
| Internet        | Required (to download ROMs, tools, sources) |

---

> ⚠️ Some tools like CRB require WSL2 (for Windows) or Linux natively for advanced features like unpacking F2FS/EROFS.
