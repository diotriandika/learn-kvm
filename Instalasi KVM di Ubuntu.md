## Instalasi KVM di Ubuntu 24.04

Untuk menginstall KVM, kita perlu untuk melakukan setup package virtualization yang diperlukan, memastikan bahwa sistem mensupport hardware virtualization dan autorisasi user untuk menjalakan KVM.

### Step 1 - Update Packages & Virtualization Support Check

Update informasi package system repository agar saat instalasi semua package dalam versi terbaru.

```bash
$ sudo apt-get update
```

Selanjutnya memastikan bahwa computer kita mendukung hardware virtualization.

```bash
$ egrep -c '(vmx|svm)' /proc/cpuinfo
16
```

Jika output yang keluar diatas dari `0`, maka computer kita mendukung hardware virtualization. Sebaliknya jika yang keluar ada `0` itu berarti computer tersebut tidak dapat menjalankan KVM.

Cek apakah computer kita bisa menggunakan KVM Acceleration. Install `cpu-checker` terlebih dahulu jika terdapat error

```bash
# Install cpu-checker
$ sudo apt-get install cpu-checker

# Verify if system support KVM acceleration
$ sudo kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used
```

### Step 2 - KVM Package Installation

Install semua KVM packages penting yang dibutuhkan.

```bash
$ sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils -y
```

Tunggu hingga semua packages terinstall.

### Step 3 - Authorize Users

Dalam pengoperasian KVM, hanya member dari `libvirt` dan `kvm` saja yang dapat menjalankan virtual machines. Kita bisa menambahkan user spesifik kedalam group tersebut untuk menjalankan VM.

```bash
# Add user to libvirt group
$ sudo adduser <username> libvirt

# Add user to kvm group
$ sudo adduser <username> kvm
```

> Note : Jika ingin menghapus otoritas user dari group, gunakan `deluser` pada opsi `adduser` diatas

Selanjutnya verifikasi instalasi KVM dengan menggunakan `virsh`. `virsh` merupakan command-line tool untuk memanage virtual machine di Linux.

```bash
$ sudo virsh list --all
 Id   Name               State
-----------------------------------
```

Kemudian cek juga status `libvirtd` apakah sudah berjalan. Jika tidak gunakan `systemctl enable --now` untuk force start & membuat `libvirtd` berjalan didaemon ketika startup.

```bash
# Check libvirtd status
$ sudo systemctl status libvirtd
 libvirtd.service - libvirt legacy monolithic daemon
     Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; preset:>
     Active: active (running) since Wed 2024-09-04 13:05:53 WITA; 49min ago
TriggeredBy: ● libvirtd-admin.socket
             ● libvirtd.socket
             ● libvirtd-ro.socket

# Enable on Startup
$ sudo systemctl enable --now libvirtd
```

