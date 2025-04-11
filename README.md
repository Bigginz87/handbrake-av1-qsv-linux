HEAD
# handbrake-av1-qsv-linux

# HandBrake AV1 QSV Linux Patch

🎬 Adds full AV1 **Intel QSV** support to HandBrake **CLI** on Linux!

---

## 🚀 What It Does

- ✅ Unlocks `qsv_av1_10bit` encoder for CLI use
- ✅ Enables **ICQ**, **B-frame**, and **LowPower** path
- ✅ Works with `makepkg -si`
- ✅ Clean patch — survives HandBrake updates
- ❌ No GUI hacks, no weird build flags

---

## 🛠 How to Build
```bash
gpg --recv-keys 5452E231DFDBCA11
```
```bash
git clone https://github.com/Bigginz87/handbrake-av1-qsv-linux.git
cd handbrake-av1-qsv-linux
makepkg -si
ff23f02 (Initial commit: HandBrake AV1 QSV patch)
```
