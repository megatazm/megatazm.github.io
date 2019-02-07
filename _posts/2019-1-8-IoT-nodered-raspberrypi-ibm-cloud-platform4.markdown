---
layout: post
title: Membina Aplikasi IoT dengan Node-RED di atas IBM Cloud Platform - Bab 4. Pengenalan Node-RED (2)
date: 2019-1-8 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---

### Mengimport dan mengeksport Flow Node-RED

Artikel [sebelum ini]({% post_url 2018-12-23-IoT-nodered-raspberrypi-ibm-cloud-platform3 %}), ada menerangkan serba sedikit berkenaan ciri-ciri dan penggunaan Array, Payload, dan JSON. Kali ini saya akan berikan lagi penjelasan berkenaan hal ini dengan sedikit mendalam. Ayuh! sila ikut arahan di bawah.

```javascript
1. Pergi ke [sini]( https://github.com/megatazm/node-red-code/blob/master/flowsample-nodered-arrayjson.txt )
2. Klik > Raw. Kemudian "Click Drag dan Copy (Ctrl+C)" semua maklumat dari situ
3. Klik simbol "+" pada bucu atas kanan kanvas untuk menambah flow kanvas yang baharu 
(Kalau awak nak memadamkannya klik > ikon hamburger > Flow > Delete)
4. Klik > hamburger ikon (di bucu kanan atas) > Import > Clipboard
5. Paste (Ctrl+V) 
6. Klik > Import
```
Nah!! dengan mudahnya awak telah menyediakan flow seperti di bawah untuk kegunaan sesi latihan praktikal ini. Awak bukan sahaja boleh mengimport masuk flow "pasang-siap" ke atas kanvas node-RED, malahan awak boleh mengeksportkannya untuk simpanan dan pengkongsian dengan rakan-rakan dan sahabat handai. Caranya lebih kurang sama sahaja dengan langkah-langkah untuk mengimport. Oleh itu saya serahkan pada awak untuk mengeksplorasikannya.

<br/>
{:refdef: style="text-align: center;"}
![nodered-arrayjson]({{site.baseurl}}/assets/img/nodered-arrayjson.png)
{: refdef}
<br/>

###  Output Data Menggunakan Array

Untuk aktiviti ini kita akan bermula dari flow yang di atas dan ke bawah satu per satu ya. Untuk aktiviti pertama, klik > nod inject ke nod function return string. Kemudian lihat hasil yang dipaparkan oleh nod debug Output.

Awak akan memperolehi error seperti ini.

```javascript
function : (error)
"Function tried to send a message of type string"
```

Ini bermaksud awak tidak boleh menggunakan cara ini untuk menyalurkan data keluar dari nod function ini. Kalau awak ingatlah, artikel sebelum ini. Untuk menyalurkan data keluar, awak perlu masukkannya ke dalam kantung **payload** dan kemudian disalurkan keluar melalui **return msg** kan? Oleh itu tukarkan kod dalam **nod return string** yang tak berguna itu dengan kod seperti di bawah yang ini, klik > Done > Deploy > inject.

```javascript
//return "This is a string";
msg.payload="This is a string";
return msg;
```
Amacam? Ada faham?   ᕙ(`▿´)ᕗ

Untuk aktiviti ke-2, **Klik > nod inject** yang memicu **nod function return string in object**. Awak akan menerima mesej "Hello Coursera" di panel debug. 

Klik 2 kali > **nod return string in object**, 

```javascript
return {"payload" : "Hello Coursera"};
```
Ini adalah cara lain (melalui objek data) untuk menyalurkan data keluar tanpa perlu menggunakan variable **msg**. Tetapi untuk memperolehi data "Hello Coursera" ini, nod penerima masih perlu mengaksesnya melalui **msg.payload**.

Aktiviti ke-3 pula, **Klik > nod inject** yang memicu **nod function Array** sebanyak 10 kali. Awak akan menerima mesej "**first message**" yang sama sebanyak 10 kali di panel debug. 

Klik 2 kali > **nod function Array**, untuk melihat kod javascriptnya.

```javascript
var msg1 = { payload:"first message" };
var msg2 = { payload:"second message" };
var msg3 = { payload:"third message" };
var msg4 = { payload:"fourth message" };
return [msg1, msg2, msg3, msg4];
```

Menurut kod di atas, ada 4 mesej string masing-masing disimpan ke dalam variable **msg1, msg2,msg3, msg4**. Kemudian penulis kod ini cuban untuk menyalurkan keempat-empat data string ini keluar menggunakan kod **return**, tetapi hanya msg1 sahaja yang berjaya disalurkan. Cuba awak tukarkan kod itu seperti berikut.

```javascript
return [msg2, msg1, msg3, msg4];
```
Klik > Done > Deploy > inject. 

Apa yang berlaku? Cuba tukar-tukarkan kedudukan variable-variable **msg** itu dan pantau hasil outputnya. Ya, awak mungkin sedang tertanya-tanya kan? Kalau begitu macam mana nak menghantar kesemua data-data ini keluar? Awak ingin tahu, sila ke aktiviti yang seterusnya.

**Klik > nod inject** yang memicu **nod function Array in Array**. Awak akan dapati keempat-empat mesej string tadi dipaparkan pada panel debug dengan sekali klik sahaja. Bagaimana ini dilakukan? Ada idea dengan apa yang dimaksudkan dengan "**Array in Array**"? Dalam Array ada Array? (;¬_¬)

Seperti biasa, Klik 2 kali > **nod function Array in Array**, untuk melihat kod javascriptnya.

```javascript
var msg1 = { payload:"first message" };
var msg2 = { payload:"second message" };
var msg3 = { payload:"third message" };
var msg4 = { payload:"fourth message" };
return [[msg1, msg2, msg3, msg4]]
```
Hmm.. ada nampak apa bezanya? Ya, ada braket bersegi tambahan mencakupi variable **msg1**, **msg2**,**msg3**, **msg4** itu tetapi keluar melalui output yang sama. Hmm.. bagaimana kalau kita nak salurkan setiap mesej-mesej itu ke output yang berbeza? Yalah, mungkin awak nak salurkan setiap satu data itu ke nod switch atau nod-nod yang berbeza pemprosesannya. Penyelesaiannya ada di aktiviti seterusnya.

**Klik > nod inject** yang memicu **nod function Multiple returns**. Awak akan dapati hanya tiga mesej string itu dipaparkan pada panel debug dengan sekali klik. Tetapi kenapa mesej yang keempat tidak disalurkan keluar? Cuba lihat kodnya di nod Multiple returns.

```javascript
var msg1 = { payload:"first message" };
var msg2 = { payload:"second message" };
var msg3 = { payload:"third message" };
var msg4 = { payload:"fourth message" };
return [msg1, msg2, msg3, msg4];
```

Tapi, kod ini tidak ada bezanya pun dengan kod di nod **Array** (tak caya cer pi check). Mesti ada perbezaan dimana-mana yang kita tak perasan, kalau tidak masakan hasilnya berbeza. Cuba awak fikirkan sejenak sambil melihat-lihat pada konfigurasi nod **Multiple returns** ini. 눈_눈

Haa.. saya dah nampak dah! ada setting untuk jumlah output di bawah  editor konfigurasi nod ini. Settingnya sekarang adalah 3 dan sebab itulah ada 3 bulatan kecil pada hujung kanan nod ini yang masing-masing bersambung dengan nod debug **Output**, **2nd Output**, dan **3rd Output**. Jika awak ndakkan "**fourth message**" juga disalurkan keluar ke panel debug, awak perlu klik **^** pada output setting untuk menambahkan jumlah output dari 3 kepada 4 output. Selepas itu awak mesti sambungkan bulatan output ke-4 itu ke salah satu nod debug tadi. Kalau awak nak sambungkan pada nod debug yang baharu pun boleh. Selepas itu,

Klik > Done > Deploy > inject.

Kalau awak nak salurkan keempat-empat mesej itu keluar melalui 3 output tanpa perlu menambah jumlah output, awak boleh gabungkan dengan teknik **Array in Array** tadi. Lihat kod di dalam nod **Multiple returns array in array**. Perbezaan kodnya hanyalah seperti berikut.

```javascript
return [msg1, [msg2, msg3], msg4];
```

Awak boleh lihat **msg2** dan **msg3** di dalam array. Array yang mengandungi **msg2** dan **msg3** ini juga adalah salah satu elemen di dalam satu lagi array yang juga mengandungi elemen **msg1** dan **msg4**. Masing-masing **msg1**, **[msg2, msg3]**, **msg4** ini disalurkan ke nod **Output**, **2nd Output**, dan **3rd Output**. 

### Membina, menghantar dan membaca mesej JSON 

Seperti yang saya telah jelaskan berkenaan format data JSON ini pada artikel [sebelum ini]({% post_url 2018-12-23-IoT-nodered-raspberrypi-ibm-cloud-platform3 %}), JSON digunakan sebagai format objek untuk menghantar data dari satu lokasi ke satu destinasi. Kenapa menggunakan JSON? Ini adalah kerana ia adalah data format yang standard digunakan pada masa kini untuk proses pertukaran data antara sistem komputer.

Aktiviti kali ini akan menerangkan berkenaan penggunaan JSON ini dengan lebih dekat lagi. Ok jom maju ke hadapan! ᕙ(`▿´)ᕗ

Klik > **nod inject** untuk memicu **nod Create JSON Object** dan **nod retrieve data from Object**. Awak akan perolehi 2 mesej seperti berikut,

```javascript
11/01/2019, 07:44:41node: Output
msg.payload : Object
{ > a: object }

11/01/2019, 07:44:41node: 3rd Output
msg.payload : string[4]
"test"
```

Mesej yang pertama yang di bawa oleh payload adalah mesej object **a**. Klik simbol "**>**" untuk melihat inti yang dikandungnya. Awak akan dapat lihat ada mesej string **"test"** yang duduk di dalam **b**.


```javascript
11/01/2019, 07:44:41node: Output
msg.payload : Object
object
a: object
b: "test"

11/01/2019, 07:44:41node: 3rd Output
msg.payload : string[4]
"test"
```

Mesej kedua yang dipamerkan oleh nod debug **3rd Output** pula memaparkan mesej string **"test"** itu tadi kerana ia telah dikupas keluar oleh nod **retrieve data from object**.

Cuba awak lihat kod yang di dalam nod **Create JSON Object**.

```javascript
msg.payload = {"a" : { "b" : "test"}};
return msg;
```
Ini adalah format untuk membina JSON object iaitu **"a"** dan **"b"** di panggil **Key** (mesti string). Manakala  **"test"** ialah **Value** atau nilainya (data jenis string, number, object, array, boolean or null). Dalam erti kata lain, ia menggunakan konsep pasangan **Key/Value**. Untuk kes ini Key **a**, nilainya adalah **{ "b" : "test"}**. Manakala untuk Key **b**, nilainya adalah **"test"**. Object JSON ni kemudiannya di simpan ke dalam **msg.payload** dan di salur keluar menggunakan kod **return msg**.

Kemudian cuba awak lihat kod dalam **retrieve data from object** pula.

```javascript
msg.payload = msg.payload.a.b;
return msg;
```
Ini adalah kod untuk "Parsing" atau mengupas keluarkan data dari JSON. Oleh kerana data **"test"** nilai Keynya adalah **"b"**. Awak kena mengaksesnya melalui **msg.payload.a.b**. Cuba awak tukarkan kod kepada ini,

```javascript
msg.payload = msg.payload.a;
return msg;
```
Apa hasil outputnya? Mengapa? 

Aktiviti seterusnya, sila klik nod **inject** untuk memicu nod **Create JSON String**. Awak akan dapat 2 mesej di panel debug seperti di bawah. mesej pertama adalah hasil dari nod output. Di sini awak dapat lihat mesejnya sama sahaja dengan yang sebelum ini. Tetapi mesej ini dipanggil JSON String sebab format JSON ini dicakupi oleh simbol **" "**. Cuba awak lihat kod di dalam nod **Create JSON String**. Nilai JSON **'{"a" : { "b" : "test"}}'** adalah dalam bentuk string (di cakupi simbol oleh **' '**) dan telah di simpan ke dalam **msg.payload**.

```javascript
msg.payload = '{"a" : { "b" : "test"}}';
return msg;
```

Oleh itu JSON ini bukan lagi dalam bentuk objek Key/Value seperti sebelum ini.

```javascript
12/01/2019, 22:57:23node: Output
msg.payload : string[23]
"{"a" : { "b" : "test"}}"

12/01/2019, 22:57:23node: retrieve data from Object
function : (error)
"TypeError: Cannot read property 'b' of undefined"
```
Oleh kerana **JSON string** ini bukan lagi **JSON objek Key/Value**, kod  **msg.payload.a.b** ini tidak boleh digunakan untuk mengakses nilai **"test"** melalui key **"a"** dan **"b"**. Maka nod **retrieve data from object** menghasilkan mesej error ke panel debug seperti yang tertera di atas. Untuk membolehkan data yang di dalam JSON string ini di kupas keluar, awak perlu menukarkannya kepada **JSON objek** terlebih dahulu.

Untuk itu, klik nod **inject** untuk memicu nod **Create JSON String in msg.payload**. Selepas awak klik nod **inject** itu, semuanya ok dan tiada lagi mesej error. Jika awak lihat kod dalam nod **Create JSON String in msg.payload** ini, awak akan dapati kodnya sama sahaja dengan kod di dalam nod **Create JSON Object**. Kalau kedua-dua kod di dalam nod-nod ini adalah sama, di mana perbezaannya? 

Bezanya adalah mesej **JSON String** yang dihasilkan oleh **Create JSON String in msg.payload** ini telah disalurkan kepada nod **json** untuk menukarkannya kepada mesej **JSON Objek** terlebih dahulu sebelum disambungkan kepada nod **retrieve data from object**. Cer awak lihat mesej pada panel debug. Awak akan dapati mesej pertama menunjukkan **JSON string** telah dihasilkan. Mesej kedua menunjukkan nod **json** telah menukarkan **JSON string** kepada **JSON objek** manakala di mesej terakhir nilai data **"test"** telah berjaya di kupas keluar oleh nod **retrieve data from object**.

Mungkin awak tertanya-tanya, apa perlunya JSON string ini. Mengapa tak gunakan sahaja JSON objek? Buang karan jer. Ini adalah kerana, sesetengah proses atau servis yang berjalan di dalam komputer memerlukan data inputnya dalam bentuk string. Contohnya, web server hanya menerima data dalam bentuk string. Oleh itu, jika awak hendak menghantar data kepada web server untuk di proses, awak mesti mengikut syarat yang ditetapkan.

Fuhh! tinggal satu lagi aktiviti selepas ini. Saya tahu awak penat. Pergilah rehat dulu, dalam 15 minit kemudian kita sambunglah semula. Kita minum dulu!! ᕕ( ᐛ )ᕗ

### Memantau status dan error nod

Selamat kembali!

Aktiviti seterusnya dan yang terakhir untuk sesi ini adalah berkaitan dengan membina nod fungsi **Status and logging functions**. Klik > nod inject untuk melihat hasil outputnya di panel debug. Awak akan perolehi 4 mesej seperti berikut.

```javascript
16/01/2019, 07:22:22node: Status and logging functions
function : (warn)
"Exiting node"

16/01/2019, 07:22:24node: entire msg
msg : Object
object
payload: "Caught error"
error: object
message: "This is an error"
source: object
id: "637f1f85.505e5"
type: "function"
name: "Status and logging functions"
count: 1
_msgid: "8528557a.72d488"

16/01/2019, 07:22:25node: Status and logging functions
function : (error)
"Second error"

16/01/2019, 07:22:25node: Output
msg.payload : string[9]
"Completed"
```

Kalau awak perasanlah. Selepas sahaja awak klik nod inject, pada ketika awak menerima mesej di atas, awak juga akan dapat melihat animasi text **"started"**, **"stage 1"** (dengan icon merah), dan **"stage 2"** (dengan ikon hijau) di bucu kiri bawah nod **Status and logging functions** itu. 

Jom kita kaji mesej output ini dengan lebih dekat. Mesej pertama datang dari nod function **Status and logging functions**. Manakala outputnya iaitu mesej string **"Exiting node"** dihasilkan oleh fungsi **warn** dari dalam nod ini. Mesej kedua pula datangnya dari nod debug **entire msg** (nod ini bersambung dengan nod catch **Catch node**). Mesej outputnya adalah dalam bentuk objek dengan mesej payload **"Caught error"** dan mesej error **"This is an error"**. Mesej ketiga datangnya dari nod function **Status and logging functions** dengan output **"Second error"** yang dihasilkan oleh fungsi **error** dari dalam nod ini. Mesej keempat dan yang terakhir, datangnya dari nod debug **Output** dengan mesej string "Completed".

Untuk mengetahui bagaimana mesej-mesej ini dihasilkan, lihat kod yang di dalam nod function **Status and logging functions** seperti tertera yang di bawah. 

{% highlight javascript linenos %}
node.status({text:"started"});//"started" dipamerkan selamat 1 saat

setTimeout(function() {
    node.status({fill:"red",shape:"ring",text:"stage 1"});//"ring" merah dipamerkan selama
                                                          // 1 saat
    
    setTimeout(function() {
        node.status({fill:"green",shape:"dot",text:"stage 2"});//"dot" hijau dipamerkan 
                                                               // selama 1 saat
        node.error("This is an error", {'payload' : 'Caught error'}); 
        
        setTimeout(function() {
            node.error("Second error");
            node.status({});
            node.send({'payload' : 'Completed'});
        }, 1000);
        
    }, 1000);
    
}, 1000);

node.warn("Exiting node");
return;
{% endhighlight %}

Pertama sekali, lihat kod **node.status** yang berada ni barisan **1**, **4**, dan **7** dan kod fungsi **setTimeout(function(){}..}, 1000)** di barisan **3**, **6**, dan **10** (nested setTimeout Function). Animasi yang awak nampak tadi itu adalah hasil daripada kod **node.status** itu.

```javascript
1: node.status({text:"started"});//lihat mesej "started"
4: node.status({fill:"red",shape:"ring",text:"stage 1"});//lihat mesej "stage 1" dengan setting ikon bentuk "ring" dengan warna "red"
7: node.status({fill:"green",shape:"dot",text:"stage 2"});//lihat mesej "stage 2" dengan setting ikon bentik "dot" dengan warna "green"
```
Jika awak perhatikan dengan teliti, awak akan dapati setiap satu mesej dan animasi itu dipaparkan dengan sedikit kelewatan atau **delay** lebih kurang dalam satu saat. Fungsi delay ini dihasilkan oleh kod fungsi **setTimeout(function(){}..}, 1000)**. Nilai **1000** itu adalah dalam unit **millisecond** bersamaan dengan **1 second** (1 sec = 1000ms). Mengapa saya katakan kod fungsi **setTimeOut()** ini adalah dalam keadaan **"Nested Function"**? Ia adalah kerana di dalam kod fungsi **setTimeOut()** ini ada 2 kod fungsi **setTimeOut()** di dalamnya (Function di dalam function). Perhatikan struktur braket "**{ }**" dengan teliti, yang mana satu berada di luar dan di dalam (kod yang berada di luar akan di proses terlebih dahulu). Cuba awak tukar-tukar nilai mesej string, warna dan jenis ikon dan ubah masa delaynya. Mungkin awak akan faham maksud saya. 

Selain daripada kod fungsi **node.status**, cer lihat pada kod **node.error**, **node.send**, dan **nod.warn**. Bandingkan kod-kod ini dengan hasil mesej yang awak perolehi di panel debug tadi. Fungsi kod **node.error** adalah untuk menghasilkan kod error.

```javascript
8: node.error("This is an error", {'payload' : 'Caught error'});
11: node.error("Second error");
```
Oleh kerana kod **node.error** di barisan 8 ini berada di dalam kod fungsi **setTimeOut()** yang kedua, mesej error ini akan dihasilkan terlebih dahulu berbanding dengan mesej dari kod **node.error** di barisan 11 yang berada di dalam **setTimeOut()** yang ketiga (di dalam **setTimeOut()** yang kedua). Cuma kod di barisan 8 ini akan menghasilkan mesej error **"This is an error"** dalam bentuk objek kerana ada nilai tambahan iaitu json objek **{'payload' : 'Caught error'}** berbanding dengan mesej error **"Second error"** di **node.error** di barisan 11 itu. Oleh kerana kod di barisan 8 menghasilkan objek error maka error mesej ini akan **"ditangkap"** oleh nod **Catch node** kemudian disalurkan ke nod **entire msg** (Ini sangat bagus dalam pengurusan mesej-mesej error atau log untuk suatu aplikasi yang komplex). Sebaliknyanya error mesej **"Second error"** dari **node.error** di barisan 11 itu dihasilkan oleh nod **Status and logging functions**. Kod **node.send** pula digunakan untuk menyalurkan mesej string **'Completed'** ke nod debug **Output**. Ini adalah mesej yang terakhir sampai ke panel debug (ini merupakan mesej payload untuk output). 

Akhir sekali, kod **node.warn** di barisan 20 itu menghasilkan mesej string amaran **"Exiting node"** dari nod **Status and logging functions** dan di hantar ke panel debug. Hmm.. tapi saya rasa macam peliklah.. Sepatutnya mesej ini adalah mesej yang terakhir muncul di panel debug sebab kodnya berada di barisan terakhir iaitu sebelum kod **return**. Tambahan lagi, kalau mengikutkan tujuan mesej ini yang dinamakan **"Exiting node"**, ia bermaksud proses sudah tamat dan perlu keluar dari nod **Status and logging functions** ini. Kenapa mesej **"Exiting node"** ini dipaparkan terlebih dahulu berbanding dengan mesej-mesej lain? Ini adalah kerana kod function **setTimeOut()** adalah merupakan **asynchronous function**. Jika ianya adalah **synchronous function**, komputer perlu menunggu delay selama 1 saat untuk setiap proses di dalam **setTimeOut()**. Oleh kerana kita ada 3 function **setTimeOut()** yang delaynya adalah 1 saat setiap satu, maka mesej **"Exiting node"** ini akan dipaparkan selepas 3 minit. Oleh kerana function ini adalah asynchronous, komputer terus boleh menjalankan kod **node.warn** ini tanpa perlu menunggu sehingga selepas 3 saat. Maka begitulah ceritanya. 

Dengan ini maka tamatlah sesi pengenalan node-RED yang mungkin dapat membantu untuk awak maju ke tahap yang seterusnya. Selepas ini saya rasa kita patut buat sesuatu yang lebih praktikal sedikit supaya ia mungkin boleh menjadi asas untuk di guna pakai oleh awak bagi membina suatu aplikasi yang berguna. Untuk tujuan ini [jom! ke sini]({% post_url 2019-1-16-IoT-nodered-raspberrypi-ibm-cloud-platform5 %}).
 






