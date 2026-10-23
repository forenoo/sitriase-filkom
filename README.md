# SiTriase FILKOM

Mockup MVP front-end untuk **Sistem Triase Otomatis Aduan Pusat Layanan FILKOM**. Sistem menyortir aduan mahasiswa berdasarkan urgensi (deteksi kata kunci), merekomendasikan petugas, dan petugas tetap bisa meng-override sebelum tiket masuk antrian kerja.

> Ini mockup front-end. Data disimpan di array JavaScript dan akan kembali ke data awal setiap halaman dimuat ulang.

## Fitur

| Tampilan | Peran | Isi |
|---|---|---|
| **Kirim Aduan** (`#/submit`) | Mahasiswa | Form aduan + panel *Deteksi Urgensi* live (chip kata kunci, rekomendasi petugas), toast nomor tiket |
| **Review Triase** (`#/review`) | Petugas | Daftar tiket "Menunggu Review", modal detail dengan override urgensi/petugas + alasan |
| **Antrian Kerja** (`#/antrian`) | Petugas / PM | Kartu statistik (termasuk % override), antrian terurut urgensi, filter tab, tombol Tandai Selesai |

Kode warna urgensi: **Tinggi = merah**, **Sedang = amber**, **Rendah = hijau**.

Untuk presentasi: pakai tombol **"Isi contoh untuk demo"** di form, lalu ganti peran lewat toggle **Mahasiswa / Petugas** di header.

## Menjalankan di komputer sendiri

```bash
npm install
npm run dev
# buka http://localhost:3000
```

---

## Panduan Upload ke GitHub

Prasyarat: [Git](https://git-scm.com/downloads) dan [Node.js 18+](https://nodejs.org) sudah terpasang, dan kamu punya akun GitHub.

**1. Buat folder proyek** (lewati jika foldernya sudah ada)

```bash
mkdir sitriase-filkom
cd sitriase-filkom
# salin index.html, package.json, .gitignore, README.md ke folder ini
```

**2. Atur identitas Git** (sekali saja per komputer)

```bash
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"
```

**3. Inisiasi Git**

```bash
git init
git branch -M main
```

**4. Pastikan `.gitignore` ada** supaya `node_modules` tidak ikut ter-upload. Isinya:

```
node_modules/
.DS_Store
Thumbs.db
.env
```

**5. Simpan file (commit)**

```bash
npm install          # membuat package-lock.json
git add .
git status           # cek: node_modules TIDAK boleh muncul di daftar
git commit -m "feat: mockup MVP SiTriase FILKOM"
```

**6. Buat repository baru di GitHub**

1. Buka https://github.com/new
2. Isi *Repository name*: `sitriase-filkom`
3. Pilih **Public** (agar bisa jadi portofolio)
4. **Jangan** centang "Add a README" / ".gitignore" / "license" (sudah ada di lokal)
5. Klik **Create repository**

**7. Hubungkan dan push**

```bash
git remote add origin https://github.com/USERNAME/sitriase-filkom.git
git push -u origin main
```

Ganti `USERNAME` dengan username GitHub-mu. Jika diminta login, ikuti jendela login GitHub yang muncul (atau gunakan Personal Access Token sebagai password).

Untuk update berikutnya cukup:

```bash
git add .
git commit -m "pesan perubahan"
git push
```

---

## Panduan Live Deploy ke Railway.app

**1. Login**
Buka https://railway.app → **Login** → pilih **Login with GitHub** dan izinkan akses.

**2. Buat project dari GitHub repo**
Di dashboard klik **New Project** → **Deploy from GitHub repo**.
Jika repo belum muncul, klik **Configure GitHub App** dan beri Railway akses ke repo `sitriase-filkom` (atau semua repo).

**3. Pilih repository**
Klik `sitriase-filkom`. Railway otomatis mendeteksi proyek Node.js dari `package.json`, menjalankan `npm install`, lalu `npm start`.

**4. Start command (biasanya tidak perlu diubah)**
`package.json` sudah berisi:

```json
"start": "serve . -l tcp://0.0.0.0:$PORT"
```

Railway mengisi variabel `PORT` secara otomatis. Jika ingin memastikan, buka service → tab **Settings** → bagian **Deploy** → **Custom Start Command**, isi `npm start`.

**5. Generate domain publik**
Buka service → tab **Settings** → bagian **Networking** → klik **Generate Domain**.
Jika diminta memasukkan port, isi dengan port yang tertulis di log deploy (lihat tab **Deployments → View Logs**, baris `Accepting connections at http://0.0.0.0:XXXX`), biasanya `8080`.
Railway memberi URL seperti `https://sitriase-filkom-production.up.railway.app`.

**6. Selesai**
Buka URL tersebut. Setiap kali kamu `git push` ke branch `main`, Railway otomatis deploy ulang.

### Troubleshooting

| Masalah | Solusi |
|---|---|
| *Application failed to respond* | Pastikan start command memakai `0.0.0.0:$PORT`, bukan `localhost:3000` |
| Build gagal karena versi Node | Cek `"engines": { "node": ">=18" }` di `package.json` |
| Repo tidak muncul di Railway | Settings GitHub → Applications → Railway → beri akses ke repo |
| Kena batas trial | Railway memberi kredit trial terbatas; cek sisa kredit di menu **Usage** |
