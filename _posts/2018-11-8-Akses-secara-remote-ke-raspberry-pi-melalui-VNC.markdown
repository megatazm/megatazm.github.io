---
layout: post
title: Akses Secara Remote Desktop ke Raspberry Pi Melalui VNC 
date: 2018-11-8 13:32:20 +0300
description:  # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to]
---


VNC adalah Virtual Network Computing yang membolehkan awak mengongsikan interface grafik komputer (Server) kepada komputer lain (Client) secara remote. Awak perlu memasang aplikasi VNC server pada rasbperry pi dan aplikasi VNC client pada laptop awak. Melalui aplikasi VNC server ini, interface grafik OS Raspbian boleh diakses melalui laptop awak. Cuma tindakbalasnya mungkin sedikit lag jika ramai orang menggunakan sambungan 
wifi yang sama. Untuk mengaktifkan VNC servis pada raspberry pi, masukkan command ini di terminal awak (jika awak pakai windows silalah pakai aplikasi MobaXterm)

```javascript
ssh pi@<ip_address_pi_awak>
password:raspberry

sudo raspi-config
```



<br/>
Daripada menu raspi-config seperti gambar di bawah, pilih dengan menggunakan keyboard simbol arah anak panah kemudian tekan ENTER: -

```javascript
1. Interfacing Options
2. P3 VNC
3. Yes
4. Finish
```

<br/>
![raspi-config1]({{site.baseurl}}/assets/img/raspi-config1.png){: .center-image }
<br/>
<br/>
![raspi-config2]({{site.baseurl}}/assets/img/raspi-config2.png){: .center-image }
<br/>
<br/>
![raspi-config2]({{site.baseurl}}/assets/img/raspi-config3.png){: .center-image }
<br/>
<br/>

Dengan ini servis VNC server telah diaktifkan. Seterusnya, awak perlu memuat-turun dan memasang perisian VNC Viewer pada laptop. Awak boleh cuba VNC veiwer seperti [RealVNC](https://www.realvnc.com/en/), [TightVNC](https://www.tightvnc.com/) atau [VNC viewer for Chrome](https://vnc-viewer-for-google-chrome.en.softonic.com/). Untuk komputer saya, saya download dan install RealVNC for MacOS. Setelah awak berjaya memuat-turun aplikasi VNC viewer, run aplikasi tersebut. RealVNC viewer interface akan dipaparkan seperti gambar di bawah.

<br/>
![VNC-Viewer]({{site.baseurl}}/assets/img/VNC-Viewer.png){: .center-image }
<br/>

```javascript
1. Click: 
        File > New Connection
2. Masukkan Raspi Ip Address:
        VNC Server: IP_Address_Pi_Awak
3. Click:
         Ok
```
<br/>
Kemudian, klik sebanyak dua kali pada jalur berwarna biru yang mengandungi IP address yang telah awak daftarkan seperti gambar di bawah.
<br/>
<br/>
![VNC-Server-IP]({{site.baseurl}}/assets/img/VNC-Srv IP-2.png){: .center-image }
<br/>
<br/>
<br/>
Dialog box identity check akan dipaparkan seperti di bawah. Tanpa ragu-ragu teruskan klik continue. 
<br/>
<br/>
{:refdef: style="text-align: center;"}
![VNC-continue]({{site.baseurl}}/assets/img/VNC-continue2.png)
{: refdef}

Kemudian login masuk ke raspi awak:
<br/>
<br/>
{:refdef: style="text-align: center;"}
![VNC-Login]({{site.baseurl}}/assets/img/VNC-Login2.png){: .center-image}
{: refdef}
<br/>
```javascript
1. Masukkan Username: pi
2. Masukkan Password: raspberry        
3. Click: OK
```
<br/>
Sejurus sahaja awak klik OK, interface grafik Raspbian OS Desktop akan terpapar di depan mata seperti gambar di bawah. Untuk membebaskan raspi awak daripada network cable yang disambungkan pada wifi router, klik pada simbol yang ditunjukkan oleh anak panah berdarah seperti gambar di bawah. Kemudian pilih nama SSD router wifi yang telah awak sediakan. Jika awak cabut wayar network tersebut, sambungan VNC awak akan terputus. Awak perlu mengulangi langkah yang sebelum ini, menggunakan angryip scanner untuk memperolehi IP address yang baru, [Camaner yek]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop %}). Selepas IP address baharu telah diperolehi, awak perlu mengulangi semula langkah di atas, menggunakan VNC Viewer untuk mengakses masuk ke dalam raspi melalui sambungan wifi. 

Ya, raspi awak sudah bebas! ( ᐛ )و
<br/>
<br/>
{:refdef: style="text-align: center;"}
![Raspbian]({{site.baseurl}}/assets/img/raspbian2.png){: .center-image}
{: refdef}











