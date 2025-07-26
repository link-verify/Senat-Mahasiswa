<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Verifikasi Surat SENAT MAHASISWA</title>
  <style>
    :root {
      color-scheme: light dark;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(to bottom right, #e0f7ff, #d5e8ff);
      color: var(--text-color, #000000);
      transition: background 0.4s ease, color 0.4s ease;
    }

    @media (prefers-color-scheme: dark) {
      body {
        --bg-color: #121212;
        --text-color: #ffffff;
        background: linear-gradient(to bottom right, #1e1e1e, #2c2c2c);
      }

      table, th, td {
        border-color: #ffffff;
      }

      .popup {
        background-color: #333;
        color: #fff;
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

      .popup {
        background-color: #f0f0f0;
        color: #000;
      }
    }

    .container {
      max-width: 600px;
      margin: 5vh auto;
      padding: 30px 20px;
      background: rgba(255,255,255,0.1);
      backdrop-filter: blur(15px);
      border-radius: 16px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.3);
      animation: fadeIn 1s ease;
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
      font-weight: 700;
      font-size: 1.8rem;
    }

    form {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    input[type="text"] {
      padding: 14px;
      font-size: 1rem;
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
      padding: 14px;
      font-size: 1rem;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      background: linear-gradient(to right, #007bff, #00b4ff);
      color: white;
      transition: all 0.3s ease;
    }

    button:hover {
      background: linear-gradient(to right, #0056b3, #0093d0);
      transform: translateY(-2px);
    }

    #hasilVerifikasi {
      margin-top: 20px;
      animation: fadeInUp 0.6s ease;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
      overflow-x: auto;
      display: block;
    }

    th, td {
      padding: 12px;
      border: 1px solid;
      text-align: left;
      background-color: rgba(255, 255, 255, 0.1);
    }

    th {
      background-color: rgba(0, 123, 255, 0.85);
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

    .popup {
      position: fixed;
      bottom: 30px;
      right: 30px;
      padding: 14px 20px;
      border-radius: 10px;
      box-shadow: 0 6px 16px rgba(0,0,0,0.3);
      font-weight: 600;
      opacity: 0;
      pointer-events: none;
      transform: translateY(20px);
      transition: all 0.4s ease;
      z-index: 999;
    }

    .popup.show {
      opacity: 1;
      transform: translateY(0);
      pointer-events: auto;
    }

    img {
      max-width: 120px;
      display: block;
      margin: 0 auto 20px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    @media (max-width: 600px) {
      h2 {
        font-size: 1.4rem;
      }

      input[type="text"],
      button {
        font-size: 0.95rem;
        padding: 12px;
      }

      .popup {
        width: calc(100% - 40px);
        right: 20px;
        bottom: 20px;
        font-size: 0.9rem;
      }

      table th, table td {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <img src="Gambar WhatsApp 2025-07-14 pukul 01.05.14_658e4143.jpg" alt="Logo Senat Mahasiswa">
    <h2>Verifikasi Surat Senat Mahasiswa</h2>
    <form id="formVerifikasi">
      <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" required>
      <button type="submit">Verifikasi</button>
    </form>
    <div id="hasilVerifikasi"></div>
  </div>

  <div class="popup" id="popupNotif"></div>

  <script>
    const dataSurat = {
      "01.010/KMH-STITNU/7052/V/2025": {
        judul: "Pengangkatan Pengurus Senat Mahasiswa STITNU AL-FARABI 2025-2026",
        tanggal: "21 Mei 2025",
        pengirim: "Ketua STITNU Al-Farabi Pangandaran"
      }
    };

    function showPopup(message, success = true) {
      const popup = document.getElementById('popupNotif');
      popup.textContent = message;
      popup.style.backgroundColor = success ? 'rgba(0,200,100,0.9)' : 'rgba(255,50,50,0.9)';
      popup.classList.add('show');
      setTimeout(() => {
        popup.classList.remove('show');
      }, 3000);
    }

    document.getElementById('formVerifikasi').addEventListener('submit', function(e) {
      e.preventDefault();
      const nomor = document.getElementById('nomorSurat').value.trim();
      const hasil = document.getElementById('hasilVerifikasi');

      if (nomor === '') {
        hasil.innerHTML = '';
        showPopup('⚠️ Nomor surat tidak boleh kosong.', false);
        return;
      }

      if (dataSurat[nomor]) {
        const surat = dataSurat[nomor];
        hasil.innerHTML = `
          <div style="color: green;">
            <p>✅ <strong>Surat Terverifikasi</strong></p>
            <table>
              <tr><th>Nomor Surat</th><td>${nomor}</td></tr>
              <tr><th>Perihal</th><td>${surat.judul}</td></tr>
              <tr><th>Tanggal</th><td>${surat.tanggal}</td></tr>
              <tr><th>Ditandatangani</th><td>${surat.pengirim}</td></tr>
            </table>
          </div>
        `;
        showPopup('✅ Surat Terverifikasi');
      } else {
        hasil.innerHTML = `<p style="color: red;">❌ <strong>Nomor surat tidak ditemukan.</strong></p>`;
        showPopup('❌ Nomor surat tidak ditemukan.', false);
      }
    });
  </script>
  <a href="<a href="BERANDA" class="btn-beranda">🏠 Ke Beranda</a>
" class="btn-beranda">🏠 Ke Beranda</a>

</body>
</html>
