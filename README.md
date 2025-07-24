<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi Surat TTE</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #121212;
      color: #e0e0e0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      animation: fadeIn 1s ease-in-out;
    }

    .container {
      background-color: #1e1e1e;
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.7);
      width: 100%;
      max-width: 500px;
      animation: slideUp 1s ease-in-out;
    }

    h2 {
      text-align: center;
      margin-bottom: 25px;
      color: #00bfff;
    }

    input[type="text"] {
      width: 100%;
      padding: 12px;
      border: none;
      border-radius: 10px;
      margin-bottom: 15px;
      font-size: 16px;
      background: #2c2c2c;
      color: #fff;
      outline: none;
      transition: 0.3s;
    }

    input[type="text"]:focus {
      background: #3a3a3a;
      border: 1px solid #00bfff;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #00bfff;
      border: none;
      border-radius: 10px;
      color: white;
      font-size: 16px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background-color: #009acf;
    }

    .result {
      margin-top: 20px;
      animation: fadeIn 0.5s ease-in-out;
    }

    table {
      width: 100%;
      margin-top: 10px;
      border-collapse: collapse;
      background-color: #2c2c2c;
      color: #fff;
      border-radius: 10px;
      overflow: hidden;
    }

    th, td {
      padding: 12px;
      border-bottom: 1px solid #444;
      text-align: left;
    }

    th {
      background-color: #00bfff;
      color: #000;
    }

    @keyframes fadeIn {
      from { opacity: 0 }
      to { opacity: 1 }
    }

    @keyframes slideUp {
      from { transform: translateY(30px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    @media (max-width: 600px) {
      .container {
        padding: 25px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Verifikasi Surat TTE</h2>
    <form id="formVerifikasi">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat..." required>
      <button type="submit">Verifikasi</button>
    </form>
    <div id="hasilVerifikasi" class="result"></div>
  </div>

  <script>
    // Simulasi data surat
    const dataSurat = {
      "001/SM/2025": {
        judul: "Undangan Rapat Koordinasi",
        tanggal: "20 Juli 2025",
        pengirim: "Senat Mahasiswa STITNU Al-Farabi"
      },
      "002/SM/2025": {
        judul: "Surat Tugas Kegiatan Sosial",
        tanggal: "15 Juli 2025",
        pengirim: "Ketua Senat Mahasiswa STITNU"
      },
      "003/SM/2025": {
        judul: "Pengumuman Pelantikan",
        tanggal: "1 Agustus 2025",
        pengirim: "Sekretariat Senat Mahasiswa"
      }
    };

    document.getElementById('formVerifikasi').addEventListener('submit', function (e) {
      e.preventDefault();
      const nomor = document.getElementById('nomorSurat').value.trim();
      const hasil = document.getElementById('hasilVerifikasi');
      hasil.innerHTML = '';

      if (nomor === '') {
        hasil.innerHTML = `<span style="color:tomato;">❌ Nomor surat wajib diisi.</span>`;
        return;
      }

      const surat = dataSurat[nomor];
      if (surat) {
        hasil.innerHTML = `
          <div style="color:lightgreen; font-weight:600;">✅ Surat TERVERIFIKASI</div>
          <table>
            <tr><th>Field</th><th>Informasi</th></tr>
            <tr><td>Nomor Surat</td><td>${nomor}</td></tr>
            <tr><td>Judul</td><td>${surat.judul}</td></tr>
            <tr><td>Tanggal</td><td>${surat.tanggal}</td></tr>
            <tr><td>Pengirim</td><td>${surat.pengirim}</td></tr>
          </table>
        `;
      } else {
        hasil.innerHTML = `<span style="color:tomato;">❌ Nomor surat tidak ditemukan dalam database.</span>`;
      }
    });
  </script>
</body>
</html>
