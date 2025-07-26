<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Verifikasi Surat TTE</title>
  <style>
    :root {
      --primary: #0d6efd;
      --success: #28a745;
      --danger: #dc3545;
      --bg-dark: #121212;
      --text-light: #f1f1f1;
      --shadow: rgba(0, 0, 0, 0.6);
    }

    * {
      box-sizing: border-box;
      transition: all 0.3s ease;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--bg-dark);
      color: var(--text-light);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      animation: fadeIn 1s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .container {
      background-color: #1e1e1e;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 20px var(--shadow);
      width: 90%;
      max-width: 500px;
    }

    h2 {
      color: var(--primary);
      text-align: center;
    }

    input[type="text"] {
      width: 100%;
      padding: 12px;
      border: none;
      border-radius: 6px;
      margin-top: 15px;
      font-size: 16px;
      background-color: #2a2a2a;
      color: var(--text-light);
    }

    button {
      margin-top: 15px;
      width: 100%;
      padding: 12px;
      font-size: 16px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      box-shadow: 0 4px 12px rgba(13, 110, 253, 0.3);
    }

    button:hover {
      background: #0b5ed7;
    }

    table {
      width: 100%;
      margin-top: 20px;
      border-collapse: collapse;
      background-color: #2c2c2c;
      border-radius: 8px;
      overflow: hidden;
    }

    th, td {
      padding: 12px;
      border-bottom: 1px solid #444;
      text-align: left;
      color: var(--text-light);
    }

    th {
      background-color: #333;
      color: #fff;
    }

    .result {
      margin-top: 20px;
      font-size: 16px;
    }

    .success {
      color: var(--success);
    }

    .error {
      color: var(--danger);
    }

    @media (max-width: 600px) {
      .container {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>🔍 Verifikasi Tanda Tangan Elektronik</h2>
    <form id="formVerifikasi">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat Contoh: 001/SM/2025" required>
      <button type="submit">Verifikasi</button>
    </form>
    <div id="hasilVerifikasi" class="result"></div>
  </div>

  <script>
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
        judul: "Notulen Rapat Akhir Semester",
        tanggal: "10 Juli 2025",
        pengirim: "Sekretaris Senat Mahasiswa"
      }
    };

    document.getElementById('formVerifikasi').addEventListener('submit', function(e) {
      e.preventDefault();
      const nomor = document.getElementById('nomorSurat').value.trim();
      const hasil = document.getElementById('hasilVerifikasi');

      if (nomor === "") {
        hasil.innerHTML = `<div class="error">❌ Nomor surat tidak boleh kosong.</div>`;
        return;
      }

      if (dataSurat[nomor]) {
        const surat = dataSurat[nomor];
        hasil.innerHTML = `
          <div class="success">✅ Surat TERVERIFIKASI</div>
          <table>
            <tr><th>Nomor Surat</th><td>${nomor}</td></tr>
            <tr><th>Judul</th><td>${surat.judul}</td></tr>
            <tr><th>Tanggal</th><td>${surat.tanggal}</td></tr>
            <tr><th>Pengirim</th><td>${surat.pengirim}</td></tr>
          </table>
        `;
      } else {
        hasil.innerHTML = `<div class="error">❌ Nomor surat <strong>${nomor}</strong> tidak ditemukan dalam sistem.</div>`;
      }
    });
  </script>
</body>
</html>
