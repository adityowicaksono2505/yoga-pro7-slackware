# 🐈‍⬛ Slackware Yoga Pro 7 - Kucing1000cc

Repository ini berisi kumpulan konfigurasi dan script optimasi untuk **Slackware 15.1/Current** yang dijalankan pada **Lenovo Yoga Pro 7 (AMD Ryzen Edition)**.

## 🚀 Optimasi Utama
Sistem ini telah dituning untuk keseimbangan antara performa tinggi dan efisiensi baterai:

* **Zero-Touch Face ID**: Autentikasi biometrik menggunakan sensor IR via **Howdy**. Dilengkapi script pemicu otomatis sehingga login berjalan tanpa menyentuh keyboard sama sekali, bahkan setelah *logout* (via `FocusRegained`).
* **ZRAM Optimized**: 13.4GB menggunakan algoritma **ZSTD**. Dilengkapi monitoring real-time untuk melihat *Compression Ratio*.
* **Kernel Tuning**: Pembatasan `zram` hanya 1 device via modprobe untuk manajemen memori yang lebih clean.
* **VFS Responsiveness**: `vm.vfs_cache_pressure = 50` untuk navigasi file manager (Dolphin/Terminal) yang jauh lebih instan.
* **XFS Health Monitoring**: Integrasi pengecekan fragmentasi sistem file XFS secara otomatis pada dashboard.
* **Network Performance**: Tuning buffer jaringan untuk memaksimalkan bandwidth (Support hingga 200Mbps++).

## 📂 Struktur & Lokasi Penempatan

| File / Script | Lokasi Sistem | Fungsi |
| :--- | :--- | :--- |
| `upgrade-kernel` | `/usr/local/bin/upgrade-kernel` | **Script Sakti**: Otomasi `mkinitrd` + `grub-mkconfig` + Rebuild Howdy |
| `howdy-config.ini`| `/lib64/security/howdy/config.ini` | Config sensor IR & Workaround (Mode: Off) |
| `trigger-howdy` | `/usr/local/bin/trigger-howdy` | Script pemicu (Enter) virtual via `xdotool` |
| `sddm.conf` | `/etc/sddm.conf` | Konfigurasi SDDM & `FocusRegained=true` (Auto-trigger logout) |
| `Xsetup` | `/usr/share/sddm/scripts/Xsetup` | Entry point startup SDDM untuk pemicu Howdy |
| `zram` | `/etc/default/zram` | Konfigurasi kapasitas & algoritma ZRAM |
| `rc.zram` | `/etc/rc.d/rc.zram` | Script init untuk aktivasi ZRAM |
| `grub` | `/etc/default/grub` | Konfigurasi grub versi 2.14 |
| `zram.conf` | `/etc/modprobe.d/zram.conf` | Limitasi device zram di level kernel |
| `sysctl.conf` | `/etc/sysctl.conf` | Tuning VFS Cache & VM Swappiness (100) |
| `cek-laptop` | `/usr/local/bin/cek-laptop` | Dashboard monitoring "Kucing1000cc" |
| `.bashrc` (root) | `/root/.bashrc` | Kumpulan alias sakti & dashboard auto-start |
| `rc.local` | `/etc/rc.d/rc.local` | Auto-start services & tuning hardware |
| `rc.local_shutdown`| `/etc/rc.d/rc.local_shutdown` | Pembersihan `/tmp` otomatis & housekeeping |

## 🛠️ Perintah Khusus (Alias)
Beberapa perintah sakti yang disematkan di `.bashrc` root untuk mempermudah hidup:

* **`upgrade-kernel`**: Perintah paling krusial. Mengotomatisasi pembuatan `initrd`, update GRUB, dan **melakukan rebuild module Howdy** setelah update kernel.
* **`kucing-upgrade`**: Full sync `slackpkg` & `sbopkg` dalam satu perintah.
* **`cek-kucing`**: Menampilkan dashboard status sistem (ZRAM Ratio, XFS Health, Suhu, Speedtest).
* **`batre-awet` / `batre-full`**: Switch mode pengisian baterai (Conservation Mode via ACPI).

## ⚠️ Troubleshooting Tip

1. **Howdy tidak muncul otomatis setelah Logout:**
   Pastikan file `/etc/sddm.conf` memiliki baris berikut agar form login langsung aktif (memicu PAM):
   [General]
   FocusRegained=true

2. **Jeda Waktu Trigger (Enter Virtual):**
   Jika Howdy tidak langsung menyala saat boot, sesuaikan angka `sleep` pada `/usr/local/bin/trigger-howdy`:
   sleep 1.2 # Tambahkan sedikit jeda jika SDDM belum siap
   export DISPLAY=:0
   xdotool key Enter

> **Note**: Selalu gunakan `su -` untuk berpindah ke root agar profil `.bashrc` dan alias termuat dengan sempurna.

---
