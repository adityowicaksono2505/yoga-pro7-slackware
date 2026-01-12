# 🐈‍⬛ Slackware Yoga Pro 7 - Kucing1000cc

Repository ini berisi kumpulan konfigurasi dan script optimasi untuk **Slackware Current** yang dijalankan pada **Lenovo Yoga Pro 7 (AMD Ryzen Edition)**.

## 🚀 Optimasi Utama
Sistem ini telah dituning untuk keseimbangan antara performa tinggi dan efisiensi baterai:

* **ZRAM Optimized**: 13.4GB menggunakan algoritma `ZSTD` (Kompresi tinggi, beban CPU rendah).
* **Kernel Tuning**: Pembatasan `zram` hanya 1 device via modprobe untuk manajemen memori yang lebih clean.
* **VFS Responsiveness**: `vm.vfs_cache_pressure = 50` untuk navigasi file manager (Dolphin/Terminal) yang jauh lebih instan.
* **Maintenance Automation**: Script khusus untuk otomasi pemeliharaan sistem.

## 📂 Struktur & Lokasi Penempatan

| File / Script | Lokasi Sistem | Fungsi |
| :--- | :--- | :--- |
| `zram` | `/etc/default/zram` | Konfigurasi kapasitas & algoritma ZRAM |
| `rc.zram` | `/etc/rc.d/rc.zram` | Script init untuk aktivasi ZRAM |
| `zram.conf` | `/etc/modprobe.d/zram.conf` | Limitasi device zram di level kernel |
| `sysctl.conf` | `/etc/sysctl.conf` | Tuning VFS Cache & VM Swappiness |
| `cek-laptop` | `/usr/local/bin/cek-laptop` | Dashboard monitoring "Kucing1000cc" |
| `rc.local` | `/etc/rc.d/rc.local` | Auto-start services & tuning hardware |
| `rc.local_shutdown` | `/etc/rc.d/rc.local_shutdown` | Pembersihan `/tmp` otomatis saat power-off |

## 🛠️ Perintah Khusus (Alias)
Beberapa perintah yang disematkan untuk mempermudah hidup sebagai Root:

* `upgrade-kernel`: Otomasi `mkinitrd` + `grub-mkconfig` setelah update kernel.
* `kucing-upgrade`: Full sync `slackpkg` & `sbopkg` dalam satu perintah.
* `cek-kucing`: Menampilkan dashboard status sistem secara real-time.
* `batre-awet` / `batre-full`: Switch mode pengisian baterai (Conservation Mode).

---
**Note**: Selalu jalankan `su -` sebelum mengeksekusi script manajemen sistem.
