---
layout: post
title: Membina Aplikasi IoT dengan Node-RED di atas IBM Cloud Platform - Bab 5. Memantau dan mengawal peranti IoT
date: 2019-1-16 13:32:20 +0300
description:  # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---

### IoT platform middleware

Untuk sesi kali ini, kita akan menggunakan sebuah raspberry pi (Ini apa kek pi ker? Bukan laa. Ndak tau apa dia menatangnya, silalah ke [sini]({% post_url 2018-10-12-Akses-raspberry-pi-dengan-keyboard-mouse-dan-monitor%})) untuk di pantau dan di kawal dari IBM Cloud Platform melalui internet. Hubung kait antara peranti, aplikasi cloud platform dan internet ini melengkapkan ekosistem suatu sistem berkonsepkan IoT. Dengan kata lain, sistem yang berteraskan pada IoT adalah terdiri dari peranti yang berkeupayaan untuk berkomunikasi dengan aplikasi yang hidup di atas cloud platform melalui capaian internet. Bagi melengkapkan lagi hubung kait sistem ini, satu servis di cloud platform yang di panggil **Middleware** diperlukan sebagai "orang tengah" di antara aplikasi yang awak bina di atas cloud platform dan peranti tersebut. Dalam konteks kita sekarang ini, raspberry pi adalah merupakan peranti yang di pantau dan di kawal, flow node-RED di cloud platform adalah aplikasi yang awak bina untuk pengguna, manakala **IBM Watson IoT platfrom** pula ialah middlewarenya. 

Apakah fungsi middleware IBM Watson IoT ini? berikut adalah fungsi-fungsinya:-

* Pendaftaran peranti (Sekuriti)
* Sambungan (Protokol MQTT)
* Sokongan Gateway (Jambatan antara peranti ke internet)
* Pengurusan Peranti (Memperoleh data dan mengurus selia peranti)
* Integrasi dengan servis luaran.

**Pendaftaran peranti** ke dalam watson IoT ini adalah penting bagi memastikan data yang awak terima adalah daripada sumber yang betul dan selamat diguna pakai. Watson IoT berkomunikasi dengan peranti menggunakan **protokol MQTT** (Message Queing Telemetry Transport). Protokol komunikasi ini merupakan standard yang diguna pakai untuk peranti IoT melalui konsep **publish** dan **subscribe**. 

Apa itu publish dan subscribe? 

Dengan erti kata yang mudah, ia berkonsepkan seperti siaran astro (publisher) dan awak sebagai pelanggan (subscriber) - *Harap maklum, MQTT hanya menyiarkan data dalam bentuk text*. **MQTT** berkomunikasi secara **"asynchronous"**. Ini tidak sama seperti melalui email atau sms kerana ia berlaku secara **"synchronous"** atau secara langsung. Iaitu penghantar perlu tahu siapa penerimanya. Manakala, MQTT pula berkomunikasi secara tidak langsung dan ia tidak perlu mengetahui siapa penerimanya. MQTT menyiarkan data pada satu atau lebih tempat yang di panggil **"topic"**. Penerima yang ingin menerima data itu perlulah **subscribe** pada **topic** yang betul. 

Peranti yang didaftarkan sebagai **gateway** akan bertindak sebagai jambatan yang berhubung dengan Watson IoT secara terus melalui internet. Semua peranti-peranti yang lain perlu melalui gateway tersebut untuk menghantar data ke cloud platform. 

Mengapa tidak dibenarkan peranti-peranti tersebut berkomunikasi dengan cloud platform secara terus sahaja?

* Kebiasaannya peranti-peranti IoT adalah berkapasiti kecil dan menggunakan bateri. Ia tidak mempunyai keupayaan yang mencukupi untuk berkomunikasi secara terus ke internet. Tambahan lagi, untuk menjimatkan penggunaan tenaga, peranti-peranti ini hanya perlu "bangun" ketika menghantar data sahaja.

* Oleh kerana terdapat pelbagai jenis peranti yang menggunakan protokol transmisi yang berbeza-beza (LPWAN, WIFI, Bluetooth, Zigbee dan lain-lain), gateway ini bertindak sebagai penterjemah sebelum memajukan data dari peranti-peranti tersebut ke cloud platform.

* Peranti gateway ini juga bertindak sebagai pengkomputeran **"edge"**. Di sini, data-data mentah yang di terima dari peranti-peranti itu akan di proses terlebih dahulu. Selepas itu, gateway hanya menghantar data yang penting dan bersaiz kecil sahaja ke cloud platform. Seperti contoh jika peranti menghantar data imej, gateway memproses imej tersebut kemudian menghantar hasil pemprosesan itu ke cloud platform dalam bentuk text JSON. Ini menjimatkan penggunaan bandwidth internet dan ruang storan data serta mempercepatkan proses transmisi data yang mungkin datangnya dari berpuluh-puluh ribu mahu pun beratus-ratus ribu peranti.

* Dengan mengurangkan jumlah peranti yang bersambung dengan internet, kita dapat mengurangkan risiko di godam oleh pengodam internet.

Gateway bukan sahaja digunakan untuk mengurus data dan peranti. Ia juga boleh diintegrasikan dengan aplikasi yang lain seperti Jasper, Alexa, IFTTT, Google Home, Things Board, and database.

Tanpa berlengah-lengah lagi jom kita gunakan Watson IoT! ᕕ( ᐛ )ᕗ

### Watson IoT Platform

Login ke akaun Bluemix IBM Cloud Platform awak. Kemudian, lakukan langkah berikut,

```javascript
1. Klik > Dashboard > MyIoTApp2
2. Klik > Connections > MyIoTApp2-iotf-service 
3. Klik > Launch
```

Paparan IBM Watson IoT Platform akan muncul seperti imej di bawah.
<br/>
{:refdef: style="text-align: center;"}
![watson-iot]({{site.baseurl}}/assets/img/watson-iot.png)
{: refdef}
<br/>

Terdapat beberapa tab menu di bahagian kiri panel paparan interface IBM Watson IoT Platform ini. Bermula dari atas hingga ke bawah fungsinya adalah,

* **Board** - Untuk menyatakan ringkasan berkenaan dengan platform yang awak bina
* **Devices** - Untuk tambah, daftar, urus dan akses peranti
* **Members** - Untuk menambah pengguna bagi tujuan mengawal akses.
* **Apps** - Ringkasan berkenaan "API keys" yang telah di tambah ke dalam "organization" awak. Ia boleh di tapis, di susun, di cari melalui pelbagai kriteria.
* **Access Management** - Untuk mengawal akses melalui konsep peranan pengguna (admin, guest, member, operator, developer dan lain-lain)
* **Usage** - Ringkasan berkenaan penggunaan peranti dan application di Watson IoT platform.
* **Security** - Tetapkan polisi security dan kawalan akses ke server dari peranti
* **Setting** - Tukar konfigurasi dan ciri-ciri platform ini.
* **Extension** - Integrasi dengan servis dari pihak ke-3 seperti Jasper, Email, Historical Data Storage, dan Arm Mbed

### Memantau dan mengawal Peranti, Aplikasi dan Gateway

Sebelum kita mula melakukan aktiviti praktikal mengkonfigurasikan peranti, aplikasi dan gateway pada Watson IoT Platform, saya berikan sedikit penjelasan berkenaan peranan 3 komponen ini.

* **Peranti** – Fungsinya di sini adalah mengumpul data dan menghantar data ke cloud platform. Di Watson IoT, Awak kena **"create device"** dan tetapkan **"type"** pada peranti yang awak masukkan tadi. Selepas itu awak daftarkan peranti itu ke platform watson IoT.
* **Aplikasi** – Ini adalah aplikasi yang awak bina untuk menerima data dari peranti dan menghantar arahan ke peranti untuk bertindak. Untuk tujuan ini, Awak tidak perlu mendaftar aplikasi ini ke platform tetapi perlu menghantar **"API key"** untuk pengesahan.
* **Gateway** – Ini merupakan jambatan antara peranti dan platform. Awak perlu mendaftarkannya ke platform. Gateway akan mencipta **"event"** sebelum peranti menghantar data ke platform, kemudian aplikasi menerima data itu dari platform untuk menentukan arahan yang perlu diberikan kepada peranti.


#### Bina dan Daftar Peranti

Sebelum awak mengikut langkah-langkah di bawah untuk mendaftarkan peranti pada Watson IoT platform, pastikan awak telah mengakses raspberry pi dan menjalankan node-RED. Sila ke sini jika awak belum pernah mengendalikan [raspberry pi]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop%}) dan [node-RED]({% post_url 2018-11-13-Pengenalan-aplikasi-node-red%}).

```javascript
1. Di Watson IoT platform, Klik > Devices > Device Types > + Add Device Type
2. Tetapkan konfigurasi seperti berikut,
   Type: Device
   Name: raspberrypi
   Description: 'Tulis lah apa-apa keterangan berkenaan peranti ini'
3. Klik > Next
   Device information: 'Biarkan sahaja kosong'
4. Klik > Done
5. Klik > Register, untuk menambah peranti ke dalam platform. Masukkan konfigurasi 
berikut,
   Device Type: raspberrypi
   Device Id: mac_address_pi_awak_tanpa ':' 
   (Buka terminal pi, taip command: ip addr. Untuk kes saya, hasilnya adalah 
   link/ether b8:27:eb:9c:89:93. Oleh itu Devide Id: b827eb9c8993)
6. Klik > Next
   Device Info: 'Biarkan Kosong'. Klik > Next.
   Security > Authentication Token: MyToken1. Klik > Next > Done
7. Ulang proses di atas jika awak ndak menambah peranti ataupun Gateway.
8. Klik tab menu > Devices (Awak boleh melihat senarai peranti yang telah didaftarkan).
9. Klik pada salah satu peranti yang telah didaftarkan itu. (Awak dapat melihat maklumat terperinci berkenaan peranti itu).
```

#### Menghantar Data dari RaspberryPi ke BlueMix

Setelah selesai mendaftar raspberry pi, kita sudah boleh mula mengkonfigurasikannya untuk menghantar data ke Bluemix. Di node-RED raspberry pi, Klik > drag, drop dan sambung; **Inject node, Random node, Function node, Debug node dan Watson IoT output node** seperti imej di bawah.
<br/>
{:refdef: style="text-align: center;"}
![nodered-senddata]({{site.baseurl}}/assets/img/nodered-senddata.png)
{: refdef}
<br/>
Kemudian konfigurasikannya seperti di bawah.

```javascript
1. Configure inject node:
   Payload: String
   Repeat: Interval (every 5 seconds)
2. Configure function node:
   Name: Format data
   Function: 1  msg.payload = { 'd' : { 'random' :  msg.payload }};
             2  return msg;
3. Configure Watson IoT:
   Connect as: Device
   Select > Registered, 
   Click > pencil symbol
   Organization: copy_paste (At Watson IoT Platform, Klik > Setting > Identity > 
   Organization Id) 
   Device Type: raspberrypi
   Device Id: your_device_id (at iot platform > click device > copy paste device id)
   Auth Token: MyToken1
   Name: Copy paste Device Id
```

#### Menerima Data di BlueMix dari RaspberryPi 

Untuk menerima data dari raspberrypi, awak perlu mengkonfigurasikan node-RED yang berjalan di dalam Bluemix pula.

Di Bluemix node-RED, drag drop nod **input ibmiot**, kemudian konfigur seperti berikut:

```javascript
Authentication: Bluemix Service
Input Type: Device Event
Device Type: Check All
Device Id: Check All
Event: Check All
Format: json
Name: IBM IoT
```
Kemudian, drag drop nod **debug**, dan sambungkannya dengan nod **input ibmiot** tadi. 

Di node-RED RaspberryPi pula, **Klik > butang nod inject** 

Aktifkan **panel debug** di Bluemix node-RED awak. Nod Input ibmiot akan menerima data setiap 5 saat seperti imej di bawah.
<br/>
{:refdef: style="text-align: center;"}
![ibmiot-getdata]({{site.baseurl}}/assets/img/ibmiot-getdata.png)
{: refdef}
<br/>
#### Menghantar Arahan ke Peranti

Di Bluemix node-RED, drag drop nod **output ibmiot**, kemudian konfigur seperti berikut:

```
Authentication: Bluemix Service
Output Type: Device Command
Device Type: raspberrypi
Device Id: (masukkan device Id peranti awak) > b827eb9c8993 (saya punya)
Command Type: statusindicator
Format: json
Data: {}
Name: IBM IoT
```

Kemudian, drag, drop dan sambung 2 **nod inject, nod function, nod json**. Sambungkan nod-nod ini dengan nod **output ibmiot** tadi seperti imej di bawah.
<br/>
{:refdef: style="text-align: center;"}
![ibmiot-sendcmd]({{site.baseurl}}/assets/img/ibmiot-sendcmd.png)
{: refdef}
<br/>
Konfigur nod-nod ini seperti konfigurasi di bawah:

```javascript
1.Konfigur nod inject 1
     Payload: Select > string, type in 'Normal'
2.Konfigur nod inject 2
     Payload: Select > string, type in 'Alert'
3.Konfigur nod function
     Name: format message
     Function: 1 msg.payload = { "a" : { "indicator" : msg.payload}};
               2 return msg;
```

Di RaspberryPi node-RED, drag drop nod **input Watson ibmiot**. Konfigur seperti berikut:

```
Connect as: Device 
Command: All command
Credentials: (Masukkan device Id peranti awak) > b827eb9c8993 (saya punya)
```

Drag drop **nod debug**, kemudian sambungkan **nod input ibmiot** tadi dengan **nod debug** seperti imej di bawah.
<br/>
{:refdef: style="text-align: center;"}
![ibmiot-sendcmd2]({{site.baseurl}}/assets/img/ibmiot-sendcmd2.png)
{: refdef}
<br/>
Untuk menghantar arahan dari BlueMix node-RED ke raspberrypi,

    Klik > Butang nod Normal inject
    Klik > Butang nod Alert inject

Di raspberrypi node-RED, lihat di panel debug. Awak akan terima maklumat seperti di bawah.

```javascript
28/01/2019, 11:53:01node: def9e35d.c16dc
iot-2/cmd/statusindicator/fmt/json : msg.payload : Object
object
a: object
indicator: "Normal"

28/01/2019, 11:53:02node: def9e35d.c16dc
iot-2/cmd/statusindicator/fmt/json : msg.payload : Object
object
a: object
indicator: "Alert"
```

Payload JSON string yang awak suntik tadi (**Normal** dan **Alert**) telah berjaya di hantar ke raspberrypi. Melalui mesej string ini, awak boleh menyalurkannya ke nod-nod tambahan seperti **nod function**, atau **nod output raspi-gpio** untuk menghantar **email**, atau/dan menyalakan **lampu LED** & membunyikan **buzzer**.

#### Node-RED Sense Hat 

Ada beberapa sensor-sensor secara individu seperti **DS18B20** (suhu), **DHT11/DHT22** (suhu & kelembapan), **HC-SR501** (PIR Motion) dan **LED output** display yang awak boleh beli dengan harga yang agak murah. Kalau awak ada duit extra, boleh lah cuba **"Sense Hat"**. Di dalam node-RED rasberrypi, nod input/output untuk Sense Hat ini sudah siap ada di pasang. Awak boleh skrol ke bawah, cari palet untuk raspberrypi. Awak akan nampak ada 2 nod Sense Hat (nod input & output).

Nod input Sense Hat input terdiri daripada:-

* **Motion sensors** (accelerometer, gyroscope, magnetometer, compass)
* **Environment sensors** (temperature, humidity, pressure)
* **Joystick sensors** 

Manakala nod output Sense Hat pula hanya terdiri daripada:-

* **8x8 LED display**

Oleh kerana harganya yang agak mahal, dan saya pula cuma lecturer biasa sahaja. Tak cukup budget nak beli (RM170 jer pun, mahal ker.. ( ˘︹˘ )). Tapi nasib baik kita masih lagi boleh mencubanya dengan menggunakan **Sense Hat Simulator**. Untuk memasang Sense Hat versi virtual ini, **ssh** masuk ke dalam raspberrypi awak. Di terminal raspberrypi,

```bash
$ cd 
$ cd .node-red/
$ npm install node-red-node-pi-sense-hat-simulator
$ sudo node-red-stop; node-red-start
```

Reload browser yang awak gunakan tadi untuk mengakses node-RED raspberrypi. Skrol ke palet raspberrypi, awak akan jumpa ada 2 nod tambahan, iaitu **nod Sense Hat Sim**.


#### Menghantar Data Persekitaran Menggunakan Sense Hat Sim

Pergi ke raspberrypi node-RED, drag, drop dan sambung **nod input Sense Hat, nod delay, nod function, nod debug,** dan **nod output watson ibmiot** seperti imej di bawah. 
<br/>
{:refdef: style="text-align: center;"}
![raspi-sensehat]({{site.baseurl}}/assets/img/raspi-sensehat.png)
{: refdef}
<br/>
Tetapkan konfigurasi nod-nod ini seperti berikut.

```javascript
1. Configure Sense Hat:
   Check Environment
   Uncheck others
2. Configure delay:
   Action: Rate Limit
   Rate: 1 msg per 5 seconds
3. Configure function:
   Name: Env. Data
   Function: 1 msg.payload = {"Data" : {"Environment" : msg.payload}};
             2 return msg;
```

Sebelum mengkonfigur **nod output ibmiot**, kita mesti mendaftar gateway terlebih dahulu.

Di Bluemix IoT Platform, **Klik > Device Type**.

Memandangkan kita hanya menggunakan sebuah raspberrypi, awak mungkin perlu memadam peranti yang telah didaftarkan tadi, kemudian mendaftarkannya sebagai **gateway** dengan menggunakan **Device Id** yang sama. Oleh kerana saya menggunakan kabel ethernet (**eth0**) untuk menyambungkan raspberrypi ke wifi router, saya masih ada wifi adapter (**wlan0**) yang boleh saya gunakan **mac** addressnya tanpa ":" sebagai **Device Id** untuk **gateway** tanpa perlu memadam peranti yang saya daftarkan tadi (Awak boleh menggunakan mac address eth0 jika awak menggunakan wlan0). 

Dengan merujuk pada langkah-langkah untuk mendaftar peranti sebelum ini, sila daftarkan satu lagi **Device Type** dengan nama **"raspberrypiGW"**. Kemudian **register device** dengan menggunakan **Device Type:raspberrypiGW** dan **Device Id:(gunakan MAC eth0 atau MAC wlan0)**.

Di RaspberryPi node-red, konfigurkan **nod output ibmiot** seperti berikut.
```
Connect as: Gateway
    Select > Registered
Credentials: Click > Pencil symbol
    Organization: Organization_ID_Awak (mine:q6itzp)
    Device Type: raspberrypiGW
    Device Id: raspberrypiGW_DeviceId_Awak (mine:74da386e6101)
    Token: MyToken1
Device Type: (Biarkan kosong)
Device Id: (Biarkan kosong)
Event Type: event
Format: json
```

Kemudian, awak kena tambah **Sense Hat Device Type & Device Id** pada nod Function. Di RaspberryPi node-RED, tambah kod di dalam **nod Function Env. Data**  seperti berikut.

```javascript
    1 msg.payload = {"Data" : {"Environment":msg.payload}};
    2 msg.deviceType = "senseHat";
    3 msg.deviceId ="senb74da386e6101"; //selepas senb, nombor 74da386e6101 itu awak 
                                        //boleh ambik dari mac address wlan atau eth0
    4 Return msg;
```
Di Bluemix node-red, Konfigur **nod input ibmiot** yang awak gunakan tadi (Awak boleh jer tambah yang baharu).
```
Authentication: Bluemix Service
Input Type: Device Event
Device Type: senseHat (Uncheck All)
Device Id: senb74da386e6101 (Uncheck All)
Format: json
```

Di RaspberryPi node-red, pastikan **nod output ibmiot** itu **"connected"** selepas awak **klik > Deploy**. Jika ada error, semak samaada ada nod ibmiot yang lain di situ. Dalam kes saya, saya buang semua nod ibmiot lain yang berada di node-RED raspberrypi saya selain nod ibmiot untuk gateway (hanya boleh ada satu sahaja nod ibmiot di dalam satu flow jika awak konfigur nod ibmiot sebagai gateway). Sekiranya konfigurasi telah dilakukan dengan betul, data environment daripada **SenseHat Sim** (bertindak sebagai peranti sensor) sepatutnya sedang mengalir keluar melalui **raspberrypi** (bertindak sebagai gateway) ke **nod input ibmiot Blumix** node-RED. Periksa panel debug node-RED di raspberrypi dan Bluemix, awak sepatutnya dapat melihat mesej-mesej seperti di bawah.
```
object
Data: object
Environment: object
temperature: 24.2
humidity: 69
pressure: 960
```
Awak mungkin dapat nilai temperature, humidity, dan pressure yang berbeza. Untuk menukarkan nilai data environment itu, 

Di node-RED raspberrypi, klik pada > nod Sense Hat Sim > panel info > **here** (hyperlink pada Node Help).

atau, 

letakkan URL seperti di bawah ini pada browser yang awak gunakan untuk mengakses rapberrypi.

    http://ip_address_raspberrypi_awak:1880/sensehat-simulator

Klik pada simbol **+** atau **-** untuk menukarkan nilai temperature, humidity, dan pressure tersebut.

<br/>
{:refdef: style="text-align: center;"}
![sensehat-gui]({{site.baseurl}}/assets/img/sensehat-gui.png)
{: refdef}
<br/>

#### Mempamerkan Data Environment ke Dashboard

Sebelum ini data environment: temperature, humidity dan pressure tadi awak cuma boleh melihatnya melalui panel debug sahaja. Tapi kali ini kita akan pamerkan nilai data ini pada meter dashboard di atas browser, dan boleh diakses melalui internet!

Mula-mula, install nod Dashboard. 

* Di Bluemix node-RED, **klik atas bucu kanan > burger tab > Manage Palette > Install**
* Cari modul dashboard, **Taip > node-red-dashboard. Klik > install**
* Skrol ke bawah. Cari palet Dashboard, drag dan drop **nod Button**
* Di atas bucu kanan, **klik > tab dashboard** (bersebelahan tab debug ikon serangga)
    * **Klik > butang '+ tab'**
    * Di **'Tab1', klik > edit**
        * Name: **Environment**
        * **Klik > Update**
* Klik 2 kali pada **nod Button** itu,
    * **Klik > simbol pensel > Select > Environment tab, Klik > Add > Done > Deploy**
* Untuk melihat button dashboard, 
    * Masukkan ke browser url: **https://nama_application_awak.mybluemix.net/ui/**  (nama_application_saya=iotappmegat)
    * Ataupun, awak copy paste sahaja url **"https://nama_application_awak.mybluemix.net"** ini dari url address node-RED Bluemix awak tu, paste pada halaman kosong browser, kemudian tambahkan **"/ui/"** 
    * Tekan enter

Dashboard **Environment** dengan **Button** yang di dalam kumpulan **Default** akan dipaparkan seperti imej di bawah,
<br/>
{:refdef: style="text-align: center;"}
![dashboard-button]({{site.baseurl}}/assets/img/dashboard-button.png)
{: refdef}
<br/>

Aktiviti yang seterusnya dan yang terakhir adalah mempamerkan **data Environment** (Suhu, Kelembapan, dan Tekanan) pada **Dashboard Environment**. Sila ikut arahan seperti di bawah.

Di node-RED Bluemix, Drag dan drop 3 nod function, 
* Namakan mereka **Suhu, Kelembapan** dan **Tekanan**. 
* Sambungkan mereka ke **nod input ibmiot** tadi.
Tambahkan kod berikut ke dalam **nod function** masing-masing
* suhu:

    ```javascript
    msg.payload=msg.payload.d.Data.Environment.temperature;
    return msg;
    ```
* kelembapan:

    ```javascript
    msg.payload=msg.payload.d.Data.Environment.humidity;
    return msg;
    ```
* pressure:

    ```javascript
    msg.payload=msg.payload.d.Data.Environment.pressure;
    return msg;    
    ```
<br/>
* Drag dan drop 3 nod gauge dari palet dashboard 
* Sambungkan 3 **nod gauge** ini ke **nod function** masing-masing.
* Klik 2 kali pada setiap **nod gauge** itu dan masukkan nama **Label: suhu, kelembapan dan tekanan** pada nod gauge masing-masing. 
* Select > **Group: Environment**
<br/>
{:refdef: style="text-align: center;"}
![dashboard-environment]({{site.baseurl}}/assets/img/dashboard-environment.png)
{: refdef}
<br/>
* Cuba browse dashboard di: **https://nama_app_awak.mybluemix.net/ui/**
* Buka semula **konfigurasi nod gauge** masing-masing dan laraskan julat (*Range*) unit gauge itu supaya jarumnya berada di tengah.
<br/>
{:refdef: style="text-align: center;"}
![dashboard-environment-gauge]({{site.baseurl}}/assets/img/dashboard-environment-gauge.png)
{: refdef}
<br/>
* Cuba pergi ke **Sense Hat Sim** dan ubahkan nilai-nilai **temperature, humidity, dan pressure**, nanti meter gauge awak akan berubah mengikut nilai yang awak tetapkan pada Sense Hat Sim itu (Awak kena tunggu lah sikit sehingga nilainya berubah di meter gauge). 
* Last sekali, cuba awak browse dashboard ini menggunakan mobile phone pula. Awak boleh monitor nilai suhu, kelembapan, dan tekanan dari mana-mana sahaja. Janji ada internet! (⌐■_■)

#### Tugasan Problem Solving

Maaflah. Belum abis lagi. 

Kali ini saya nak bagi awak tugasan. Sebab kalau belajar bak *Spoon Feeding* jer tak boleh mahirlah awak. Nak mahir kena *learning by doing* kemudian *learning by solving problem* kata orang putih.

Objektif yang perlu awak capai ialah,

Dapatkan 1 buah **raspberrypi 3** dan 2 buah **raspi zero**. raspi zero ni kecil dan lebih murah harganya. Oleh kerana kuasa pemprosesannya lebih rendah, awak kena install **raspbian OS versi LITE**. Kemudian awak kena install node-RED secara manual (Cuba cari maklumat di internet contohnya macam [ini](https://diyprojects.io/install-node-red-raspbian-jessie-lite-raspberry-pi-zero-w/#.XFKi9c8zaRc), tapi dalam bahasa inggerislah). Beli 1 sensor temperature macam **DS18B20**, 1 LED dan buzzer, wifi router (rumah awak ada wifi kan? kalau takda nak safe budget beli lah ethernet switch 5 port yang kecil tu, tapi wifi router harga dalam rm80 jer pun, saya rasa. Pakai hotspot handphone awak jer lah, jimat). 

Bina satu sistem supaya rasberrypi 3 ini di daftarkan sebagai **gateway** kepada 2 buah raspi zero itu yang didaftarkan sebagai **device**. Design **flow node-RED** pada raspi-raspi itu dan di Bluemix supaya apabila suhu yang di baca oleh sensor di **raspi zero 1** itu melebihi **30 darjah celcius**, node-RED bluemix akan menghantar arahan kepada **raspi zero 2** untuk menyalakan LED dan membunyikan buzzer. Pada masa yang sama **raspi zero 2** itu menghantarkan notifikasi **email** kepada awak. Pastikan data **suhu** yang dirakam oleh **sensor temperature** itu di simpan ke dalam **database cloudant** dan di pamerkan pada dashboard di bluemix.

Selamat mencuba! 










