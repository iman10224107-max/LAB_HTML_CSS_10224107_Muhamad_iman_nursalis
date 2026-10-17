# Jawaban Praktikum: Muhamad Iman Nursalis (10224107)

## Bagian 1: Pemanasan
1. `nav a.active:hover { color: red; }`
   - Selector: `nav a.active:hover`
   - Deklarasi: `color: red;`
   - Property: `color`
   - Value: `red`
   - Pseudo-class: `:hover`
2. Block: p, li, h2 — Inline: span, a, strong
3. Yang jadi hijau: A dan B. C tidak hijau karena `.box p` butuh elemen `p` yang menjadi descendant dari elemen ber-class `box`, bukan elemen itu sendiri yang punya class `box`. D tidak hijau karena di luar `.box`.
4. Warnanya merah, karena `#title` (ID selector) punya specificity paling tinggi dibanding `.heading` (class) dan `h1` (type), terlepas dari urutan aturan di stylesheet.
5. Tag `<strong>` dibuka di dalam `<p>` tapi ditutup setelah `</p>`. Tag harus ditutup dalam urutan kebalikan saat dibuka, seharusnya `<p>Hello <strong>world</strong></p>`.

## Bagian 3: Prediksi Selector Golf
P1.
(a) "Weekly hack nights." → hijau, karena ada di dalam `<section>` sehingga `section p` (lebih spesifik dari `p`) berlaku.
(b) "Bring your own laptop." → oranye, karena class selector `.note` (specificity 0,1,0,0) mengalahkan `section p` (0,0,0,2).
(c) "© 2026 Student Affairs" → biru, karena hanya aturan `p` yang berlaku (di luar section, tanpa class note).

P2. Urutan specificity tertinggi → terendah:
#tech p > .club p > main section p > p

Setelah diuji (hasil sebenarnya):
Hasil di browser (pakai test.css sementara) sesuai prediksi di atas, mengikuti aturan cascade/specificity CSS standar. (a) hijau, (b) oranye, (c) biru.

## Bagian 4: Box model
Q1 (content-box): Lebar terlihat = width + padding kiri+kanan + border kiri+kanan
= 300 + (16+16) + (1+1) = 334px

Q2 (border-box): `width: 300px` sudah mencakup padding dan border, jadi lebar terlihat (border ke border) tetap 300px, tapi area content menyusut menjadi 300 - 32 - 2 = 266px.

Pengecekan DevTools: (isi dengan nilai asli dari Inspect → Computed → Box Model di browsermu sendiri — seharusnya mendekati: content ≈266px, padding 16px tiap sisi, border 1px tiap sisi, margin 24px tiap sisi)

## Bagian 5: Tabel debug
| # | Baris | Bug | Perbaikan | Cara menemukannya |
|---|-------|-----|-----------|-------------------|
| 1 | `colour: #333;` | Nama property salah (British spelling) | Ganti jadi `color: #333;` | Membaca kode / DevTools |
| 2 | `background: #dbe7f3` | Tidak ada titik koma penutup | Tambahkan `;` di akhir | Membaca kode |
| 3 | `.Card { ... }` | Selector salah huruf besar (HTML pakai `class="card"`) | Ganti jadi `.card` | DevTools: style tidak diterapkan |
| 4 | `#news-list { ... }` | ID selector tidak cocok dengan `id="newsList"` | Ganti jadi `#newsList` | DevTools |
| 5 | `font-size: 18 px;` | Spasi antara angka dan unit membuat value invalid | Ganti jadi `18px` | Validator / DevTools |
| 6 | `text-align: centre;` | Value salah (bukan keyword CSS valid) | Ganti jadi `center` | Validator |
| 7 | `<h1>Campus News</h2>` | Tag pembuka/penutup tidak cocok | Ganti jadi `</h1>` | Validator |
| 8 | `<a href="about.html>About</a>` | Tanda kutip penutup atribut hilang | Tambahkan `"` setelah `about.html` | Validator |
| 9 | `<img src="...">` | Atribut `alt` tidak ada | Tambahkan `alt="Campus news banner"` | Validator |

## Bagian 6: Tabel Code Review
| # | Baris | Masalah | Mengapa penting | Perbaikan saya |
|---|-------|---------|-----------------|----------------|
| 1 | 1 | Tidak ada `<!DOCTYPE html>` dan `lang` | Browser bisa quirks mode; screen reader salah baca bahasa | Tambahkan `<!DOCTYPE html>` dan `<html lang="en">` |
| 2 | 2-3 | Tidak ada meta charset & viewport | Risiko encoding salah, tidak responsif di mobile | Tambahkan kedua meta tag |
| 3 | 13-31 | Semua layout pakai `<div>` bukan tag semantik | Merusak aksesibilitas, SEO, keterbacaan kode | Ganti dengan header/nav/main/section/footer |
| 4 | 14,20,26 | Tidak ada heading asli, dibuat dengan `<b>`/div besar | Outline dokumen rusak, buruk untuk SEO & screen reader | Gunakan `<h1>`/`<h2>` |
| 5 | 20,26 | Inline `style=""` | Campur presentasi & struktur, tidak reusable | Pindahkan ke class CSS |
| 6 | 6 | `!important` pada `.nav a` | Merusak cascade, sulit di-override | Hapus `!important` |
| 7 | 5 | `width: 1200px` fixed | Tidak responsif | Ganti dengan `max-width` + `width: 100%` |
| 8 | 24 | `<img>` tanpa `alt` | Gagal validator & aksesibilitas | Tambahkan `alt` deskriptif |
| 9 | 27-29 | Input tanpa `<form>`/`<label>`, email pakai `type="text"` | Screen reader tidak tahu fungsi input | Bungkus `<form>`, tambah `<label>`, pakai `type="email"` |
| 10 | 8 | `.sidebar` didefinisikan tapi tidak dipakai | Kode mati, membingungkan | Hapus aturan `.sidebar` |

Refleksi:
1. Masalah yang paling sulit disadari hanya dari browser adalah yang tidak terlihat secara visual, seperti `alt` yang hilang, heading yang sebenarnya `<div>` berstyle besar, dan form tanpa label — karena tampak normal secara visual, bug ini hanya muncul lewat validator atau inspeksi struktur.
2. Halaman aslinya "berfungsi" secara visual, tapi tetap penting karena memengaruhi aksesibilitas (screen reader), SEO (search engine mengandalkan heading/semantik), dan maintenance (CSS dengan `!important` dan width fixed sulit diubah nanti).
3. Kebiasaan yang akan saya lakukan: selalu menjalankan halaman lewat W3C Validator dan mengecek heading outline sebelum submit, serta mencoba navigasi hanya dengan keyboard untuk memastikan form dan link bisa diakses.

## Bagian 7: Exit ticket
1. Aturan CSS terdiri dari selector (menunjuk elemen HTML yang di-style) dan blok deklarasi `{ }` berisi satu/lebih deklarasi; setiap deklarasi punya property dan value dipisahkan `:` dan diakhiri `;`.
2. Yang masih membingungkan: specificity saat beberapa selector bersaing, terutama kombinasi id, class, dan pseudo-class.
3. Hal yang sekarang bisa dilakukan tanpa mencari referensi: menulis selector dasar (type, class, id, descendant) dan mengenali bug CSS umum seperti property salah ketik atau value yang formatnya salah.
