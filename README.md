<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Verifikasi Surat | Senat Mahasiswa STITNU</title>
  <style>
    :root {
      color-scheme: light dark;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #fff;
      color: #000;
      transition: background-color 0.3s, color 0.3s;
      padding: 2rem;
    }

    @media (prefers-color-scheme: dark) {
      body {
        background-color: #121212;
        color: #fff;
      }

      input, button {
        background-color: #1e1e1e;
        color: #fff;
        border: 1px solid #444;
      }

      table {
        background-color: #1e1e1e;
        color: #fff;
      }

      th, td {
        border-color: #333;
      }
    }

    h1 {
      text-align: center;
      margin-bottom: 2rem;
    }

    .container {
      max-width: 600px;
      margin: auto;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    input[type="text"] {
      padding: 0.75rem;
      font-size: 1rem;
      border: 1px solid #ccc;
      border-radius: 6px;
      transition: all 0.3s;
    }

    button {
      padding: 0.75rem;
      font-size: 1rem;
      border: none;
      border-radius: 6px;
      background-color: #0066cc;
      color: white;
      cursor: pointer;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #004999;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      margin-top: 1rem;
      animation: fadeIn 0.5s ease-in-out;
    }

    th, td {
      padding: 0.75rem;
      border: 1px solid #ddd;
      text-align: left;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 600px) {
      body {
        padding: 1rem;
      }

      h1 {
        font-size: 1.5rem;
      }

      table, th, td {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Verifikasi Nomor Surat</h1>
    <div class="form-group">
      <input type="text" id="nomorSurat" placeholder="Masukkan nomor surat..." />
      <button onclick="verifikasiSurat()">Verifikasi</button>
    </div>
    <div id="hasilVerifikasi"></div>
  </div>

  <script>
    const dataSurat = [
      {
        nomor: "001/SM-STITNU/2024",
        judul: "Undangan Rapat Kerja",
        instansi: "Senat Mahasiswa STITNU Al-Farabi",
        tanggal: "2024-01-15",
        status: "TERVERIFIKASI ✅"
      },
      {
        nomor: "002/SM-STITNU/2024",
        judul: "Pemberitahuan Pelantikan",
        instansi: "Senat Mahasiswa STITNU Al-Farabi",
        tanggal: "2024-02-20",
        status: "TERVERIFIKASI ✅"
      }
    ];

    function verifikasiSurat() {
      const input = document.getElementById("nomorSurat").value.trim();
      const hasilDiv = document.getElementById("hasilVerifikasi");

      const surat = dataSurat.find(s => s.nomor.toLowerCase() === input.toLowerCase());

      if (surat) {
        hasilDiv.innerHTML = `
          <table>
            <tr><th>Nomor Surat</th><td>${surat.nomor}</td></tr>
            <tr><th>Judul</th><td>${surat.judul}</td></tr>
            <tr><th>Instansi</th><td>${surat.instansi}</td></tr>
            <tr><th>Tanggal</th><td>${surat.tanggal}</td></tr>
            <tr><th>Status</th><td style="color:limegreen; font-weight: bold;">${surat.status}</td></tr>
          </table>
        `;
      } else {
        hasilDiv.innerHTML = `<p style="color:tomato; font-weight:bold;">❌ Nomor surat tidak ditemukan atau tidak valid.</p>`;
      }
    }
  </script>
</body>
</html>
