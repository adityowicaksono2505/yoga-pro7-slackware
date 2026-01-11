# Slackware Yoga Pro 7 - Kucing1000cc
Optimasi sistem Slackware Current untuk AMD Ryzen.

## Konfigurasi Utama:
* **ZRAM**: 13.4GB dengan algoritma ZSTD.
* **Kernel**: Dibatasi hanya 1 device zram via modprobe.
* **Update Script**: `kucing-update` untuk otomasi slackpkg & sbopkg.

## Lokasi Penempatan:
* `zram` -> `/etc/default/zram`
* `rc.zram` -> `/etc/rc.d/rc.zram`
* `zram.conf` -> `/etc/modprobe.d/zram.conf`
* `kucing-update` -> `/usr/local/bin/kucing-update`
* `rc.local` -> `/etc/rc.d/rc.local`
