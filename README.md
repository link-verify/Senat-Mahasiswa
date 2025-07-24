<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Verifikasi Surat TTE</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #e9f1fb;
      margin: 0;
      padding: 0;
    }

    .container {
      max-width: 500px;
      margin: 80px auto;
      padding: 30px;
      background: white;
      border-radius: 12px;
      box-shadow: 0 0 15px rgba(0,0,0,0.1);
      text-align: center;
    }

    h2 {
      color: #007bff;
    }

    input[type="text"] {
      width: 80%;
      padding: 10px;
      margin-top: 20px;
      font-size: 16px;
      border: 2px solid #007bff;
      border-radius: 5px;
    }

    button {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 16px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background: #0056b3;
    }

    #hasilVerifikasi {
      margin-top: 25px;
      font-weight: bold;
      font-size: 18px;
    }

    @media (max-width: 600px) {
      .container {
        margin: 40px 15px;
        padding: 25px;
      }

      input[type="text"] {
        width: 100%;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Verifikasi Tanda Tangan Elektronik</h2>
    <form id="formVerifikasi">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" required>
      <br>
      <button type="submit">Verifikasi</button>
    </form>
    <div id="hasilVerifikasi"></div>
  </div>

  <script>
    // === CONTOH DATA SURAT YANG TELAH TERVERIFIKASI ===
    const dataSurat = {
      "001/SM/2025": {
        judul: "Undangan Rapat Koordinasi Divisi",
        tanggal: "20 Juli 2025",
        pengirim: "Senat Mahasiswa STITNU Al-Farabi Pangandaran",
        status: "Aktif"
      },
      "002/SM/2025": {
        judul: "Surat Tugas Pelatihan Dasar Kepemimpinan",
        tanggal: "15 Juli 2025",
        pengirim: "Ketua Senat Mahasiswa STITNU Al-Farabi",
        status: "Aktif"
      },
      "003/SM/2025": {
        judul: "Pemberitahuan Kegiatan Bakti Sosial",
        tanggal: "10 Juli 2025",
        pengirim: "Sekretaris Senat Mahasiswa STITNU",
        status: "Aktif"
      },
      "004/SM/2024": {
        judul: "Surat Edaran Libur Semester Ganjil",
        tanggal: "15 Desember 2024",
        pengirim: "Wakil Ketua Senat Mahasiswa",
        status: "Kadaluarsa"
      }
    };

    // === LOGIKA VERIFIKASI ===
    document.getElementById('formVerifikasi').addEventListener('submit', function(e) {
      e.preventDefault();
      const nomor = document.getElementById('nomorSurat').value.trim();
      const hasil = document.getElementById('hasilVerifikasi');

      if (nomor === '') {
        hasil.innerHTML = `<span style="color:red;">Nomor surat tidak boleh kosong.</span>`;
        return;
      }

      if (dataSurat[nomor]) {
        const surat = dataSurat[nomor];
        const warna = surat.status === "Aktif" ? "green" : "orange";
        const icon = surat.status === "Aktif" ? "✅" : "⚠️";

        hasil.innerHTML = `
          <div style="color:${warna};">
            ${icon} Surat <strong>${surat.status === "Aktif" ? "TERVERIFIKASI" : "TERVERIFIKASI TAPI KADALUARSA"}</strong><br><br>
            <strong>Nomor Surat:</strong> ${nomor}<br>
            <strong>Judul:</strong> ${surat.judul}<br>
            <strong>Tanggal:</strong> ${surat.tanggal}<br>
            <strong>Pengirim:</strong> ${surat.pengirim}
          </div>
        `;
      } else {
        hasil.innerHTML = `<span style="color:red;">❌ Nomor surat <strong>${nomor}</strong> tidak ditemukan dalam basis data kami.</span>`;
      }
    });
  </script>
</body>
</html>
