<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Verifikasi Surat | STITNU</title>
  <style>
    :root {
      --bg-color-light: #ffffff;
      --text-color-light: #000000;
      --bg-color-dark: #121212;
      --text-color-dark: #ffffff;
      --accent-color: #1e90ff;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      transition: background-color 0.5s ease, color 0.5s ease;
      background-color: var(--bg-color-light);
      color: var(--text-color-light);
    }

    @media (prefers-color-scheme: dark) {
      body {
        background-color: var(--bg-color-dark);
        color: var(--text-color-dark);
      }

      table {
        background-color: #1e1e1e;
      }

      th, td {
        color: #f0f0f0;
      }

      input, button {
        background-color: #222;
        color: #fff;
        border: 1px solid #444;
      }
    }

    .container {
      max-width: 600px;
      margin: 50px auto;
      padding: 20px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      border-radius: 10px;
      background: inherit;
      animation: fadeIn 1s ease-in-out;
    }

    @keyframes fadeIn {
      from {opacity: 0; transform: translateY(20px);}
      to {opacity: 1; transform: translateY(0);}
    }

    h1 {
      text-align: center;
      color: var(--accent-color);
    }

    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-sizing: border-box;
      font-size: 16px;
    }

    button {
      margin-top: 15px;
      width: 100%;
      padding: 10px;
      font-size: 16px;
      background-color: var(--accent-color);
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #187bcd;
    }

    .result-table {
      margin-top: 20px;
      width: 100%;
      border-collapse: collapse;
      animation: fadeIn 0.5s ease-in-out;
    }

    th, td {
      padding: 10px;
      border: 1px solid #ccc;
      text-align: left;
    }

    @media screen and (max-width: 600px) {
      .container {
        margin: 20px 10px;
        padding: 15px;
      }

      h1 {
        font-size: 1.5em;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Verifikasi Surat</h1>
    <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" />
    <button onclick="verifikasiSurat()">Verifikasi</button>

    <div id="hasilVerifikasi"></div>
  </div>

  <script>
    const dataSurat = [
      {
        nomor: "001/SM/07/2025",
        nama: "Syadad Nabil Mudzafar",
        perihal: "Pelantikan Senat Mahasiswa",
        tanggal: "20 Juli 2025",
        status: "Terverifikasi"
      },
      {
        nomor: "002/SM/07/2025",
        nama: "Rismah Nurani",
        perihal: "Undangan Rapat Akbar",
        tanggal: "18 Juli 2025",
        status: "Terverifikasi"
      }
    ];

    function verifikasiSurat() {
      const input = document.getElementById("nomorSurat").value.trim();
      const hasil = document.getElementById("hasilVerifikasi");
      const surat = dataSurat.find(item => item.nomor === input);

      if (surat) {
        hasil.innerHTML = `
          <table class="result-table">
            <tr><th>Nomor Surat</th><td>${surat.nomor}</td></tr>
            <tr><th>Nama</th><td>${surat.nama}</td></tr>
            <tr><th>Perihal</th><td>${surat.perihal}</td></tr>
            <tr><th>Tanggal</th><td>${surat.tanggal}</td></tr>
            <tr><th>Status</th><td style="color: limegreen;"><strong>${surat.status}</strong></td></tr>
          </table>
        `;
      } else {
        hasil.innerHTML = `<p style="color: red; text-align: center; margin-top: 15px;">Nomor surat tidak ditemukan.</p>`;
      }
    }
  </script>
</body>
</html>
