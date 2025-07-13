<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi TTE Surat</title>
  <!-- SweetAlert2 -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --primary: #21A9A0; /* Asumsi hijau toska dari logo */
      --secondary: #17817A;
      --light-bg: #f6f9f8;
      --shadow: 0 10px 30px rgba(0,0,0,0.1);
      --radius: 12px;
      --transition: all 0.3s ease;
    }

    body {
      margin: 0;
      font-family: 'Inter', sans-serif;
      background: var(--light-bg);
      color: #333;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    header {
      text-align: center;
      padding: 40px 20px 20px;
    }

    header img {
      max-width: 100px;
      margin-bottom: 10px;
    }

    header h1 {
      margin: 0;
      font-weight: 700;
      color: var(--primary);
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
      transition: var(--transition);
    }

    .card h2 {
      margin-top: 0;
      color: var(--primary);
    }

    form {
      display: flex;
      flex-direction: column;
    }

    input {
      padding: 12px 15px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: var(--radius);
      font-size: 16px;
      transition: var(--transition);
    }

    input:focus {
      border-color: var(--primary);
      outline: none;
      box-shadow: 0 0 5px rgba(33, 169, 160, 0.3);
    }

    button {
      padding: 12px;
      background: var(--primary);
      color: #fff;
      border: none;
      border-radius: var(--radius);
      cursor: pointer;
      font-weight: 600;
      font-size: 16px;
      box-shadow: 0 4px 12px rgba(33,169,160,0.3);
      transition: var(--transition);
    }

    button:hover {
      background: var(--secondary);
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
      color: var(--primary);
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
      color: #aaa;
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
    <img src="https://drive.google.com/uc?export=view&id=1RtL277zYQBcQRQ7gCeV1UhQ5o91GIMVk" alt="Logo Organisasi">
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
    &copy; 2025 Organisasi Anda. All rights reserved.
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
        nomor: "002/TTE/2025",
        ditandatangani: ["Agus Salim, M.Pd"],
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
          <p>✅ Nomor Surat TERDAFTAR</p>
          <table>
            <tr><td>Nomor</td><td>${surat.nomor}</td></tr>
            <tr><td>Ditandatangani</td><td>${surat.ditandatangani.join(", ")}</td></tr>
            <tr><td>Perihal</td><td>${surat.perihal}</td></tr>
            <tr><td>Ditujukan</td><td>${surat.ditujukan}</td></tr>
            <tr><td>Tanggal</td><td>${surat.tanggal}</td></tr>
          </table>
        `;
        Swal.fire({
          icon: 'success',
          title: 'Verifikasi Berhasil',
          text: `Nomor Surat "${surat.nomor}" valid.`,
          showConfirmButton: false,
          timer: 2000
        });
      } else {
        result.className = "error show";
        result.innerHTML = "❌ Nomor Surat TIDAK TERDAFTAR.";
        Swal.fire({
          icon: 'error',
          title: 'Gagal',
          text: 'Nomor Surat tidak terdaftar. Cek kembali!',
          showConfirmButton: false,
          timer: 2000
        });
      }
    });
  </script>
</body>
</html>