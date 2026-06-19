# Form Perintah Langsir (versi web)

Web app pengganti Google Sheets "Form Perintah Langsir". Murni HTML/CSS/JS, tanpa server, tanpa dependensi — bisa langsung dibuka di browser atau dihosting gratis lewat GitHub Pages.

## Cara pakai

### Buka langsung
Download `index.html`, lalu klik dua kali untuk membuka di browser.

### Hosting via GitHub Pages
1. Buat repo baru di GitHub, upload `index.html`.
2. Masuk ke **Settings → Pages**, pilih branch `main` dan folder `/ (root)`.
3. Tunggu beberapa menit, situs akan aktif di `https://<username>.github.io/<nama-repo>/`.

## Fitur

- **3 tab shift**: Dinas Malam, Dinas Siang, Dinas Pagi — masing-masing punya data form, rangkaian, dan tanda tangan terpisah, karena rangkaian kereta biasanya sama tiap shift dan hanya pergerakan langsirnya yang beda.
- **Export / Import JSON per shift** — simpan isi satu shift ke file `.json` untuk dibagikan atau dibuka lagi nanti, tanpa mempengaruhi shift lain.
- **Nomor surat & Hari/Tanggal otomatis** — format sama seperti rumus aslinya (`NOMOR: 13/KTG/VI/2026`, `KAMIS/18-06-2026`).
- **Edit Keterangan via popup yang bisa digeser** — klik tombol "Edit Keterangan" di tiap rangkaian untuk membuka kotak tempel/ketik massal (mis. hasil copy dari simulator). Tabel utama tetap tampil rapi seperti spreadsheet asli, tidak tercampur kotak input besar.
- **Kolom Keterangan, Posisi Awal, dan Posisi Akhir bisa diedit langsung di tabel** — perubahan ini otomatis tersinkron dengan isi popup (dua arah): edit di tabel akan terbawa kalau popup dibuka lagi, dan generate ulang dari popup akan menimpa tabel. Perubahan terakhir yang dipakai.
- **Sisip / hapus baris manual** — klik ikon titik tiga di ujung kanan tiap baris untuk menyisipkan baris baru di atas, di bawah, atau menghapus baris itu. Berguna untuk kasus kombinasi posisi yang belum ada di tabel RUTE (lewat jalur perantara secara manual).
- **Hitung jumlah kereta otomatis (LOKO + n KERETA)** — dihitung kumulatif dari `AMBIL n KRT`, `LEPAS n KRT`, atau `LEPAS SEMUA`.
- **Judul rangkaian otomatis** — contoh `C1-J.III (2)`, dibentuk dari posisi yang punya keterangan ambil/lepas saja, jumlahnya dihitung otomatis (tidak bisa salah hitung manual lagi).
- **Lookup urutan pergerakan & wesel otomatis** dari tabel RUTE. Kalau kombinasi posisi belum ada di tabel, akan muncul catatan jelas supaya kamu tahu perlu menambah data atau menyisip jalur perantara manual.
- **Posisi awal berantai otomatis antar rangkaian** — posisi awal rangkaian baru otomatis terisi dari posisi akhir terakhir rangkaian sebelumnya.
- **Catatan kaki (NB) bisa diedit** langsung di form.
- **Label "Yang Menerima Perintah" dan "Yang Memerintah"** di atas kolom tanda tangan, sesuai tata letak form asli.
- **Tanda tangan dengan auto-isi NIPP** dari dropdown nama.
- **Cetak / Simpan PDF** — tampilan cetak bersih tanpa tombol/menu, mengikuti shift yang sedang aktif.
- **Tersimpan otomatis di browser** (localStorage) untuk seluruh shift.

## Cara isi form (alur kerja harian)

1. Pilih tab shift yang sesuai (Dinas Malam/Siang/Pagi).
2. Klik **+ Tambah Rangkaian**, beri nama (misal `EX KA279`).
3. Klik **Edit Keterangan** di rangkaian itu, isi posisi awal pertama (manual, biasanya `DL` untuk rangkaian pertama dalam form — rangkaian berikutnya otomatis terisi), lalu ketik atau tempel baris-baris gerakan, format `LABEL: teks` per baris.
4. Klik **Terapkan ke Tabel**.
5. Kalau ada catatan "kombinasi posisi belum ada di tabel RUTE", gunakan menu titik-tiga di baris itu untuk **sisip baris** lewat jalur perantara yang sesuai kondisi lapangan, isi manual Posisi Akhir dan Keterangannya.
6. Ulangi untuk rangkaian berikutnya.
7. Isi jam mulai/selesai, pilih nama petugas tanda tangan, lalu Cetak/Simpan PDF.
8. Kalau perlu disimpan sebagai arsip atau dipindah ke perangkat lain, gunakan **Export JSON** lalu nanti **Import JSON** di shift yang sama.

## Mengedit data referensi (RUTE dan TTD)

Semua data ada di bagian awal script `index.html`, ditandai komentar:

```js
/* =========================================================
   DATA — silakan diedit sesuai kebutuhan stasiun/emplasemen
   ========================================================= */
```

- **`RUTE`** — array `[Posisi Awal, Posisi Akhir, Urutan Gerakan, Wesel]`. Tambahkan baris baru kalau ada kombinasi posisi jalur baru yang sering dipakai, supaya tidak perlu sisip manual berulang-ulang.
- **`TTD`** — objek `{ "NAMA": "NIPP" }` untuk daftar petugas di dropdown tanda tangan.

Edit langsung di teks editor (Notepad, VS Code, dll), simpan, refresh browser.

## Catatan

- Data tersimpan di localStorage hanya berlaku per browser/perangkat, tidak otomatis sinkron antar perangkat. Pakai fitur Export/Import JSON untuk memindahkan data antar perangkat atau membuat arsip harian.
- Kalau butuh data multi-pengguna yang sinkron otomatis di banyak perangkat secara realtime, perlu backend/database tambahan — bisa didiskusikan lebih lanjut kalau diperlukan.
