---
layout: post
title: Sistem pengecaman plat kereta otomatik melalui Cloud API
date: 2018-10-16 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner nak, How to]
---
Untuk membina sebuah sistem pengecaman plat kereta secepat yang mungkin, maka tidak perlulah menghabiskan masa yang lama untuk cuba membina enjin pengecaman menggunakan perisian terbuka seperti OpenCV, yang belum tentu dapat menghasilkan suatu sistem yang jitu dalam masa yang singkat. Tugasan ini biarlah kita sandarkan pada para penyelidik di institusi pengajian tinggi. Setelah saya merujuk sekilas lalu pada pakcik google.com maka saya memperoleh tiga sistem pengecaman plat kereta melalui cloud API. Apa itu cloud API, maksudnya servis pengecaman yang kita kehendaki itu berjalan di dalam komputer yang berada luar negara atau mungkin dalam negara jika ada lah, menerima dan melayan permintaan dari seluruh dunia melalui internet. Melalui kajian ringkas yang telah saya lakukan, saya dapati servis yang ditawarkan oleh OpenALPR tidak dapat mengecam plat kereta Malaysia. Selain itu permintaan atau request cuma percuma sebanyak 2000/sebulan dan selepas 14 hari anda perlu letakkan maklumat credit card anda. Sudah tentu lah saya reject!. sighthound.com menawarkan 5000 API request percuma dalam sebulan berbanding platerecognizer.com cuma 2500 sahaja (untuk 50,000 request sebulan kosnya adalah USD39 sahaja). Namun buat masa ini saya memilih platerecognizer.com sebab cloud APInya lebih mudah digunapakai dan hasil pengecamannya lebih jitu

Oleh itu jom kita mendaftar akaun platerecognizer.com melalui internet browser yang popular, biasanya chrome atau firefox lah. Terngiang-ngiang di kotak minda kata-kata bekas anak murid saya, kata beliau kegunaan Internet explorer hanya untuk muat turun chrome atau firefox. Gambar di bawah adalah screenshot platerecognizer.com. Awak boleh terus mencuba mengecam plat kereta dengan memuat naik contoh gambar plat kereta. Kalau awak nak mudah, dapatkan imej plat kereta Malaysia dari internet, minta jer daripada pakcik google.com. Setelah di muat naik gambar plat kereta, klik butang biru, "Recognize". Jika anda berpuas hati dengan hasilnya, tanpa ragu-ragu, klik Sign up untuk membuka akaun secara percuma, prosesnya sangat mudah!
<br/>
<br/>

![Plate Recognizer]({{site.baseurl}}/assets/img/platerecognizerregister.jpg)
<br/>
<br/>

Setelah berjaya mendaftar akaun dan login masuk, awak akan dipamerkan dengan paparan seperti di bawah. 
<br/>
<br/>

![MobaXterm]({{site.baseurl}}/assets/img/platerecognizer-request-response.jpg){: .center-image }
<br/>
<br/>

API token adalah nombor pengenalan (ID number) unik untuk anda gunakan ketika menghantar request pengecaman. Setiap request akan di balas dengan response. Untuk menghantar satu imej plat kereta ke platerecognizer.com, awak perlu menggunakan command curl berserta data yang wajib disisip bersama. Seperti contoh di bawah.

```bash
curl -F ‘upload=@/path/to/car.jpg‘ \
-H ‘Authorization: Token put-your-token-id-here‘ \
https://platerecognizer.com/plate-reader/
```

Option -F adalah untuk menetapkan kedudukan gambar plat kereta yang awak hendak hantar. Manakala Option -H pula untuk awak maklumkan Token Id yang akan digunakan sebagai kunci mengakses masuk ke dalam platerecognizer.com. Pastikan awak semak setiap huruf, spacing dan tanda back tick ‘’ yang betul. Jika tidak tiada response dihasilkan dari platerecognizer.com.

Jika segala maklumat yang disediakan adalah betul,  selepas curl request di hantar response akan dijana sekelip mata oleh platerecognizer.com. Berikut adalah contoh response di terima.

```bash
{“filename“:”car.jpg”,“results”:[
{“box”:{“xmin”:”12“,”ymin”;”84“,”xmax”:”168“,”ymax:”380“},
”plat”:”pge9537”,”score”:0.9}] }
```
Reponse yang diterima seperti di atas adalah dalam format JSON. Maklumat plat kereta “pge9537” ini boleh diguna pakai oleh aplikasi pembangunan seperti node-red. Nilai ini kemudiannya akan dibandingkan dengan database nombor plat kereta yang telah didaftarkan di dalam raspberry pi. Raspberry pi akan bertindak menghantar maklum balas jika nombor plat yang dicam itu tiada di dalam record.

Jika awak menggunakan Mac OS atau Linux OS, buka aplikasi Terminal kemudian masukkan command curl tersebut dan awak pasti memperoleh responsenya. Untuk MS Windows, tak pasti sebab saya tak pakai MS Windows. Saya sarankan awak cuba lah linux OS. Beginilah, kalau awak nak cuba linux OS tanpa menjejaskan MS Windows kesayangan awak tu, sila install linux OS tersebut di dalam aplikasi Virtualbox. Camaner yek Virtualbox tu. Walaubagaimanapun, awak boleh skip operasi menghantar request menggunakan command curl. Kita akan lakukannya menggunakkan dalam tutorial node-red nanti.





