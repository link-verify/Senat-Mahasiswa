<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi TTE Surat | Senat Mahasiswa STITNU Al-Farabi Pangandaran</title>
  <!-- SweetAlert2 -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --primary: #4FC3F7;
      --secondary: #0288D1;
      --gradient: linear-gradient(135deg, #4FC3F7 0%, #0288D1 100%);
      --radius: 12px;
      --shadow: 0 10px 40px rgba(0,0,0,0.1);
    }

    html, body {
      margin: 0;
      padding: 0;
      font-family: 'Inter', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      background: #f0f4f8;
      color: #222;
    }

    header {
      text-align: center;
      padding: 40px 20px 20px;
    }

    header img {
      max-width: 120px;
      margin-bottom: 15px;
    }

    header h1 {
      margin: 0;
      font-size: 1.8rem;
      background: var(--gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    main {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      padding: 20px;
    }

    .card {
      background: #fff;
      padding: 40px;
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      max-width: 500px;
      width: 100%;
      transition: all 0.3s ease;
    }

    .card h2 {
      margin-top: 0;
      margin-bottom: 20px;
      background: var(--gradient);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    form {
      display: flex;
      flex-direction: column;
    }

    input {
      padding: 14px 16px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: var(--radius);
      font-size: 16px;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.05);
      transition: all 0.3s ease;
    }

    input:focus {
      border-color: var(--primary);
      outline: none;
      box-shadow: 0 0 8px rgba(79,195,247,0.4);
    }

    button {
      padding: 14px;
      background: var(--gradient);
      color: #fff;
      border: none;
      border-radius: var(--radius);
      cursor: pointer;
      font-weight: 600;
      font-size: 16px;
      box-shadow: 0 4px 20px rgba(79,195,247,0.4);
      transition: all 0.3s ease;
    }

    button:hover {
      transform: translateY(-2px);
    }

    #result {
      margin-top: 20px;
      opacity: 0;
      transform: translateY(10px);
      transition: opacity 0.5s ease, transform 0.5s ease;
    }

    #result.show {
      opacity: 1;
      transform: translateY(0);
    }

    #result.success {
      color: var(--secondary);
    }

    #result.error {
      color: #dc3545;
      font-weight: 600;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }

    td {
      padding: 6px 0;
    }

    td:first-child {
      font-weight: 600;
      color: #444;
      width: 40%;
    }

    footer {
      text-align: center;
      padding: 20px;
      font-size: 14px;
      color: #777;
    }

    /* Auto Dark Mode */
    @media (prefers-color-scheme: dark) {
      html, body {
        background: #111;
        color: #eee;
      }
      .card {
        background: #222;
        color: #eee;
      }
      input {
        background: #333;
        color: #eee;
        border: 1px solid #555;
      }
      button {
        box-shadow: 0 4px 20px rgba(79,195,247,0.6);
      }
    }

    @media(max-width: 600px) {
      .card {
        padding: 30px 20px;
      }
    }
  </style>
</head>

<body>
  <header>
    <h1>Verifikasi TTE Surat</h1>
  </header>

  <main>
    <div class="card">
      <h2>Cek Keaslian Surat</h2>
      <form id="verifyForm">
        <input type="text" id="nomorSurat" placeholder="Masukkan Nomor Surat" required />
        <button type="submit">Verifikasi</button>
      </form>
      <div id="result"></div>
    </div>
  </main>

  <footer>
    &copy; 2025 Senat Mahasiswa
    <p> STITNU Al-Farabi Pangandaran. </p>
  </footer>

  <script>
    const suratData = [
      {
        nomor: "001/TTE/2025",
        ditandatangani: ["Budi Santoso, S.Pd", "Rina Wijaya, M.M"],
        perihal: "Undangan Rapat Koordinasi",
        ditujukan: "Kepala Sekolah SMA Negeri 1 Pangandaran",
        tanggal: "15 Januari 2025"
      },
      {
        nomor: "MELEDAKS",
        ditandatangani: ["Agus Salim, M.Pd"],
        perihal: "Pemberitahuan Libur Sekolah",
        ditujukan: "Seluruh Orang Tua/Wali Murid",
        tanggal: "20 Februari 2025"
      },
      {
        nomor: "000/TTE/2025",
        ditandatangani: ["Syadad Nabil Mudzafar"],
        perihal: "Pemberitahuan Libur Sekolah",
        ditujukan: "Seluruh Orang Tua/Wali Murid",
        tanggal: "20 Februari 2025"
      }
    ];

    document.getElementById("verifyForm").addEventListener("submit", function(e) {
      e.preventDefault();
      const nomorInput = document.getElementById("nomorSurat").value.trim();
      const result = document.getElementById("result");
      const surat = suratData.find(item => item.nomor === nomorInput);

      if (surat) {
        result.className = "success show";
        result.innerHTML = `
          <p>Nomor Surat TERDAFTAR</p>
          <table>
            <tr><td>Nomor</td><td>${surat.nomor}</td></tr>
            <tr><td>Ditandatangani</td><td>${surat.ditandatangani.join(", ")}</td></tr>
            <tr><td>Perihal</td><td>${surat.perihal}</td></tr>
            <tr><td>Ditujukan</td><td>${surat.ditujukan}</td></tr>
            <tr><td>Tanggal</td><td>${surat.tanggal}</td></tr>
          </table>
          <br>
          <a href="https://wa.me/6285211379911?text=Nomor%20Surat%20${encodeURIComponent(surat.nomor)}%20telah%20terverifikasi." target="_blank">
            WhatsApp
          </a>
        `;
        Swal.fire({
          icon: 'success',
          title: 'Valid',
          text: `Nomor Surat "${surat.nomor}" terverifikasi.`,
          showConfirmButton: false,
          timer: 2000
        });
      } else {
        result.className = "error show";
        result.innerHTML = "❌ Nomor Surat TIDAK TERDAFTAR.";
        Swal.fire({
          icon: 'error',
          title: 'Gagal',
          text: 'Nomor Surat tidak terdaftar.',
          showConfirmButton: false,
          timer: 2000
        });
      }
    });
  </script>
</body>
</html>