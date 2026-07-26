# Panduan Mengelola Website ASJ Kelas XI

## Struktur File
- `index.html` → Halaman utama (Roadmap). Setiap kartu Bab sudah menjadi hyperlink.
- `bab1.html` → Contoh materi + kuis yang sudah lengkap (Bab 1). Gunakan file ini sebagai **template** untuk membuat bab lain.
- `belum-tersedia.html` → Halaman otomatis yang muncul jika sebuah bab belum punya materi. Bab 2–18 saat ini semuanya mengarah ke halaman ini.

## Cara Menambahkan Materi Bab Baru (Contoh: Bab 2)
1. Duplikat file `bab1.html`, ganti nama menjadi `bab2.html`.
2. Buka `bab2.html`, ubah:
   - Judul di tag `<title>`
   - Judul & isi materi di bagian `<header>` dan `<main>`
   - Pertanyaan kuis beserta `data-correct` (kunci jawaban) pada setiap `data-question`
   - Link "Bab Berikutnya" di bagian bawah
3. Simpan file `bab2.html` di folder yang sama dengan `index.html`.
4. Buka `index.html`, cari kartu **Bab 2**, lalu ubah:
   ```html
   <a href="belum-tersedia.html?bab=Bab%202&judul=Hardware%20dan%20OS%20Server" ...>
   ```
   menjadi:
   ```html
   <a href="bab2.html" ...>
   ```
5. Upload/unggah semua file (index.html, bab1.html, bab2.html, belum-tersedia.html, dst) ke satu folder hosting yang sama (misalnya Google Sites embed, GitHub Pages, Netlify, atau hosting sekolah).

## Cara Kerja Kuis & Nilai
- Kuis pilihan ganda dinilai otomatis oleh JavaScript di browser (bukan server), lalu nilai ditampilkan langsung di layar siswa.
- Karena website ini statis (tanpa database), **cara mengambil nilai** ada 2 opsi:
  1. **Manual** — Guru meminta siswa screenshot kartu hasil nilai, lalu mengirimkannya lewat WhatsApp/Google Classroom.
  2. **Salin Otomatis** — Setelah submit, siswa bisa klik tombol "Salin Hasil untuk Dikirim ke Guru" yang akan menyalin teks nilai ke clipboard, lalu tempel (paste) ke chat/formulir.
- Soal nomor terakhir (esai/reflektif) sengaja tidak dinilai otomatis, karena perlu penilaian manual oleh Guru.

> Jika ke depannya Bapak Khalid ingin nilai otomatis masuk ke Google Sheet/Form, itu bisa ditambahkan dengan menghubungkan tombol submit ke Google Apps Script atau Google Form — beri tahu saya jika ingin dibuatkan.

## Format Penulisan Materi Kuis Baru
Setiap soal pilihan ganda menggunakan struktur berikut (boleh dicopy-paste dari `bab1.html`):
```html
<div class="bg-dark border border-gray-800 rounded-xl p-6">
    <p class="font-semibold text-white mb-4">Teks pertanyaan...</p>
    <div class="space-y-2" data-question="1" data-correct="b">
        <label class="quiz-option flex items-center gap-3 p-3 rounded-lg border border-gray-700 cursor-pointer">
            <input type="radio" name="q1" value="a" class="accent-primary"> <span>Pilihan A</span>
        </label>
        <!-- dst untuk pilihan b, c, d -->
    </div>
</div>
```
`data-correct` diisi huruf kunci jawaban yang benar (a/b/c/d), dan `name="q1"` harus unik per nomor soal.
