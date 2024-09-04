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

## Membuat Virtual Machine

Dalam membuat VM menggunakan KVM, kita dapat menggunakan 2 metode yang ada, yakni menggunakan `virt-manager` yang berbasis GUI dan `virt-install` yang berbasis command-line

### Method 1 - Virt Manager (GUI)

Virt-manager adalah sebuah tool berbasis GUI (graphical user interface) untuk memanage virtual machines, mengizinkan user untuk membuat, memodifikasi, mengkonfigurasi, dan mengontrol VM menggunakan `libvirt`

Install `virt-manager` lalu buka

```bash
# Install virt-manager
$ sudo apt-get install virt-manager -y

# Start virt-manager
$ sudo virt-manager
```


Untuk membuat VM click logo komputer

![2024-09-04_14-12](https://github.com/user-attachments/assets/26095eba-83fa-4826-b72f-d86380a2990b)


Pilih Local Install Media, karena disini kita akan melakukan instalasi dengan ISO Image

![image-20240904141455039](https://github.com/user-attachments/assets/5acea83c-8b1e-4c16-8914-97b9a55d9eaf)


Selanjutnya pilih ISO Image yang akan digunakan, lalu Forward

![image-20240904141848148](https://github.com/user-attachments/assets/c0ccfe76-2961-4735-9bbf-dc62d5a14f8b)


Alokasikan resource RAM dan CPU yang akan digunakan untuk VM.

![image-20240904142012262](https://github.com/user-attachments/assets/8944f0cb-edc0-42fa-af76-2d5c6b874f3f)


Alokasikan juga storage yang akan digunakan untuk VM

![image-20240904142109421](https://github.com/user-attachments/assets/4f4b866e-d207-4c33-a410-9a69a89fcfc2)


Terakhir beri nama VM

![image-20240904142240458](https://github.com/user-attachments/assets/de050be5-59be-4ebf-b953-90de5ac0ad87)


### Method 2 - virt-install (CLI)

Untuk dapat membuat VM dicommand-line, kita dapat menggunakan tool `virt-install`

```bash
$ sudo virt-install --name=ubuntu-test \
> --ram=4096 \
> --vcpus=2 \
> --disk path=/var/lib/libvirt/images/ubuntu-test.qcow2,size=15 \
> --cdrom /path/to/iso/ubuntu-22.04.4-live-server-amd64.iso \
> --graphics vnc
```

![2024-09-04_14-41](https://github.com/user-attachments/assets/88679d8f-732f-42df-b3e7-a02dc00771d3)

Options yang tersedia :

![Screenshot from 2024-09-04 14-43-58](https://github.com/user-attachments/assets/b378a974-fdcf-4646-8d8b-2edc2617bb36)



