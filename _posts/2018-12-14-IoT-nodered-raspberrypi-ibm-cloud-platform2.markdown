---
layout: post
title: Membina Aplikasi IoT dengan Node-RED di atas IBM Cloud Platform - Pengenalan IBM Cloud Platform 
date: 2018-12-13 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---

### IBM Cloud Platform? 

IBM Cloud Platform yang dahulunya dikenali sebagai IBM Bluemix adalah merupakan Cloud Platform as a Service (PaaS). Dengan cloud PaaS ini awak boleh membikin, membina, menguji, menjalankan dan mengawal selia aplikasi di cloud dengan pantas tanpa perlu memikirkan hal-hal berkaitan infrastruktur yang diperlukan untuk mendokong pengunaan dan penyebaran aplikasi tersebut. Mengapa saya menyarankan awak menggunakan IBM Cloud Platform ini sedangkan ada tiga gergasi cloud platform yang lebih hebat seperti Amazon Web Service (AWS), Microsoft Azure, Google Cloud? Ini adalah kerana gergasi-gergasi ini rata-ratanya memerlukan awak meletakkan maklumat kad kredit jika awak ingin mencuba servis-servis yang mereka tawarkan. Mereka hanya akan "charge" kad kredit awak jika awak menggunakannya melebihi tahap minimum penggunaan servis-servis tertentu. Jika awak adalah seorang pelajar universiti, mungkin awak boleh memohon untuk menerima kredit percuma sebanyak USD200. Banyak juga tu macam-macam boleh cuba. Hmmm.. tapi untuk adik-adik sekolah yang berminat ingin mencuba, tak boleh lah kan. Kelebihan IBM Cloud Platform ini, ia membenarkan awak membuka akaun dan mencuba pakai servis minimun mereka dengan percuma. Tanpa perlu apa-apa syarat seperti yang saya nyatakan tadi.


<br/>
{:refdef: style="text-align: center;"}
![ibm-blumix]({{site.baseurl}}/assets/img/ibm-blumix.png)
{: refdef}
<br/>

IBM Cloud PaaS di bina berdasarkan pada perisian open source Cloud Foundry PaaS. IBM Cloud PaaS ini di dokong oleh Infrastruktur IBM Public Cloud dan Private Cloud menggunakan IBM Softlayer sebagai perisian untuk IaaSnya. **Public Cloud** bermaksud awak berkongsi dengan pengguna lain menggunakan servis cloud tersebut yang berjalan di atas infrastruktur fizikal yang sama, ibarat macam awak naik bas atau tren lah. Manakala untuk **Private Cloud** pula, IBM Softlayer itu dipasangkan pada fizikal infrastruktur yang di sewa khas untuk kegunaan awak sahaja, macam awak menaiki teksi ataupun memandu kereta sewa. Awak juga boleh menjalankan IBM Cloud PaaS ini di atas infrastruktur fizikal awak sendiri secara local, analoginya adalah seolah macam awak memandu kereta awak sendiri bawak penumpang dan guna servis "Grab". Selain menggunakan IBM Softlayer sebagai perisian untuk IaaS, awak juga boleh menggunakan perisian cloud computing popular yang lain seperti Openstack atau Container (nanti lah saya cerita pasal benda ni). Dengan IBM Cloud PaaS ini awak bukan sahaja boleh menjalankan aplikasi berdasarkan pada Cloud Foundary, awak juga boleh jalankan aplikasi awak sendiri di atas openstack virtual machine atau container (docker atau lxc dan kubernetes). Apa yang specialnya IBM Cloud PaaS ini, ia menambah nilai Cloud Foundary PaaS dengan menawarkan pelbagai servis katalog seperti web, data, mobile, cognitive, analytics, IoT, security, dan lain-lain lagi di samping aplikasi yang awak bina. Awak boleh mengguna dan mengintegrasikan pelbagai servis dari katalog ini bagi membina aplikasi melalui **Integration and API Management**. Aplikasi ciptaan awak ni kemudiannya boleh disiarkan di atas IBM platform ini secara terus untuk di akses oleh pelanggan-pelanggan awak. Oh ya, untuk mempercepat dan memudahkan pembikinan aplikasi, IBM Cloud Platform menyediakan **DevOPs Tooling** untuk membantu awak membikin, membina, menguji, menjalankan dan mengawal selia aplikasi di cloud dengan pantas.

### Mendaftar Akaun IBM Cloud Platform

Jom kita mendaftar untuk membuka akaun IBM Cloud Platform. Sila ikut arahan di bawah.

```javascript
1. Pergi ke https://console.bluemix.net
2. Klik > "create a free account"
3. Masukkan maklumat yang diperlukan.
4. Setelah selesai klik "Create Account", semak email awak.
5. Klik > Confirm Account
6. SILA Login Ke IBM cloud.
    * ID: <your email address>
    * Password: <your password>
```

Tahniah! awak sudah memiliki akaun cloud platform sendiri. Paparan IBM Cloud Dashboard seperti imej di bawah akan muncul di depan awak.

<br/>
{:refdef: style="text-align: center;"}
![bluemix-dashboard]({{site.baseurl}}/assets/img/bluemix-dashboard.png)
{: refdef}
<br/>

Untuk menyemak maklumat berkenaan akaun awak, sila ikut arahan di bawah.

```javascript
1. Di bucu atas kanan, klik > Account > Profile
2. Kemudian Klik > Billing.
3. Semak akaun awak.
    * Nama akaun:
    * ID akaun:
    * Account Type: Lite(free)
```

Gambar di bawah menunjukkan akaun yang telah awak daftarkan tadi adalah akaun **Lite free** yang hanya membenarkan awak mengguna pakai 1 virtual machine yang RAMnya berkapasiti 256MB dalam setiap bulan. Awak juga boleh menggunakan servis-servis yang di dalam kategori percuma sahaja. Jika awak meletakkan maklumat kad kredit, awak akan diberikan kredit percuma sebanyak USD200 sebagai permulaan dan boleh mengakses kesemua plan-plan dan servis-service yang ditawarkan. Selepas kredit percuma itu habis di pakai, IBM Cloud akan mula mengenakan bayaran pada kad kredit awak berdasarkan pada apa yang telah digunakan. Ini adalah konsep penggunaan sumber pengkomputeraan yang menarik dalam cloud computing, iaitu "Pay Per Use".

<br/>
{:refdef: style="text-align: center;"}
![bluemix-profile]({{site.baseurl}}/assets/img/blumix-profile.png)
{: refdef}
<br/>

### Jom Cuba Bina Aplikasi IoT

Kembali kepada paparan **Dashboard** dengan mengklik **> Menu** pada ikon **Hamburger** di bucu atas kiri skrin. Kemudian klik **> Create resource**. Awak akan dipaparkan dengan senarai panjang katalog servis yang dikategorikan untuk memudahkan awak membuat pilihan berdasarkan pada keperluan. Bayangkan banyak benda yang awak boleh lakukan dan pelajari menggunakan IBM Cloud Platform ini secara percuma. Untuk tujuan kita kali ini, klik > **Starter Kits(2)** dari senarai katalog di bahagian kiri skrin. Kemudian klik > **Internet of Things Platform Starter**. IoT Platform bersaiz kecil ini sesuai untuk "beginner" macam kita ni untuk mencuba dan belajar. 

<br/>
{:refdef: style="text-align: center;"}
![iot-starter]({{site.baseurl}}/assets/img/iot-starter.png)
{: refdef}
<br/>

Masukkan maklumat seperti berikut.

```javascript
App name: MyIoTApp 
Host name: MyIoTAppH
```
Nama App dan Host di atas mestilah unik. Skrol ke bawah, awak akan dapat lihat **IoT platform starter** ini menggunakan 3 plan lite percuma iaitu **SDK for Node.js** (pembangunan aplikasi), **Cloudant** (document database), **IoT Platform** (sambung, pantau, kawal dan analisis data pada peranti iot). Setiap dari servis percuma ini mempunyai spesifikasi dan had masing-masing. Jika awak nak upgrade ke tahap yang lebih tinggi untuk buat business ker, masukkan maklumat kad kredit awak. Tapi hati-hati yang, pastikan awak periksa harganya betul-betul! Pastikan pulangan ongkosnya melewati kos yang awak langgan.

Sudah bersedia? Klik **> Create** untuk mengaktifkan aplikasi di atas IoT platform ini. Paparan seperti di bawah akan dipamerkan sejuru selepas pengaktifan berjaya. 

<br/>
{:refdef: style="text-align: center;"}
![bluemix-create-resource]({{site.baseurl}}/assets/img/bluemix-create-resource.png)
{: refdef}
<br/>

Kemudian, pada hamburger icon di buju atas kiri, klik **Menu > Dashboard**. Awak akan dipamerkan dengan maklumat berkenaan aplikasi yang diaktifkan iaitu 1 aplikasi cloud foundry (MyIoTApp2), 2 servis Cloud Foundary (MyIoTApp2-cloudantNoSQLDB, MyIoTApp2-iotf-service), dan 1 servis (Cloudant-vl).

<br/>
{:refdef: style="text-align: center;"}
![bluemix-dashboard2]({{site.baseurl}}/assets/img/bluemix-dashboard2.png)
{: refdef}
<br/>

Seterusnya, untuk mengakses aplikasi MyIoTApp2 awak itu, klik **> MyIoTApp2**. Awak akan dipamerkan dengan maklumat berkenaan aplikasi MyIoTApp2 tadi. Dari imej di bawah, menunjukkan awak akan menggunakan **SDK Node.js** untuk membina aplikasi. Oleh kerana awak menggunakan plan lite free, awak cuma boleh menggunakan satu virtual machine (VM) instance dengan jumlah maksimum memori sebanyak 256M sahaja. Pada ruang **Connections (2)**, menunjukkan bahawa VM instance awak ini telahpun disambung pada database **MyIoTApp2-cloudantNoSQLDB** dan IoT platform **MyIoTApp2-iotf-service**. Jika awak nak tambah sambungan servis yang lain, klik **> Create connection**.

<br/>
{:refdef: style="text-align: center;"}
![bluemix-myapps]({{site.baseurl}}/assets/img/bluemix-myapps.png)
{: refdef}
<br/>


<br/>
{:refdef: style="text-align: center;"}
![bluemix-iotp]({{site.baseurl}}/assets/img/bluemix-iotp.png)
{: refdef}
<br/>

<br/>
{:refdef: style="text-align: center;"}
![bluemix-nodered-set-credential]({{site.baseurl}}/assets/img/bluemix-nodered-set-credential.png)
{: refdef}
<br/>

<br/>
{:refdef: style="text-align: center;"}
![bluemix-nodered]({{site.baseurl}}/assets/img/bluemix-nodered.png)
{: refdef}
<br/>

<br/>
{:refdef: style="text-align: center;"}
![bluemix-nodered-login]({{site.baseurl}}/assets/img/bluemix-nodered-login.png)
{: refdef}
<br/>

<br/>
{:refdef: style="text-align: center;"}
![bluemix-nodered-gui]({{site.baseurl}}/assets/img/bluemix-nodered-gui.png)
{: refdef}
<br/>





