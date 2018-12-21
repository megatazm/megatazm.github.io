---
layout: post
title: Menggunakan VirtualBox untuk Mencuba Linux OS dalam Windows 
date: 2018-11-8 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to]
---
Apa itu VirtualBox? Ia adalah aplikasi "Hypervisor" yang membolehkan pelbagai jenis komputer OS (Virtual Machine) menumpang di dalam komputer awak (Physical Machine). Gambarannya adalah seperti gambar di bawah. Contohnya, jika awak memakai Windows sebagai OS dalam komputer kemudian awak teringin mencuba OS lain seperti Mac OS atau Linux OS tanpa perlu membuang atau menyemak dan menganggu Windows kesayangan awak itu. Dalam erti kata lain Windows adalah "Host" OS (Tuan rumah komputer awak) dan Mac OS atau Linux OS adalah "Guest" OS (Menumpang dalam komputer awak). Jika komputer awak mempunyai keupayaan yang tinggi (RAM dan CPU core yang banyak), lebih banyak komputer "Virtual" ini boleh menumpang hidup di dalam komputer Windows awak. 
<br/>
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualization.png)
{: refdef}
<br/>
## Berikut adalah langkah-langkah secara kasar untuk:-
### Memasang VirtualBox pada Komputer Windows


```javascript
1. Mengaktifkan Virtualization 
2. Muat-turun dan install VirtualBox dan Extension Pack
```

### Mengkonfigurasi dan melancarkan VM Linux OS dalam VirtualBox

```javascript
1. Muat-turun image OS Linux
2. Konfigurasikan VM
3. Melancarkan VM Linux OS
```
#### Mengaktifkan Virtualization

Kebanyakkan komputer yang berspesifikasi sederhana dan tinggi kini rata-ratanya menyokong teknologi virtualization dan telah siap diaktifkan. Namun, awak boleh memastikannnya melalui sistem operasi Windows 10 atau Windows 8, dengan membuka Task Manager > Performance Tab. Seperti gambar di bawah, "Virtualization: Enabled" menunjukkan bahawa CPU komputer awak menyokong virtualization dan kini telah diaktifkan dalam BIOS. Jika ia menunjukkan "Virtualization: Disabled", awak perlu mengaktifkannya dalam BIOS. Jika tidak ada "Virtualization" di paparkan, ini bermakna CPU komputer awak tidak menyokong virtualization.

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/windows-task-manager.jpg)
{: refdef}
<br/>

#### Memuat-turun, install VirtualBox dan Extension Pack

Pergi ke laman web [virtualbox](https://www.virtualbox.org/wiki/Downloads) ini dan muat-turunkan versi binari untuk **"Windows Hosts"**. Selepas memuat-turun, klik dua kali pada fail binari tersebut untuk memasang VirtualBox. 

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-installation.png)
{: refdef}
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-network-interface.png)
{: refdef}
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-install.png)
{: refdef}
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-trusted-app.png)
{: refdef}
<br/>
Proses pemasangan VirtualBox atas windows memang sangat mudah. Mengikut turutan gambar di atas, klik:-
<br/>
```javascript
1. Next
2. Yes
3. Install
4. Install
```
<br/>
Selesai!

Jalankan VirtualBox.
<br/>
<br/>
Seterusnya untuk memasang ["VirtualBox Extension Pack"](https://www.virtualbox.org/wiki/Downloads), download dahulu softwarenya. Klik pada **All supported platform**. (pastikan nombor versinya sama dengan software Virtualbox yang awak download)

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-ext-pack-install.png)
{: refdef}
<br/>
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/virtualbox-ext-pack-update.png)
{: refdef}
<br/>

Untuk memasangkan "Extenstion Pack" itu, mudah sahaja. mengikut urutan gambar di atas:-
<b/>
```javascript
1. Klik File > Preference
2. Klik Extension > Butang (sebelah "Version") > Pilih "VirtualBox Extension Pack"
3. Klik OK
````
<br/>
Beres!
<br/>

#### Memuat-turun Image OS Linux, Konfigurasi dan Melancarkan VM

Awak memerlukan fail ISO Linux OS. Saya cadangkan awak guna CentOS Linux. Download "DVD ISO" fail [di sini](https://www.centos.org/download/). Untuk membina VM, jalankan VirtualBox. Klik > New. Isikan maklumat berikut:-
<br/>

```javascript
Name: CentOS
Type: Linux
Version: Red Hat (64-bit)
Klik > Continue
```
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-create-new.png)
{: refdef}
<br/>

Kini, awak perlu memutuskan jumlah RAM yang perlu diperuntukkan untuk VM ini. Untuk CentOS Desktop ini, minimum yang diperlukan adalah 1GB tetapi mungkin agak perlahan nanti prestasinya. 2GB ram adalah nilai yang optimum untuk sekadar kegunaan biasa. Oleh kerana laptop saya jumlah RAMnya adalah 8GB, kalau setakat 2GB untuk VM ini tiada masalah. Apa sahaja tetapan konfigurasinya, pastikan awak setkan dalam linkungan hijau. Jika awak memperuntukkan terlalu banyak RAM untuk VM, nanti awak akan menghadapi masalah prestasi yang lajunya macam siput.

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-set-memory.png)
{: refdef}
<br/>

Klik > Continue. 

   Kotak menu "Hard Disk" akan tertera. Tanpa perlu risau ikut arahan seperti di bawah.
<br/>
```bash
Hard Disk: Select > Create a virtual hard disk now > Klik Create
Hard Disk File Type: Select > VDI (VirtualBox Disk Image) > Klik Continue
Storage on Physical Hard Disk: Select > Dynamically Allocated > Klik Continue
```
<br/>

Seterusnya awak perlu menetapkan saiz hard disk yang diperlukan seperti kotak menu di bawah, "File Location and Size". Saya rasa untuk kegunaan biasa, kapasiti 20GB untuk hard disknya sudah memadai. Tapi, pastikan awak mempunyai ruang hard disk yang mencukupi pada cakera keras sebenar pada host komputer.
<br/> 
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-set-hd.png)
{: refdef}
<br/>
Sudah selesai set? Klik "Create".

Seterusnya, anda perlu memberikan VM ini sebuah virtual DVD drive untuk memacu fail ISO CentOS itu nanti. 

```javascript
Klik > Settings > Storage
Klik > Controller: IDE atau Controller: SATA
Klik > ikon CD ('add optical drive')
Pilih > Fail ISO CentOS yang awak download tadi.
Klik > OK
```
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-add-cd.png)
{: refdef}
<br/>

Untuk memasang CentOS, di virtualbox klik "Start" (Simbol Anak panah hijau). Ikut arahan skrin pemasangan CentOS ini (Awak klik "Yes" kan sahaja).

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-install-centos.png)
{: refdef}
<br/>

Proses pemasangan bermula sejurus sahaja awak klik "Start". Selepas awak memilih bahasa untuk OS ini, proses akan terhenti bagi memperolehi input daripada awak melalui interface Centos 7 INSTALLATION SUMMARY seperti gambar di bawah.

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-centos-setup.png)
{: refdef}
<br/>

Masukkan maklumat seperti berikut:-

```javascript
Installation Destination: ATA VBOX HARD DISK 20GB > Klik Done
Software Selection: GNOME Desktop > klik Done
Network & Hostname: Ethernet (enp0s3) > set ON > Klik Done
Klik > Begin Installation
------------------------------------------------------------------
ROOT PASSWORD: apaapajer > Klik 2x Done
USER CREATION: Username: user Password: apapapajer > Klik 2x Done
Tunggu sehingga pemasangan selesai, kemudian Klik > Reboot. 
```
Oh ya. Jika awak nak keluarkan cursor dari dalam VM ke komputer host, tekan keyboard "Ctrl" untuk Windows atau "Command" untuk MacOS.
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/vm-centos-reboot.png)
{: refdef}
<br/>

Setelah selesai reboot dengan jayanya, login ke CentOS dan awak boleh mula berjinak-jinak dengan Linux OS.








