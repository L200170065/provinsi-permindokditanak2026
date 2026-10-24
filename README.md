# provinsi-permindokditanak2026

Paket static wrapper untuk deployment Vercel. UI aplikasi dan backend tetap dijalankan oleh Google Apps Script pada URL:

https://script.google.com/macros/s/AKfycby4sXvTRzx67dAJdBCL7PLVRaacjGKcyFKO2X-DIp63jI-6LZQMh7acbVyIniIdUucZlA/exec

## Deploy ke Vercel
1. Buat repository GitHub baru bernama `provinsi-permindokditanak2026`.
2. Upload seluruh isi folder ini (bukan folder pembungkusnya) ke root repository.
3. Di Vercel, pilih **Add New → Project**, import repository tersebut, dan deploy dengan Framework Preset **Other**. Tidak perlu Build Command atau Output Directory khusus.
4. Domain target: `https://provinsi-permindokditanak2026.vercel.app` (baru aktif setelah project berhasil dibuat dan domain tersedia).

## Penting: izinkan aplikasi Google Apps Script ditampilkan dalam iframe
Jika Google Apps Script menolak ditampilkan dalam iframe, ubah fungsi `doGet(e)` di `Code.gs` agar hasil `evaluate()` menyertakan:

```javascript
.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
```

Contoh:
```javascript
function doGet(e) {
  const t = HtmlService.createTemplateFromFile('Index');
  t.view = 'user';
  return t.evaluate()
    .setTitle('Permintaan Data Daerah | Rehabilitasi Sosial Anak')
    .addMetaTag('viewport', 'width=device-width, initial-scale=1')
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
}
```
Simpan lalu buat deployment versi baru pada Apps Script. Perhatikan bahwa `ALLOWALL` mengizinkan situs lain membingkai aplikasi; gunakan hanya jika memang diperlukan dan sesuai kebijakan instansi.

## Catatan
- Vercel hanya menyajikan pembungkus/URL tersendiri; pengisian, `google.script.run`, validasi, dan penyimpanan tetap berlangsung di Google Apps Script.
- File `Code.gs` dan `Index.html` disertakan sebagai salinan sumber untuk referensi dan pemeliharaan Apps Script; Vercel tidak mengeksekusi file tersebut.
- Uji tampilan iframe, lanjutkan wizard, kirim respons uji yang disepakati, lalu pastikan respons masuk ke spreadsheet sebelum menyebarkan URL.
