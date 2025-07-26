<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Verifikasi Surat TTE</title>
  <style>
    :root {
      color-scheme: light dark;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: var(--bg-color, #ffffff);
      color: var(--text-color, #000000);
      transition: background-color 0.4s ease, color 0.4s ease;
    }

    @media (prefers-color-scheme: dark) {
      body {
        --bg-color: #121212;
        --text-color: #ffffff;
      }

      table, th, td {
        border-color: #ffffff;
      }
    }

    @media (prefers-color-scheme: light) {
      body {
        --bg-color: #ffffff;
        --text-color: #000000;
      }

      table, th, td {
        border-color: #000000;
      }
    }

    .container {
      max-width: 600px;
      margin: 80px auto;
      padding: 30px;
      background: rgba(255,255,255,0.05);
      backdrop-filter: blur(10px);
      border-radius: 16px;
      box-shadow: 0 8px 30px rgba(0,0,0,0.3);
      animation: fadeIn 1s ease;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      font-weight: 600;
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    input[type="text"] {
      padding: 12px;
      font-size: 16px;
      border-radius: 8px;
      border: 1px solid #ccc;
      outline: none;
      background-color: var(--bg-color);
      color: var(--text-color);
    }

    input[type="text"]::placeholder {
      color: #888;
    }

    button {
      padding: 12px;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background: #007bff;
      color: white;
      transition: background 0.3s ease;
    }

    button:hover {
      background: #0056b3;
    }

    #hasilVerifikasi {
      margin-top: 20px;
      animation: fadeInUp 0.5s ease;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }

    th, td {
      padding: 12px;
      border: 1px solid;
      text-align: left;
      background-color: rgba(255, 255, 255, 0.1);
    }

    th {
      background-color: rgba(0, 123, 255, 0.8);
      color: #fff;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 600px) {
      .container {
        margin: 20px;
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Verifikasi Tanda Tangan Elektronik</h2>
    <form id="formVerifikasi">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" required>
      <button type="submit">Verifikasi</button>
    </form>
    <div id="hasilVerifikasi"></div>
  </div>

  <script>
    const dataSurat = {
      "001/SM/2025": {
        judul: "Undangan Rapat Koordinasi",
        tanggal: "20 Juli 2025",
        pengirim: "Senat Mahasiswa STITNU Al-Farabi Pangandaran"
      },
      "002/SM/2025": {
        judul: "Surat Tugas Kegiatan Sosial",
        tanggal: "15 Juli 2025",
        pengirim: "Ketua Umum Senat Mahasiswa"
      },
      "003/SM/2025": {
        judul: "Pemberitahuan Pelantikan",
        tanggal: "10 Juli 2025",
        pengirim: "Divisi Kominfo & Kreatif"
      }
    };

    document.getElementById('formVerifikasi').addEventListener('submit', function(e) {
      e.preventDefault();
      const nomor = document.getElementById('nomorSurat').value.trim();
      const hasil = document.getElementById('hasilVerifikasi');

      if (nomor === '') {
        hasil.innerHTML = `<p style="color: red;">⚠️ Nomor surat tidak boleh kosong.</p>`;
        return;
      }

      if (dataSurat[nomor]) {
        const surat = dataSurat[nomor];
        hasil.innerHTML = `
          <div style="color: green;">
            <p>✅ Surat <strong>TERVERIFIKASI</strong></p>
            <table>
              <tr><th>Nomor Surat</th><td>${nomor}</td></tr>
              <tr><th>Judul</th><td>${surat.judul}</td></tr>
              <tr><th>Tanggal</th><td>${surat.tanggal}</td></tr>
              <tr><th>Pengirim</th><td>${surat.pengirim}</td></tr>
            </table>
          </div>
        `;
      } else {
        hasil.innerHTML = `<p style="color: red;">❌ Nomor surat <strong>tidak ditemukan</strong>.</p>`;
      }
    });
  </script>
</body>
</html>
