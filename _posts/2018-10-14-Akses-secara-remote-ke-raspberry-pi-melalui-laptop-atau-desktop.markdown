---
layout: post
title: Akses raspberry pi secara remote melalui laptop atau desktop
date: 2018-10-14 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camner Nak, How to]
---
Kebolehan untuk mengakses komputer secara remote melalui internet sangat penting dalam menjalankan pengurusan sistem komputer dengan berkesan dan efisien. Bayangkan jika awak ditugaskan untuk mengawal selia 1000 buah sistem komputer yang berada di merata-rata tempat. Pengaksesan secara remote bukan sahaja memudahkan tugasan awak, ia juga menjimatkan kos operasi syarikat. Bila kos operasi rendah, syarikat memperoleh keuntungan lebih, bonus pun dapat lebih. Untuk membolehkan raspberry pi menerima akses secara remote melalui wifi router dari komputer lain, aplikasi SSH perlu diaktifkan terlebih dahulu. Selepas itu awak perlu menyambungkan wifi raspberry pi ke wifi router tanpa memerlukan keyboard, mouse dan monitor, gimana dong?. Berikut adalah langkah-langkahnya:-

* Perkakas yang diperlukan ialah, Wifi router, kabel ethernet, raspberry pi beserta wifi adapter, 5V USB power supply/power bank,
  SD card mini 16GB + Raspbian OS dan komputer/laptop.
* Download dan install perisian [Angry IP Scanner](www.google.com) ke dalam komputer. Awak akan gunakan perisian ini untuk mengimbas dan mendapatkan
  IP address raspberry pi. Setiap komputer mesti memerlukan IP address iaitu suatu nombor ID yang unik untuk berkomunikasi. Bayangkan awak memanggil Rahman! di sebuah shopping komplex, mungkin ada lebih dari seorang akan menyahut. Berita baik, jika awak menginap di penjara, awak akan diberikan nombor id yang unik!
* Jika awak menggunakan MS Windows. Saya cadangkan awak download perisian MobaXterm. Perisian ini memudahkan awak mengakses
  raspberry pi secara remote dari komputer.
* Masukkan SD card yang telah dimuat dengan Raspbian OS melalui SD Card reader ke komputer. 
* Klik masuk ke dalam SD card tersebut, seterusnya klik masuk ke dalam direktori /boot. Kemudian ciptakan satu text file kosong
  yang dinamakan ssh.
* Ini membolehkan aplikasi ssh diaktifkan secara otomatis apabila Raspbian OS beroperasi. Aplikasi ssh membolehkan komputer dari
  luar mengakses masuk ke dalam raspberry pi.
* Cucuk masuk power supply 5V pada raspberry pi untuk menghidupkan (boot up) Raspbian OS. Tunggu sehingga led hijau tidak 
  berkelip-kelip lagi.
* Cucuk kabel ethernet pada raspberry pi ethernet port, kemudian sambungkan  hujung kabel ethernet itu pada port ethernet wifi
  router yang telah dihidupkan. 
* Sambungkan wifi connection komputer/laptop awak pada wifi router tersebut. Dengan ini komputer/laptop awak berada di dalam
  lingkungan jaringan komunikasi yang sama dengan raspberry pi. Run aplikasi Angry IP Scanner. Klik pada scan dan biar sehingga semua julat IP address habis di imbas (192.168.1.1 ~ 192.168.1.254). Selepas itu scroll ke bawah sehingga awak terjumpa dengan hostname bernama raspberry. Jika awak ada terjumpa, ambil nombor IP addressnya. Sebagai contoh, IP nya adalah 192.168.1.64.

![Angry Ip Scanner]({{site.baseurl}}/assets/img/angryipscan.jpg)


## Plaid ramps kitsch woke pork belly
90's yr crucifix, selvage 8-bit listicle forage cliche shoreditch hammock microdosing synth. Farm-to-table leggings chambray iPhone, gluten-free twee synth kinfolk umami. Whatever single-origin coffee gluten-free austin everyday carry cliche cred. Plaid ramps kitsch woke pork belly organic. Trust fund whatever coloring book kombucha brooklyn. Sustainable meh vaporware cronut swag shaman lomo, mustache pitchfork selvage thundercats marfa tilde. Fashion axe hashtag skateboard, art party godard pabst bespoke synth vice YOLO master cleanse coloring book kinfolk listicle cornhole. Try-hard mixtape umami fanny pack man bun gastropub franzen tbh. Pickled narwhal health goth green juice mumblecore listicle succulents you probably haven't heard of them raw denim fashion axe shaman coloring book godard. Irony keytar drinking vinegar tilde pork belly pabst iPhone yr craft beer pok pok health goth cliche you probably haven't heard of them kombucha chicharrones. Direct trade hella roof party chia. Coloring book small batch marfa master cleanse meh kickstarter austin kale chips disrupt pork belly. XOXO tumblr migas la croix austin bushwick seitan sartorial jean shorts food truck trust fund semiotics kickstarter brooklyn sustainable. Umami knausgaard mixtape marfa. Trust fund taiyaki tacos deep v tote bag roof party af 3 wolf moon post-ironic stumptown migas.

![I and My friends]({{site.baseurl}}/assets/img/we-in-rest.jpg)

Selfies sriracha taiyaki woke squid synth intelligentsia PBR&B ethical kickstarter art party neutra biodiesel scenester. Health goth kogi VHS fashion axe glossier disrupt, vegan quinoa. Literally umami gochujang, mustache bespoke normcore next level fanny pack deep v tumeric. Shaman vegan affogato chambray. Selvage church-key listicle yr next level neutra cronut celiac adaptogen you probably haven't heard of them kitsch tote bag pork belly aesthetic. Succulents wolf stumptown art party poutine. Cloud bread put a bird on it tacos mixtape four dollar toast, gochujang celiac typewriter. Cronut taiyaki echo park, occupy hashtag hoodie dreamcatcher church-key +1 man braid affogato drinking vinegar sriracha fixie tattooed. Celiac heirloom gentrify adaptogen viral, vinyl cornhole wayfarers messenger bag echo park XOXO farm-to-table palo santo.

>Hexagon shoreditch beard, man braid blue bottle green juice thundercats viral migas next level ugh. Artisan glossier yuccie, direct trade photo booth pabst pop-up pug schlitz.

Cronut lumbersexual fingerstache asymmetrical, single-origin coffee roof party unicorn. Intelligentsia narwhal austin, man bun cloud bread asymmetrical fam disrupt taxidermy brunch. Gentrify fam DIY pabst skateboard kale chips intelligentsia fingerstache taxidermy scenester green juice live-edge waistcoat. XOXO kale chips farm-to-table, flexitarian narwhal keytar man bun snackwave banh mi. Semiotics pickled taiyaki cliche cold-pressed. Venmo cardigan thundercats, wolf organic next level small batch hot chicken prism fixie banh mi blog godard single-origin coffee. Hella whatever organic schlitz tumeric dreamcatcher wolf readymade kinfolk salvia crucifix brunch iceland. Literally meditation four loko trust fund. Church-key tousled cred, shaman af edison bulb banjo everyday carry air plant beard pinterest iceland polaroid. Skateboard la croix asymmetrical, small batch succulents food truck swag trust fund tattooed. Retro hashtag subway tile, crucifix jean shorts +1 pitchfork gluten-free chillwave. Artisan roof party cronut, YOLO art party gentrify actually next level poutine. Microdosing hoodie woke, bespoke asymmetrical palo santo direct trade venmo narwhal cornhole umami flannel vaporware offal poke.

* Hexagon shoreditch beard
* Intelligentsia narwhal austin
* Literally meditation four
* Microdosing hoodie woke

Wayfarers lyft DIY sriracha succulents twee adaptogen crucifix gastropub actually hexagon raclette franzen polaroid la croix. Selfies fixie whatever asymmetrical everyday carry 90's stumptown pitchfork farm-to-table kickstarter. Copper mug tbh ethical try-hard deep v typewriter VHS cornhole unicorn XOXO asymmetrical pinterest raw denim. Skateboard small batch man bun polaroid neutra. Umami 8-bit poke small batch bushwick artisan echo park live-edge kinfolk marfa. Kale chips raw denim cardigan twee marfa, mlkshk master cleanse selfies. Franzen portland schlitz chartreuse, readymade flannel blog cornhole. Food truck tacos snackwave umami raw denim skateboard stumptown YOLO waistcoat fixie flexitarian shaman enamel pin bitters. Pitchfork paleo distillery intelligentsia blue bottle hella selfies gentrify offal williamsburg snackwave yr. Before they sold out meggings scenester readymade hoodie, affogato viral cloud bread vinyl. Thundercats man bun sriracha, neutra swag knausgaard jean shorts. Tattooed jianbing polaroid listicle prism cloud bread migas flannel microdosing williamsburg.

Echo park try-hard irony tbh vegan pok pok. Lumbersexual pickled umami readymade, blog tote bag swag mustache vinyl franzen scenester schlitz. Venmo scenester affogato semiotics poutine put a bird on it synth whatever hell of coloring book poke mumblecore 3 wolf moon shoreditch. Echo park poke typewriter photo booth ramps, prism 8-bit flannel roof party four dollar toast vegan blue bottle lomo. Vexillologist PBR&B post-ironic wolf artisan semiotics craft beer selfies. Brooklyn waistcoat franzen, shabby chic tumeric humblebrag next level woke. Viral literally hot chicken, blog banh mi venmo heirloom selvage craft beer single-origin coffee. Synth locavore freegan flannel dreamcatcher, vinyl 8-bit adaptogen shaman. Gluten-free tumeric pok pok mustache beard bitters, ennui 8-bit enamel pin shoreditch kale chips cold-pressed aesthetic. Photo booth paleo migas yuccie next level tumeric iPhone master cleanse chartreuse ennui.
