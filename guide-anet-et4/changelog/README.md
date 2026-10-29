---
description: Cara penggunaan Anet ET4
icon: clock-rotate-left
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: false
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: false
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# TUTORIAL



### Reference

[How To Print](https://youtu.be/wzhjyUGtKXM?si=RrMIhHAZ99-bLbN7)

[Z offsets leveling](https://youtu.be/jf5_EanYB4k?si=_8PVmZ8vLZbr2wMW)

[Manual Setup](https://manuals.plus/m/9f15afd03037f2de022fd572eddcdae79a60d93fd4a0604d55cc1987afe54166_optim.pdf)&#x20;

[Manual Assembly](https://3dprint.wiki/images/reprap/anet/et4/1.setup_manual.pdf)

{% embed url="https://www.orcaslicer.com/wiki/#printer-settings" %}

### Resources

{% embed url="https://www.orcaslicer.com/" %}





{% hint style="danger" %}
Peringatan jangan mengubah, mengganti, merusak seluruh komponen pada mesin; Jika ingin memperbaiki mohon untuk **mempelajari manual mesin** terlebih dahulu.
{% endhint %}

{% hint style="warning" %}
Himbauan

1. Hindari penggunaan suhu >215°C
2. &#x20;Gunakan filament PLA, PLA+
3. Pastikan Nozzle dan Bed panas terlebih dahulu
4. Apabila ada getaran mohon untuk kencangkan baut kembali
5. Jangan menyentuh **Tip Nozzle**
6. &#x20;Bersihkan kembali Plate Kaca Bed  menggunakan air mengalir
7. Tipe Anet ET4 ataupun Anet ET4 XR hampir sama
8. Apabila Terjadi Malfungsi pada stepper lakukan [.](./ "mention")
{% endhint %}



## Z Offset calibration

{% hint style="info" %}
Pasang Sensor Auto leveling terlebih dahulu lihat pada [video ini](https://www.youtube.com/watch?v=jf5_EanYB4k)
{% endhint %}

1. Tekan <img src=".gitbook/assets/3.png" alt="" data-size="line"> (Setting) Setelah itu tekan <img src=".gitbook/assets/Copy of Add a heading.png" alt="" data-size="line"> untuk mengebalikan extruder pada posisi awal
2. Kembali ke menu awal dan pilih <img src=".gitbook/assets/2 (1).png" alt="" data-size="line"> (prepare) dan pilih <img src=".gitbook/assets/3 (1).png" alt="" data-size="line"> dan pilih <img src=".gitbook/assets/4.png" alt="" data-size="line">
3. Tunggu sampai auto leveling selesai
4. Setelah Selesai, autor offset dengan menekan tombol **+** atau **- (rekomendasi nilai 0.20)** cek dengan kertas; pastikan tidak tersobek/terhimpit saat digerakan digerakan dan pastikan nozzle hampir dekat dengan bed plate
5. Jika sudah tekan <img src=".gitbook/assets/4 (1).png" alt="" data-size="line"> (OK) untuk memastikan leveling tersimpan.



## Heat Preparation

{% hint style="info" %}
Pastikan sensor auto leveling tidak terpasang
{% endhint %}

1. PIlih <img src=".gitbook/assets/2 (1).png" alt="" data-size="line"> (Prepare), kemudian pilih <img src=".gitbook/assets/1.png" alt="" data-size="line">, atur suhu nozzle <img src=".gitbook/assets/11.png" alt="" data-size="line"> pada suhu 200C dan bed plate <img src=".gitbook/assets/12.png" alt="" data-size="line"> pada suhu 50C dengan menekan <img src=".gitbook/assets/11.png" alt="" data-size="line"> dan klik tanda **+ atau -** begitu pula untuk bed plate  <img src=".gitbook/assets/12.png" alt="" data-size="line">&#x20;
2. Kemudian tekan <img src=".gitbook/assets/10.png" alt="" data-size="line"> untuk memulai pemanasan pada nozzle dan bed plate
3. Tunggu sampai suhu tercapai
4. Lanjut pada pembersihan residu nozzle



## Nozzle Cleaning

1. Masukan filament pada extuder.
2. Pilih  <img src=".gitbook/assets/2 (1).png" alt="" data-size="line"> (Prepare), kemudian pilih <img src=".gitbook/assets/2 (2).png" alt="" data-size="line"> dan pilih 30 cm dengan kecepatan 8mm/s
3. Klik \<Load> dan tunggu sampai filament keluar dari nozzle
4. Setelah itu tekan <img src=".gitbook/assets/9.png" alt="" data-size="line"> Jika dirasa sudah cukup untuk membersihkan residu dari filament sebelumnnya
5. Lanjut proses print



## Printing Process

{% hint style="info" %}
Gunakan Preset sesuai Kebutuhan, masukan _memory card_ pada port di mesin&#x20;
{% endhint %}

{% hint style="info" %}
Coarse -> untuk proses cepat, kualitas mid-low

Smooth -> untuk proses standar, kulitas mid

Fine -> untuk proses lambat, kualitas High
{% endhint %}

1. buka `<orcaslicer>`, klik `<new project>`
2. Klik `<File>` kemudian Klik `<Export>` pilih `<import configs..>`
3. Kemduian pilih file yang tersedia pada resources halaman ini.
4. Tekan \<CTRL+I> atau klik `<add>`
5. Pilih File `.stl` atau `.step` yang sudah diekspor sebelumnya
6. setelah itu tekan `<slice plate>`
7. Klik `<Export G-Code file>`  dan masukan pada memory card.



1. Setalh memory card diisi program G-code, masukan memory card pada port memory card di mesin
2. Pilih <img src=".gitbook/assets/1 (1).png" alt="" data-size="line"> (print) kemudian klik file g-code yang sudah dibuat tadi
3. dan klik <img src=".gitbook/assets/4 (1).png" alt="" data-size="line"> (ok) untuk memulai prosess printing dan pastikan first layer sudah diprint sebelum meninggalkan mesin.&#x20;
