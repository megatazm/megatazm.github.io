---
layout: post
title: Membina Aplikasi IoT dengan Node-RED di atas IBM Cloud Platform - Bab 3. Pengenalan Node-RED
date: 2018-12-22 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---

### Node-RED Flow Editor

Jika awak telah mengikuti artikel [sebelum ini]({% post_url 2018-12-14-IoT-nodered-raspberrypi-ibm-cloud-platform2 %}), Node-RED flow editor sepatutnya telah siap sedia berada di depan awak untuk di godek. Sebelum itu, saya berikan sedikit penerangan berkenaan interface Node-RED flow editor ini.

<br/>
{:refdef: style="text-align: center;"}
![nodered-interface2]({{site.baseurl}}/assets/img/nodered-interface2.png)
{: refdef}
<br/>

Merujuk pada imej interface Node-RED di atas, setiap flow terdiri daripada gabungan beberapa nod dan sambungan di antara nod-nod di atas kanvas. Setiap nod-nod yang berbeza mempunyai keupayaannya yang tersendiri mengikut keperluan untuk memproses data yang melalui input hingga ke output flow yang awak bina. Nod-nod itu boleh di pilih dari panel di sebelah kiri yang di panggil palet. Jika nod yang ingin di guna tiada di dalam senarai, awak boleh "install" atau memasangkannya untuk ditambahkan ke dalam palet tersebut. Untuk menambahkannya klik **> ikon hamburger** di bucu kanan atas skrin **> Manage Pallet >** Skrol dan pilih nod yang awak inginkan. Manakala panel **info** di sebelah kanan pula membolehkan awak memperolehi maklumat berkenaan nod-nod yang berada di atas kanvas. Klik pada salah satu nod di atas kanvas itu, maklumat berkenaan nod tersebut akan di paparkan pada panel **info**. Panel **Debug** (klik > **ikon serangga** sebelah **info**) pula digunakan bersama-sama nod debug yang disambungkan dengan mana-mana nod yang ingin awak pantau atau periksa hasil outputnya. Ini berguna dalam proses mengenal pasti masalah.

Jom cuba guna aplikasi contoh Node-RED ini. Mula-mula lakukan operasi berikut.

```javascript
1. Klik > [Send Data] node
2. Periksa pada panel info
   Information: Maklumat berkenaan nod seperti id, nama dan jenis
   Node Help: Penerangan berkenaan nod
   Node output: Output yang boleh dikonfigurasikan
   Details: Maklumat lanjut berkenaan nod
3. Klik 2 kali > [Send Data] node
   Panel konfigurasi nod dipaparkan
4. Klik > Done
```

Sekarang awak sudah tahu memperolehi maklumat berkenaan nod dan juga memaparkan panel untuk mengkonfigurasikan nod. Mari kita mengkonfigurasikan nod output IBM IoT yang bernama **Send to IBM IoT Platform**.

```javascript
1. Klik 2 kali > nod [Send to IBM IoT Platform]
2. Pada paparan panel konfigurasi nod, 
   Authentication: Pilih > Quickstart. (Untuk persekitaran "sandbox")
3. Klik > Done
4. Klik > Deploy (Butang berwarna merah di bucu atas kanan skrin). Bulatan kecil
   berwarna biru pada bucu atas kanan nod [Send to IBM IoT Platform] akan hilang.
```

Pastikan ada mesej **successfully deployed** dipamerkan selepas awak klik butang deploy. Konfigurasi **quickstart** yang awak pilih tadi bertujuan untuk memudahkan awak mencuba bermain dengan nod output IBM IoT Platform ini. Seterusnya lakukan aktiviti berikut:-


```javascript
1. Klik > butang kelabu di hujung kanan nod [Debug output payload]. Butang itu
   akan bergerak ke kanan dan bertukar menjadi hijau. Ini mengaktifkan nod debug
   untuk mempamirkan mesej ke panel debug. 
2. Klik > ikon serangga atau tab debug untuk mengaktifkan panel debug. Debug
   membolehkan awak melihat mesej yang mengalir melalui nod-nod tersebut. 
3. Seterusnya, klik > Deploy.
4. Untuk mengalirkan mesej secara manual melalui nod-nod itu, klik > butang
   kelabu pada hujung kiri nod [Send Data]. Sejurus itu, awak akan dapat melihat
   informasi dipaparkan pada panel debug.
5. Untuk mengkonfigurasikan nod [Send Data] supaya menghantar mesej itu setiap 1
   saat, Klik > 2 kali nod [Send Data], kemudian setkan Repeat:"interval".  
6. Klik > Done > Deploy > Send
```
Mesej akan melimpah-limpah keluar di panel debug. Klik **> ikon tong sampah** di panel debug untuk memadamkan mesej-mesej itu. Tapi, mesej masih lagi keluar mencurah-curah setiap 1 saat. Macam mana yek nak hentikannya? Bak kata pelawak si Nabil tu. Lu pikirlah sendiri!

### Mesej Output Payload 

Sudah berjaya menghentikan kebanjiran mesej-mesej tadi? Bagus. Seterusnya kali ini jom kita tengok mesej-mesej ini dengan lebih dekat. Salah satu daripada mesej ini adalah seperti di bawah. Persoalan yang harus bermain di dalam kepala awak, apakah maklumat yang terkandung dalam mesej ini? Dari mana datangnya mesej ini?

```javascript
"{"d":{"temp":17,"humidity":55,"location":{"longitude":-98.49,"latitude":29.42}}}”
```

Mesej yang awak terima di panel debug ini adalah mesej dalam bentuk format yang di panggil JSON (Java Script Object Notation). JSON adalah format yang popular buat masa kini untuk menyimpan data dalam satu kantung objek yang digunakan untuk mengangkut data mengalir melalui nod-nod dari satu punca input ke satu destinasi output. Awak nak tau dari mana datangnya mesej ini? Klik 2 kali pada nod Function, **Device payload**. Haa ye, mesej itu sebenarnya datang dari nod function **Device Payload**. Nod inject **Send Data** berfungsi hanyalah sebagai pencetus kepada nod function yang berada disebelahnya. Apabila awak menyuntik nod **Send Data**, ia menyebabkan kod javascript di dalam nod function itu berfungsi lalu menghasilkan data dan di simpan dalam bentuk format JSON. Ia kemudiannya disalurkan keluar ke nod debug dan dipamirkan di panel debug.
<br/>

{% highlight javascript linenos %}
// Thermostat's location:
var longitude1 = -98.49;
var latitude1 = 29.42;

// Array of pseudo random temperatures
var temp1 = [15,17,18.5,20,21.5,23,24,22.2,19,18];

// Array of pseudo random relative humidities
var humidity1 = [50,55,61,68,65,60,53,49,45,47];

// Counter to select from array.
var counter1 = context.get('counter1')||0;
counter1 = counter1+1;
if(counter1 > 9) counter1 = 0;
context.set('counter1',counter1);

// Create MQTT message in JSON
msg = {
  payload: JSON.stringify(
    {
      d:{
        "temp" : temp1[counter1],
        "humidity" : humidity1[counter1],
        "location" :
        {
          "longitude" : longitude1,
          "latitude" : latitude1
        },
      }
    }
  )
};
return msg;
{% endhighlight %}

Kepada yang tidak pernah belajar programming atau pengaturcaraan, mungkin awak tidak mengerti maksud bait-bait perkataan bahasa Inggeris seperti yang dinyatakan di atas. Kepada yang pernah belajar programming, saya rasa kod javascript di atas ini agak mudah untuk awak fahami. Takpa, kepada yang tak mengerti hal programming, awak ikut jer. Sebabnya cara untuk belajar programming adalah dengan melakukannya, Learning by Doing! Mula-mula meniru contoh, menghafal dan memodifikasikan kod mengikut keperluan. Awak tak perlu pun ada keputusan exam 10A untuk jadi seorang programmer yang mahir. Janji, awak sanggup berusaha dengan semangat kesabaran dan keazaman yang tinggi. 

Pertama sekali, cuba awak bandingkan data **longitude** dan **latitude** yang di dalam JSON dengan kod yang di dalam nod function (kod di barisan ke-2 dan ke-3). Awak akan dapati nilai **-98.49** dan **29.42** masing-masing disimpankan ke dalam variable atau pembolehubah **longitude1** dan **latitude1**. Seterusnya, cuba awak lihat pada barisan kod yang ke-6 dan ke-9. Awak akan dapati 2 jajaran nombor dengan jujukan yang berbeza-beza ini masing-masing disimpankan ke dalam variable atau pembolehubah **temp1** dan **humidity1**. Jajaran nombor ini di panggil **Array**. Cuba awak klik butang nod [Send Data] berulang kali sebanyak 11 kali. Bandingkan nilai-nilai **longitude**, **latitude**, **temp** dan **humidity** yang awak perolehi di panel debug dengan kod di barisan 2,3,6 dan 9. Cuba fikirkan sejenak. Ada mentol menyala dalam minda awak sekarang?

Jika perhatikan betul-betul nilai-nilai pada panel debug, awak akan dapati nilai **longitude** dan **latitude** adalah tetap sama (awak boleh agak kenapakan?) tetapi nilai-nilai **temp** dan **humidity** berubah-rubah mengikut pasangan yang sama dengan turutan jujukan array pada **temp1** dan **humidity1**. 


|<center>Klik Send Data</center> | <center>temp</center> | <center>humidity</center> |
|------ | ----- | ----- |
| <center>1</center>| <center>17</center> | <center>55</center>|
| <center>2</center> | <center>18.5</center> | <center>61</center>|
| <center>3</center> | <center>20</center> | <center>68</center>|
| <center>4</center> | <center>21.5</center> | <center>65</center>|
| <center>5</center> | <center>23</center> | <center>60</center>|
| <center>6</center> | <center>24</center> | <center>53</center>|
| <center>7</center> | <center>22.2</center> | <center>49</center>|
| <center>8</center> | <center>19</center> | <center>45</center>|
| <center>9</center> | <center>18</center> | <center>47</center>|
| <center>10</center> | <center>15 </center> | <center>50</center>|
| <center>11</center> | <center>17 </center> | <center>55</center>|

Merujuk pada jadual di atas. Jika awak bandingkan turutan data **temp** dan **humidity** dengan variable **temp1** dan **humidity1**, sepatutnya data yang dihasilkan selepas awak klik butang nod [Send Data] pada kali **ke-1** adalah **temp=15** dan **humidity=50**, tetapi nilai ini hanya muncul pada klik yang **ke-10**. Seterusnya pada klik yang **ke-11** nilai yang sama akan di ulangi semula seperti pada nilai **ke-1** dan seterusnya. Mengapa? Rahsianya berada pada kod di barisan 12, 13, 14, 15, 22 dan 23.

Untuk memecahkan rahsia ini. Pertama, awak perlu tahu rahsia berkenaan ciri-ciri  **Array** terlebih dahulu. Dari segi analoginya, array ini adalah ibarat dulang panjang yang duduk di atas telapak tangan seorang pelayan restoran sedang menghidangkan air minuman. Andaikan di atas dulang itu ada 5 cawan minuman beraneka rasa. Cawan minuman yang berada di depan sekali ialah air sirap limau, yang kedua - air limau nipis, ketiga - air sirap bandung, keempat - air teh tarik, dan kelima - air teh o. Dalam konteks array, setiap satu jenis air ini di panggil **Elemen**. Oleh itu nombor-nombor yang disimpan ke dalam variable **temp1** dan **humidity1** itu adalah masing-masing merupakan elemen-elemen untuk 2 array yang berbeza. Manakala kedudukan air minuman di atas dulang itu pula di panggil **Index**. Tetapi dalam konteks array, kedudukan elemen-elemen itu bermula dengan index nombor 0, 1, 2, 3 dan 4. Fakta ini diperjelaskan seperti jadual di bawah.

|<center>Index</center> | <center>Elemen temp1</center> | <center>Elemen humidity1</center> |
|------ | ----- | ----- |
| <center>0</center>| <center>15</center> | <center>50</center>|
| <center>1</center>| <center>17</center> | <center>55</center>|
| <center>2</center>| <center>18.5</center> | <center>61</center>|
| <center>3</center>| <center>20</center> | <center>68</center>|
| <center>4</center>| <center>21.5</center> | <center>65</center>|
| <center>5</center>| <center>23</center> | <center>60</center>|
| <center>6</center>| <center>24</center> | <center>53</center>|
| <center>7</center>| <center>22.2</center> | <center>49</center>|
| <center>8</center>| <center>19</center> | <center>45</center>|
| <center>9</center>| <center>18</center> | <center>47</center>|

Ok jom kita buat sedikit analisis pada kod di barisan 12, 13, 14 dan 15 tadi satu persatu. Pernyataan di barisan 11 adalah "comment" yang menerangkan bahawa kod di bawah bertujuan untuk membuat "counter" sebagai nombor index untuk memilih element daripada array (apa-apa sahaja selepas simbol "**//**" di anggap sebagai bukan kod tetapi adalah komen yang diabaikan dan tidak diproseskan oleh komputer).

```javascript
12: var counter1 = context.get('counter1')||0;
```
Kod **var counter1** ini mengarahkan supaya komputer mencipta variable **counter1** di memori RAM. Manakala kod **context.get('counter1')||0** pula mengarahkan supaya memdapatkan nilai daripada variable **counter1**. Jika variable **counter1** masih belum menyimpan apa-apa nilai, maka masukkan nilai **0** sebagai nilai permulaan. Kemudian, nilai **0** ini disimpankan ke dalam variable **counter1** dengan menggunakan symbol operator "**=**".

```javascript
13: counter1 = counter1+1;
```
Kod ini mengarahkan supaya nilai **counter1** itu di tambah sebanyak satu. Jika awak menyuntik nod [Send Data] buat kali ke-1. Nilai **counter1** di sini akan "**=**" dengan "**0 + 1**" bermaksud nilai index akan bermula dengan "**1**". Inilah rahsianya kenapa bila awak klik nod [Send Data] pada kali ke-1, nilai yang diperolehi adalah **temp=17** dan **humidity=55** (lokasi di index 1) dan tidak bermula dengan nilai **temp=15** dan **humidity=50** (lokasi di index 0). Puncanya adalah kerana nombor index array itu bermula dengan nombor "**1**" bukan "**0**". 

```javascript
14: if(counter1 > 9) counter1 = 0;
```
Setiap kali awak klik butang nod [Send Data], nilai **counter1** akan ditambahkan sebanyak satu (bermula dari **1,2,3...9**). Kod ini mengarahkan supaya jika nilai **counter1** adalah lebih besar ( "**>**" ) daripada **9** (iaitu 9 + 1 = 10), maka resetkan nilai **counter1** kepada nilai **0** (iaitu index = 0). Inilah rahsianya kenapa pada klik yang ke-10, nilainya adalah **temp=15** dan **humidity=50**.

```javascript
15: context.set('counter1',counter1);
```
Kalau kod di barisan ke-12 menggunakan **context.get('counter1')** untuk mendapatkan nilai dari variable **counter1**, kod **context.set('counter1',counter1)** di barisan ke-15 ini pula menetapkan nilai yang sekarang berada di dalam variable **counter1** pada context bernama **'counter1'** (boleh jer pakai nama lain dengan syarat kedua-dua context.get dan context.set mesti mengakses nama context yang sama). Penggunaan kod **"context"** ini bermaksud nilai yang awak simpan ke dalam variable **counter1** itu kekal di dalam nod function ini. Dengan itu setiap kali awak klik butang nod [Send Data], nilai **counter1** akan meningkat sebanyak 1. Cuba letak symbol comment "//" di depan kod barisan ke-15 itu. Kemudian klik > Done > Deploy > Send Data. Apa yang berlaku? Mengapa?

```javascript
15: // context.set('counter1',counter1);
```
Fuhh! harap-harap awak dapatlah perolehi kefahaman. Cuba godek-godek, main-main, tukar itu ini. Pastu klik > Done > Deploy kemudian analisakan apa yang berlaku dan cuba fikirkan mengapa yek? 

Seterusnya untuk penghabisan kod ini. Barisan Kod ke-18 hingga ke-32 adalah untuk menyimpan data dari variable **temp1**, **humidity1**, **longitude1** dan **latitude1** ke dalam format JSON (data di simpan di dalam kurungan "**d**"). Data yang di dalam kurungan "**d**" itu kemudiannya disimpankan ke dalam kantung "**payload**" menggunakan fungsi **JSON.stringify** (dihasilkan dalam bentuk data jenis "String") yang kemudiannya di simpan ke dalam variable **msg**. Mesej berformatkan JSON String ini akhirnya disalurkan keluar melalui kod **return msg;** yang berada di barisan terakhir.

### Menghantar Mesej ke Nod Input IBM IoT

Jika sebelum ini awak telah mesej ke panel debug, kali kita akan gunakan Nod Output IBM IoT untuk menghantar ke Nod Input IBM IoT. Secara praktikalnya, awak boleh menghantar mesej dari satu peranti ke satu peranti yang lain dengan menggunakan nod output dan input IBM IoT ini. Untuk tujuan latihan cuba guna, saya tunjukkan cara penggunaanya di atas cloud platform yang sama.










