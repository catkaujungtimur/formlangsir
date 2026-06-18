# formlangsir
Form Langsir Briefing
# Form Perintah Langsir (versi web)

Web app pengganti Google Sheets "Form Perintah Langsir". Murni HTML/CSS/JS, tanpa server, tanpa dependensi — bisa langsung dibuka di browser atau dihosting gratis lewat GitHub Pages.

## Cara pakai

### Buka langsung
Download `index.html`, lalu klik dua kali untuk membuka di browser.

### Hosting via GitHub Pages
1. Buat repo baru di GitHub, upload `index.html`.
2. Masuk ke **Settings → Pages**, pilih branch `main` dan folder `/ (root)`.
3. Tunggu beberapa menit, sites akan aktif di `https://<username>.github.io/<nama-repo>/`.

## Fitur

- **Nomor surat otomatis** — format `NOMOR: 13/KTG/VI/2026`, nomor urut dan kode emplasemen bisa diubah di kolom input.
- **Hari/Tanggal otomatis** — mengambil tanggal hari ini, format `KAMIS/18-06-2026`.
- **Kolom Keterangan sebagai sumber utama** — sesuai cara kerja aslinya, ketik atau tempel (paste, misalnya dari simulator langsir) baris-baris gerakan di kotak Keterangan tiap rangkaian, format per baris: `LABEL: teks` (misal `C1: AMBIL 9 KRT EX 279`) atau cukup `LABEL` saja kalau loko cuma lewat tanpa ambil/lepas. Klik **Generate dari Keterangan** untuk mengisi otomatis kolom Posisi Awal, Posisi Akhir, LOKO, dan lookup Urutan Pergerakan di seluruh baris tabel rangkaian itu.
- **Posisi awal otomatis berantai antar rangkaian** — saat klik Generate, posisi awal rangkaian berikutnya otomatis terisi dari posisi akhir terakhir rangkaian sebelumnya (kecuali rangkaian pertama dalam form, yang diisi manual, biasanya `DL`).
- **Hitung jumlah kereta otomatis (LOKO + n KERETA)** — dihitung kumulatif dari teks `AMBIL n KRT`, `LEPAS n KRT`, atau `LEPAS SEMUA` di tiap baris Keterangan.
- **Judul rangkaian otomatis** — contoh `C1-J.III (2)`, dibentuk dari posisi-posisi yang punya keterangan terisi saja (posisi transit tanpa ambil/lepas dilewati), dengan angka jumlah dihitung otomatis — tidak akan salah hitung manual lagi.
- **Lookup urutan pergerakan & wesel otomatis** dari tabel RUTE berdasarkan kombinasi Posisi Awal-Akhir hasil parsing.
- **Override manual tetap memungkinkan** — kolom Posisi Awal/Akhir di tabel tetap bisa diedit langsung untuk kasus khusus (misalnya tukar lokomotif di Dipo Loko tanpa berpindah jalur). Override ini akan tertimpa lagi kalau tombol Generate dipencet ulang, karena kotak Keterangan tetap jadi acuan final.
- **Catatan kaki (NB) bisa diedit** — teks "KEC LANGSIR MAX..." dan keterangan singkatan W/DL/D1/dst bisa diubah langsung di form, karena terkadang berbeda isi/singkatannya per form.
- **Tanda tangan dengan auto-isi NIPP** — pilih nama dari dropdown, NIPP otomatis muncul.
- **Tambah/hapus rangkaian** secara dinamis.
- **Cetak / Simpan PDF** — tombol cetak menghasilkan tampilan rapi tanpa elemen tombol/edit, kotak Keterangan dicetak sebagai teks biasa.
- **Tersimpan otomatis di browser** (localStorage) — kalau browser ditutup dan dibuka lagi, isi form sebelumnya masih ada.

## Cara isi form (alur kerja harian)

1. Klik **+ Tambah Rangkaian**, beri nama rangkaian (misal `EX KA279`).
2. Isi **Posisi awal pertama** kalau ini rangkaian pertama dalam form (biasanya `DL`). Untuk rangkaian kedua dan seterusnya biasanya sudah otomatis terisi dari rangkaian sebelumnya.
3. Ketik manual atau tempel (paste) dari simulator ke kotak **Keterangan**, satu baris per gerakan.
4. Klik **Generate dari Keterangan**.
5. Cek hasilnya di tabel atas — kalau ada kombinasi posisi yang belum dikenal, akan muncul catatan "kombinasi posisi belum ada di tabel RUTE" supaya kamu tahu perlu menambah baris baru di data RUTE.
6. Ulangi untuk rangkaian berikutnya.
7. Isi jam mulai/selesai, pilih nama petugas di bagian tanda tangan, lalu Cetak/Simpan PDF.

## Mengedit data (RUTE dan TTD)

Semua data referensi disimpan langsung di dalam file `index.html`, di bagian yang ditandai komentar:

```js
/* =========================================================
   DATA — silakan diedit sesuai kebutuhan stasiun/emplasemen
   ========================================================= */
```

- **`RUTE`** — array berisi `[Posisi Awal, Posisi Akhir, Urutan Gerakan, Wesel]`. Tambahkan baris baru kalau ada kombinasi posisi jalur baru.
- **`TTD`** — objek `{ "NAMA": "NIPP" }` untuk daftar petugas yang muncul di dropdown tanda tangan.

Edit langsung di teks editor apa saja (Notepad, VS Code, dll), simpan, lalu refresh browser.

## Catatan

- Tidak memerlukan koneksi internet setelah file di-download (kecuali saat diakses lewat GitHub Pages pertama kali).
- Data tersimpan hanya di browser/perangkat yang dipakai (localStorage), tidak otomatis sinkron antar perangkat. Kalau perlu multi-user / multi-perangkat dengan data terpusat, perlu backend tambahan (database) — bisa didiskusikan lebih lanjut.
