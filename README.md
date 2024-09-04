## Apa itu KVM?

KVM atau *Kernel-based Virtual Machine* adalah sebuah teknologi virtualisasi opensource yang bekerja didalam kernel OS Linux. Dengan kernel Linux, KVM mampu memiliki performa dan kemampuan skalabilitas yang lebih baik. Teknologi ini dapat diinstal pada mesin Linux fisik untuk membuat Virtual Machine sehingga memungkinkan pengguna untuk berbagi resources seperti CPU, bandwidth, dan memori dari satu mesin fisik. KVM dapat membagi server fisik secara virtual menjadi beberapa resource dedicated atau lebih dikenal dengan VPS. KVM disini berfungsi untuk mengubah setiap mesin Linux menjadi Hypervisor. 

Adapun jenis Hypervisor terbagi menjadi dua tipe berbeda, yaitu:

- Hypervisor Tipe 1 atau Bare-Metal: Hypervisor tipe ini bekerja langsung diatas hardware dan tidak memerlukan sistem operasi host tambahan. Contohnya seperti KVM, VMware ESXi, Microsoft Hyper-V dan Xen.
- Hypervisor Tipe 2 atau Hosted: Hypervisor ini berjalan sebagai aplikasi diatas sistem operasi host yang sudah ada. Contohnya seperti VirtualBox dan VMware Workstation.

KVM bekerja dengan cara mengubah Linux menjadi Hypervisor bare-metal (tipe-1) untuk menjalankan beberapa mesin virtual secara efisien. Untuk melakukannya, Hypervisor memerlukan komponen-komponen tingkat system operasi seperti security manager, memory manager, process scheduler, device drivers, dan lain sebagainnya. Karena KVM terintegrasi dengan kernel Linux, maka seluruh komponen tingkat sistem operasi tersebut sudah tersedia. Alhasil, setiap mesin virtual akan diimplementasikan sebagai proses Linux biasa dengan hardware virtual khusus seperti storage, graphics adapter, memory dan CPU.

### !-Kernel Overview

Kernel, atau inti, merupakan dasar dari sebuah sistem operasi atau OS (Operational System). Fungsinya sebagai lapisan penghubung antara perangkat keras komputer dan OS yang beroperasi di dalamnya. Kernel bertanggung jawab untuk mengoordinasikan kinerja perangkat keras, menjalankan aplikasi, dan memuatnya ke dalam memori utama. Fungsi utama Kernel mencakup manajemen memori, manajemen proses dan tugas, serta pengelolaan disk.

Proses awal Kernel dimulai saat komputer dihidupkan. Bootloader akan mengaktifkan Kernel dan memuatnya ke dalam memori komputer. Sejak saat itu, Kernel mengambil kendali atas sistem input/output, mengelola proses awal hingga OS aktif. Kendali atas proses ini dapat diatur melalui desktop. Oleh karena itu, Kernel memiliki peran krusial pada tahap awal aktivasi OS pada perangkat komputer. Ketika sistem mengalami kerusakan, proses aktivasi awal ini dapat terganggu atau gagal loading.

## Keunggulan KVM

### Performa yang efisien

KVM berjalan diatas kernel Linux untuk menghasilkan performa yang lebih efisien. Ini membuat kinerja KVM sangat bagus berkat integrasinya dengan kernel linux dan ekstensi virtualisasi perangkat keras. Integrasi tersebut membuat mesin virtual mampu menghasilkan lantency yang rendah dan throughput yang tinggi.

### Fleksibilitas dan Skalabilitas









Referensi:

- https://dte.telkomuniversity.ac.id/mengenal-kernel-dan-tugasnya-dalam-kinerja-sebuah-operational-system/
- https://cloudmatika.co.id/blog-detail/kvm-adalah
- https://www.niagahoster.co.id/blog/kvm-adalah/

## 
