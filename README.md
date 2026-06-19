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

### Struktur shift & form
- **3 tab shift**: Dinas Malam, Dinas Siang, Dinas Pagi — masing-masing independen.
- **Banyak Form Langsir dalam satu shift** — klik **+ Tambah Form Langsir** di paling bawah untuk membuat form baru (nomor surat, jam, rangkaian, tanda tangan semuanya terpisah dari form lain). Cocok untuk shift yang punya beberapa kali perintah langsir di jam berbeda. Saat dicetak, semua form dalam shift itu tercetak berurutan, masing-masing mulai di halaman baru.
- **Export / Import JSON per shift** — menyimpan seluruh form dalam satu shift ke satu file `.json`.

### Pengisian data
- **Nomor surat & Hari/Tanggal otomatis** per form (`NOMOR: 13/KTG/VI/2026`, `KAMIS/18-06-2026`), dengan **panah maju/mundur 1 hari** di sebelah tanggal — berguna kalau satu lembar form dibuat untuk beberapa hari ke depan sekaligus (form 1 = hari ini, form 2 = besok, dst).
- **Edit Keterangan via popup yang bisa digeser** — tombol hijau "Edit Keterangan" di tiap rangkaian membuka kotak tempel/ketik massal (mis. hasil copy dari simulator). Tabel utama tetap tampil rapi seperti spreadsheet asli.
- **Kolom Keterangan, Posisi Awal, Posisi Akhir, dan nama rangkaian bisa diedit langsung di tabel** — tersinkron dua arah dengan popup; perubahan terakhir yang dipakai. Tekan **Enter** di kolom Keterangan untuk pindah ke baris bawah; kalau baris bawah belum ada, akan dibuat otomatis dan kursor langsung pindah ke sana.
- **Sisip / hapus baris manual** lewat menu titik-tiga di tiap baris (sisip di atas/bawah, atau hapus). Berguna untuk kombinasi posisi yang belum ada di tabel RUTE.
- **Hitung jumlah kereta otomatis (LOKO + n KERETA)** dari teks `AMBIL n KRT`, `LEPAS n KRT`, atau `LEPAS SEMUA`.
- **Judul rangkaian otomatis**, dihitung dari posisi yang punya keterangan ambil/lepas saja.
- **Lookup urutan pergerakan & wesel otomatis** dari tabel RUTE, dengan catatan jelas kalau kombinasi belum dikenal.
- **Posisi awal berantai otomatis** antar rangkaian dan antar form (form kedua bisa lanjut dari posisi akhir form pertama bila diisi manual).
- **Catatan kaki (NB)** dan **nama petugas tanda tangan** bisa diedit, lengkap dengan label "Yang Menerima Perintah" / "Yang Memerintah" sesuai tata letak asli.

### Tampilan & layout
- **Ubah font dan ukuran teks dengan blok** — sorot/blok sebagian teks di kolom manual (nama rangkaian, Keterangan, catatan kaki) untuk memunculkan toolbar kecil mengambang, pilih font dan ukuran khusus bagian itu saja (seperti di Word).
- **Pengaturan font global untuk kolom otomatis** — dropdown di toolbar atas mengatur font & ukuran kolom LOKO dan Urutan Pergerakan untuk semua baris (kolom ini tidak bisa diblok manual karena terus digenerate ulang oleh sistem).
- **Geser lebar kolom** — arahkan kursor ke tepi kanan judul kolom tabel (Rangkaian, Posisi Awal/Akhir, Urutan Pergerakan, Keterangan) lalu drag untuk mengatur ulang lebar sesuai kebutuhan ukuran kertas/printer. Lebar tersimpan otomatis dan berlaku untuk semua form & shift.
- **Cetak / Simpan PDF** — tampilan cetak bersih tanpa tombol/menu/toolbar, semua form dalam shift tercetak berurutan.
- **Tersimpan otomatis di browser** (localStorage), termasuk pengaturan font dan lebar kolom.

## Cara isi form (alur kerja harian)

1. Pilih tab shift yang sesuai.
2. Kalau perlu lebih dari satu form dalam shift ini (misal ada 2 perintah langsir di jam berbeda), klik **+ Tambah Form Langsir**.
3. Di form yang aktif, klik **+ Tambah Rangkaian**, beri nama (misal `EX KA279`).
4. Klik **Edit Keterangan**, isi posisi awal pertama (manual untuk rangkaian pertama, biasanya `DL`), lalu ketik/tempel baris gerakan format `LABEL: teks`.
5. Klik **Terapkan ke Tabel**.
6. Kalau ada catatan "kombinasi posisi belum ada di tabel RUTE", gunakan menu titik-tiga di baris itu untuk **sisip baris** manual lewat jalur perantara yang sesuai kondisi lapangan.
7. Ulangi untuk rangkaian/form berikutnya.
8. Sesuaikan lebar kolom (drag tepi header) dan font sesuai kebutuhan cetak.
9. Isi jam, pilih nama petugas tanda tangan, lalu Cetak/Simpan PDF atau Export JSON untuk arsip.

## Mengedit data referensi (RUTE dan TTD)

Semua data ada di bagian awal script `index.html`, ditandai komentar:

```js
/* =========================================================
   DATA — silakan diedit sesuai kebutuhan stasiun/emplasemen
   ========================================================= */
```

- **`RUTE`** — array `[Posisi Awal, Posisi Akhir, Urutan Gerakan, Wesel]`.
- **`TTD`** — objek `{ "NAMA": "NIPP" }` untuk dropdown tanda tangan.

Edit langsung di teks editor (Notepad, VS Code, dll), simpan, refresh browser.

## Catatan

- Data tersimpan di localStorage hanya berlaku per browser/perangkat. Pakai Export/Import JSON untuk memindahkan data antar perangkat atau membuat arsip harian.
- Kalau butuh sinkronisasi otomatis multi-pengguna di banyak perangkat secara realtime, perlu backend/database tambahan — bisa didiskusikan lebih lanjut kalau diperlukan.
