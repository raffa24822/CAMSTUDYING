CAMSTUDY_FINAL_FILE — PETUNJUK DEPLOY

File untuk repository GitHub:
- CAMSTUDY_FINAL_FILE.html
- CAMSTUDY_FINAL_FILE_SERVER.js
- package.json

Render:
1. Buat Web Service dari repository GitHub.
2. Build Command: npm install
3. Start Command: npm start
4. Tambahkan Environment Variable:
   OPENAI_API_KEY = API key OpenAI milik pengelola (jangan masukkan ke HTML/GitHub)
   TEACHER_PASSWORD = password login guru pilihan sendiri
   DATA_DIR = /var/data (gunakan jika memasang Persistent Disk di /var/data)
5. Jika memakai DATA_DIR=/var/data, tambahkan Persistent Disk dengan mount path /var/data agar data tidak hilang saat instance diganti.
6. Setelah deploy, buka URL Render. Endpoint /health harus menampilkan status ok.

Catatan penting:
- Font Awesome eksternal masih dipakai di beberapa tombol; ikon mata pelajaran pada kartu siswa memakai emoji bawaan sebagai fallback agar tetap terlihat jika CDN ikon lambat/gagal.
- Fitur AI dari materi membutuhkan OPENAI_API_KEY yang valid, kuota/billing API aktif, dan login guru yang valid. Tidak mungkin menjamin AI selalu berhasil karena layanan dan jaringan eksternal dapat gagal.
- Materi disimpan dalam daftar Materi Pelajaran & Tugas: pilih jenis “Materi pelajaran”, pilih mapel, isi judul/deskripsi, lalu simpan dan tekan Simpan ke Server. Berkas maksimal 1,5 MB sesuai batas portal saat ini.
- Status Offline dikirim saat halaman disembunyikan/ditinggalkan dan heartbeat tidak lagi menandai tab tersembunyi sebagai online. Browser/OS dapat membatasi pengiriman saat aplikasi ditutup paksa, sehingga monitor juga menggunakan lastSeen.
- Backup data server sebelum mengganti file versi lama.


PATCH PEMULIHAN QUIZ (03-10-2026)
- Hanya urutan SOAL yang diacak; opsi A/B/C/D dan indeks kunci tetap persis seperti data guru.
- Review hasil menangani soal pilihan tunggal, pilihan ganda lebih dari satu, dan esai.
- Setelah quiz selesai, portal mencoba menunggu konfirmasi simpan nilai dari server; jika gagal, nilai tetap lokal dan status memberi peringatan.
- Counter pelanggaran server digabung memakai nilai maksimum agar sinkronisasi perangkat lama tidak menurunkannya.
- Penghitungan keluar-tab tetap bergantung pada browser mengirim event visibilitychange/pagehide; browser/perangkat tertentu dapat membatasi event saat aplikasi ditutup paksa/offline.

Perbaikan terbaru: urutan soal diacak tanpa mengacak opsi A–D; reset akun mengirim token sesi guru yang aktif; pelanggaran saat keluar dari tab ujian dikirim melalui beacon/keepalive dan server membuat catatan minimal bila sinkronisasi profil terlambat.
