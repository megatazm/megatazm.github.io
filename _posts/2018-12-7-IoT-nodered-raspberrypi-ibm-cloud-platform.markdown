---
layout: post
title: Membina Aplikasi IoT dengan Node-RED di atas IBM Cloud Platform - Bab 1. Pengenalan IoT & Cloud Platform
date: 2018-12-6 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---

### Apa itu IoT? 

IoT atau Internet of Things. Internet Benda? Internet Kebendaan? Hmm.. tak perlulah diterjemahkan. Kita cuma perlu fahamkan konsepnya sahaja, gunakan sahaja perkataan bahasa inggeris tu. Saya rasa semua orang tahu kan apa itu "Internet". Kalau takda internet, tak blehlah nak main game, hantar mesej whatapps, hantar status IG, melayan channel youtube. Servis-servis ini dijana oleh aplikasi-aplikasi yang berputar pada komputer server dan berada di luar sana, di mana? di "Awan" (sebab awak tidak tahu di mana). Melalui infrastuktur jaringan internet yang dibina oleh syarikat-syarikat telekomunikasi di dalam dan di luar negaralah yang membolehkan awak mencapai servis-servis ini. Untuk awak mencapai servis-servis kegemaran awak ini, awak perlulah memiliki peranti seperti handphone atau komputer. 

Ok, kalau begitu apa bezanya Internet of Thing ini berbanding penggunaan internet sebelum ini. IoT bermaksud benda-benda selain handphone dan komputer (mereka ini juga adalah peranti IoT) yang ada kaitannya untuk manusia disambungkan pada internet. Cuba awak bayangkan, di masa hadapan jumlah peranti yang bersambung dengan internet akan meningkat secara drastik!. Untuk apa disambungkan benda-benda ini? apa faedahnya? Ya,ia dikatakan memberi manfaat dan kemudahan kepada kehidupan pengguna, tapi ingat! Kalau ia sekadar memberi kemudahan dan faedah kepada pengguna sahaja tanpa manfaat kepada perniagaan dan pemerintah, teknologi ini tak akan berkembang dan dikembangkan. Mengapa IoT sangat popular sekarang? Cuba lihat pada imej di bawah. "Collect, Analyze and Act", tiga patah perkataan bahasa inggeris bermaksud mengumpul dan menganalisa sesuatu, kemudian bertindak balas berdasarkan pada dapatan analisa tersebut. Apakah dia "sesuatu" itu yang membolehkan kita bertindak dengan lebih cepat dan tepat? Ya! bahan yang sangat bernilai di alaf kini, ia adalah "Data".


 <br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/iot-collect-analyze-act.png)
{: refdef}
<br/>

Oleh kerana peranti-peranti IoT ini disambungkan dengan internet, maka data-data yang mereka hasilkan dengan mudah boleh dikumpul, disalur dan disimpan ke dalam komputer server yang berperisian database. Jenis-jenis data yang dikumpulkan adalah bergantung kepada jenis-jenis sensor yang dipasang pada peranti IoT itu. Seperti contoh, jika awak memasang sensor suhu dan kelembapan pada raspberry pi, siang malam raspberry pi akan mengumpulkan data suhu dan kelembapan di persekitaran peranti itu untuk awak. Apabila data-data ini telah di kumpul dengan cukup banyak di dalam pusat data, data ini kemudian di analisa supaya data tersebut menjadi maklumat yang berguna untuk membuat sesuatu keputusan yang penting seperti memaklumkan amaran awal berkenaan banjir, tsunami, gempa bumi dan macam-macam lagi.

### Pengenalan kepada Cloud Computing

Saya masih menggunakan terma "Cloud Computing" tanpa perlu mengguna-pakai perkataan "Pengkomputeraan Awan". Bagi saya tak perlulah nak terjemah semua benda kepada Bahasa Malaysia. Perkataan "Cloud Computing" ini telahpun menjadi trend di mana-mana pun di dunia ini termasuk di Malaysia. Ok cukuplah mengomel di sini. 

Apa itu "Cloud Computing"? Sila rujuk pada imej di bawah.

Cloud computing, atau boleh juga di panggil sebagai "Utilities Based Computing", membolehkan awak memperolehi pelbagai sumber pengkomputeraan iaitu penggunaan penyimpanan data, rangkaian komputer, CPU, database, sistem operasi dan pelbagai aplikasi seperti mana awak menggunakan sumber utiliti seperti air, elektrik, telepon dan gas. Tanpa perlu melabur dengan kos yang tinggi, awak cuma perlu bayar berdasarkan pada jumlah sumber pengkomputeraan yang telah di pakai sahaja!
 
 <br/>
{:refdef: style="text-align: center;"}
![cloud-computing]({{site.baseurl}}/assets/img/cloud-computing.png)
{: refdef}
<br/>

Ada tiga kategori servis dalam cloud computing iaitu SaaS (Software as a Service), PaaS (Platform as a Service), dan IaaS (Infrastructure as a Service). Seperti yang dinyatakan oleh imej di bawah, melalui SaaS, kita boleh menggunakan aplikasi-aplikasi yang berada di cloud. Awak pun mungkin sudah pun menggunakan aplikasi tersebut seperti, gmail, whatapss, facebook, google drive, IG dan macam-macam lagi aplikasi yang awak boleh guna melalui web browser atau pun mobile app tanpa perlu memasang keseluruhan sistem aplikasi tersebut ke dalam komputer atau mobile phone. PaaS pula adalah cloud platform atau persekitaran yang di bina di "awan" digunakan untuk membina aplikasi cloud. Para pembina aplikasi menggunakan cloud platform ini untuk memudahkan mereka supaya lebih memberi fokus pada proses membina, memantau dan mengemas kini aplikasi dengan lebih cepat, efisyen dan kos efektif. Manakala IaaS pula membolehkan sesebuah syarikat memperolehi capaian untuk mengguna pelbagai sumber pengkomputeraan berdasarkan pada keperluan semasa tanpa memerlukan mereka melabur dengan kos yang tinggi bagi memiliki infrastuktur pengkomputeraan itu secara fizikal. 

<br/>
{:refdef: style="text-align: center;"}
![cloud-model]({{site.baseurl}}/assets/img/cloud-models-detail.jpg)
{: refdef}
<br/>

Pemilik IaaS mempunyai kuasa penuh terhadap infrastruktur pengkomputeraan secara virtual. Mereka menggunakan sumber-sumber pengkomputeraan virtual itu bagi membangun cloud platform mereka sendiri untuk langganan pihak pembina aplikasi. Ada kemungkinan juga para pembina aplikasi ini menggunakan IaaS itu untuk membangunkan cloud platform mereka sendiri dan membina aplikasi cloud diatasnya. Gambarajah di bawah menunjukkan perbezaan dari segi kuasa kebolehkawalan di antara infrastruktur di dalam permis, IaaS, PaaS dan SaaS. Jika awak bekerja di syarikat yang memiliki infrastruktur pengkomputeraan secara fizikal, awak bertanggungjawab untuk mengawal selia keseluruh lapisan servis, dari bawah sampai ke atas. Hebat! Mungkin awak bekerja dengan Google kot. Jika awak bekerja dengan syarikat yang menggunakan IaaS, awak tak perlulah nak menghadap mengawal selia lautan infrastruktur pengkomputeraan fizikal. Awak boleh mengawal selia infrastruktur pengkomputeraan itu secara virtual di mana-mana saja awak berada! janji ada internet. Kalau awak menggunakan PaaS untuk membina aplikasi, awak tak perlu risaukan tentang konfigurasi dan mengawal selia sistem operasi, networking, penyimpanan data, database, versi kod, dan banyak lagi infrastruktur sokongan yang awak perlukan. Awak cuma perlu fokus pada membina, memantau, menyebar, dan mengemas kini aplikasi, sangat produktif. SaaS pula memudahkan awak menjadi seorang pengguna yang hebat. Awak cuma perlu ada sambungan internet sahaja, macam-macam aplikasi cloud (gmail, gdrive, fb, youtube, instagram, twitter, dll) yang awak boleh pakai, di mana-mana sahaja awak berada. Walaupun awak sedang berada di dalam bilik "termenung"!


 <br/>
{:refdef: style="text-align: center;"}
![cloud-service-model]({{site.baseurl}}/assets/img/cloud-service-model.png)
{: refdef}
<br/>

Gambarajah di bawah adalah contoh syarikat-syarikat gergasi yang menawarkan servis cloud computing IaaS, PaaS dan SaaS. Ada satu lagi syarikat gergasi untuk servis PaaS yang ndak saya perkenalkan tapi tiada pada gambarajah di bawah, iaitu IBM Cloud Platform. Selepas ini kita akan gunakan PaaS IBM ini untuk membina aplikasi menggunakan node-RED di atas IBM Cloud Platform "Bluemix", yang kemudiannya dikonfigurasikan untuk berkomunikasi dengan node-RED raspbery pi. Dengan ini awak boleh mengawal dan memantau raspberry pi dari mana-mana sahaja! janji ada internet. Tapi sebelum itu, saya perlu perkenalkan awak dengan IBM Cloud Platform Bluemix terlebih dahulu. Nak tau camaner? [Sila la ke sini]({% post_url 2018-12-14-IoT-nodered-raspberrypi-ibm-cloud-platform2 %}).

<br/>
{:refdef: style="text-align: center;"}
![cloud-company]({{site.baseurl}}/assets/img/cloud-company.jpg)
{: refdef} 
<br/>











