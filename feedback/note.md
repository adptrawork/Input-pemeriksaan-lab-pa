**Relate**
https://support.morbis.id/issues/35977 | Labor PA, Sesuaikan ukuran file cetak laporan pemeriksaan PAhttps://support.morbis.id/issues/36219 | [LAB PA] Kolom saran dan ICD-0

**Feedback**

Berdasarkan feedback dari user (DokterLab PA), perlu merombak alur pengisian dan layout cetak hasil Patologi Anatomi. User mengeluhkan hasil cetak saat ini terlalu panjang dan terpisah-pisah per item.

🔗 **Link Prototype:** https://adptrawork.github.io/Input-pemeriksaan-lab-pa/

(Source code HTML terlampir pada tiket ini untuk acuan styling Tailwind dan struktur DataTables).

Berikut adalah detail business logic yang harus diimplementasikan:

**1. Perubahan Logika View / Output Cetak**

**Hapus Nama Tindakan dari Cetakan:** Variabel seperti "Jaringan kecil < 5 cm" hanya digunakan untuk insert ke database (kebutuhan billing / rekam jejak). **JANGAN** di-render ke halaman cetak.**Sistem Single Section:** Jangan melakukan looping section (Makroskopik, Mikroskopik, Kesimpulan) untuk setiap sampel. Buat hanya satu section Makroskopik, satu Mikroskopik, dan satu Kesimpulan di template cetak.**Penomoran Romawi:** Gunakan variabel "Lokasi Jaringan" (Kanan, Kiri, dll.) yang diurutkan dengan angka Romawi (I, II, III) di dalam section tunggal tersebut.Tempatkan inputan ICD-0 user di akhir setelah bacaan kesimpulan, namun juga user tidak mengisi maka tidak perlu di tampilkan apa apa setelah bacaan kesimpulan.Tambahkan section dari inputan saranPada form input jangan dibuat auto Sentence/Capitalized , biarkan saja seperti * inputan biasa* terutama di form input RS Luar karena agar user bisa menginputkan bacaan seperti RSUD Daud  (Campuran Besar dan kecil) dan bukan nya menjadi Rsud Daud  (Hanya huruf pertama yang besar), atau jika bisa di matikan saja di semua form input yang ada auto Sentence/Capitalized nya
**2. Implementasi Fitur "Samakan Dengan" (Penggabungan Hasil)**

**Frontend (Form Input):** Terapkan dropdown "Samakan Dengan" pada setiap row sediaan (kecuali sediaan pertama). Gunakan fungsi JavaScript handleLinkTarget() dari prototype. Jika user memilih untuk menyamakan sediaan, sembunyikan form input Mikroskopik & Kesimpulan, dan munculkan alert box biru ("Hasil Mikroskopis dan Kesimpulan akan disamakan...").**Backend (Sistem Cetak):** Buat logika kondisional di controller/backend saat generate cetakan. Jika sediaan II di-link ke sediaan I di database, maka hasil cetaknya harus cerdas menggabungkan nomor romawinya menjadi format: **"I & II. [Teks hasil yang sama]"**. (Lihat contoh output di deskripsi tiket).Penambahan form input seperti ICD-0 dan juga Saran
---
