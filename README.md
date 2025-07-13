<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Verifikasi Nomor Surat</title>

  <!-- SweetAlert2 CDN -->
  <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>

  <style>
    :root {
      --primary-color: #0047AB;
      --secondary-color: #0066CC;
      --success-color: #28a745;
      --error-color: #dc3545;
      --bg-color: #f2f5fa;
      --border-radius: 10px;
      --transition: all 0.4s ease;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: var(--bg-color);
      margin: 0;
      padding: 0;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
    }

    .container {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 40px 20px;
    }

    .card {
      background: #fff;
      padding: 40px;
      border-radius: var(--border-radius);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
      max-width: 500px;
      width: 100%;
      text-align: center;
      transition: var(--transition);
    }

    h1 {
      margin-bottom: 10px;
      color: var(--primary-color);
    }

    .subtitle {
      margin-bottom: 30px;
      color: #555;
      font-size: 14px;
    }

    form {
      display: flex;
      flex-direction: column;
    }

    input {
      padding: 12px 15px;
      border: 1px solid #ccc;
      border-radius: var(--border-radius);
      margin-bottom: 20px;
      font-size: 16px;
      transition: var(--transition);
      box-shadow: inset 0 1px 3px rgba(0,0,0,0.1);
    }

    input:focus {
      border-color: var(--primary-color);
      outline: none;
      box-shadow: 0 0 5px rgba(0, 71, 171, 0.3);
    }

    button {
      padding: 12px 20px;
      background: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: var(--border-radius);
      cursor: pointer;
      font-size: 16px;
      transition: var(--transition);
      box-shadow: 0 4px 12px rgba(0, 71, 171, 0.3);
    }

    button:hover {
      background: var(--secondary-color);
      transform: translateY(-2px);
    }

    #hasilVerifikasi {
      margin-top: 20px;
      text-align: left;
      opacity: 0;
      transform: translateY(10px);
      transition: opacity 0.5s ease, transform 0.5s ease;
    }

    #hasilVerifikasi.show {
      opacity: 1;
      transform: translateY(0);
    }

    #hasilVerifikasi.success {
      color: var(--success-color);
    }

    #hasilVerifikasi.error {
      color: var(--error-color);
      font-weight: bold;
    }

    .info-table {
      border-collapse: collapse;
      width: 100%;
      margin-top: 10px;
    }

    .info-table td {
      padding: 6px 0;
    }

    .info-table td:first-child {
      font-weight: bold;
      width: 40%;
      color: #333;
    }

    footer {
      text-align: center;
      padding: 20px;
      font-size: 14px;
      color: #999;
    }

    @media (max-width: 500px) {
      .card {
        padding: 30px 20px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="card">
      <h1>Verifikasi Nomor Surat</h1>
      <p class="subtitle">Masukkan nomor surat Anda untuk memastikan keaslian.</p>
      <form id="verifikasiForm">
        <input type="text" id="nomorSurat" placeholder="Contoh: 001/2025" required/>
        <button type="submit">Verifikasi</button>
      </form>
      <div id="hasilVerifikasi"></div>
    </div>
  </div>
  <footer>
    &copy; 2025 Instansi Resmi. All rights reserved.
  </footer>

  <script>
    // Data surat (bisa dikembangkan)
    const suratData = [
      {
        nomor: "001/2025",
        ditandatangani: ["Budi Santoso, S.Pd", "Rina Wijaya, M.M"],
        perihal: "Undangan Rapat Koordinasi",
        ditujukan: "Kepala Sekolah SMA Negeri 1 Pangandaran",
        tanggal: "15 Januari 2025"
      },
      {
        nomor: "002/2025",
        ditandatangani: ["Agus Salim, M.Pd"],
        perihal: "Pemberitahuan Libur Sekolah",
        ditujukan: "Seluruh Orang Tua/Wali Murid",
        tanggal: "20 Februari 2025"
      }
    ];

    document.getElementById("verifikasiForm").addEventListener("submit", function(e) {
      e.preventDefault();

      const inputNomor = document.getElementById("nomorSurat").value.trim();
      const hasil = document.getElementById("hasilVerifikasi");
      const surat = suratData.find(item => item.nomor === inputNomor);

      if (surat) {
        hasil.className = "success show";
        hasil.innerHTML = `
          <p>✅ Nomor Surat TERDAFTAR.</p>
          <table class="info-table">
            <tr><td>Nomor Surat</td><td>${surat.nomor}</td></tr>
            <tr><td>Ditandatangani Oleh</td><td>${surat.ditandatangani.join(", ")}</td></tr>
            <tr><td>Perihal</td><td>${surat.perihal}</td></tr>
            <tr><td>Ditujukan Kepada</td><td>${surat.ditujukan}</td></tr>
            <tr><td>Tanggal Ditandatangani</td><td>${surat.tanggal}</td></tr>
          </table>
        `;

        Swal.fire({
          icon: 'success',
          title: 'Nomor Valid',
          text: 'Nomor surat terdaftar dan valid.',
          showConfirmButton: false,
          timer: 2000
        });

      } else {
        hasil.className = "error show";
        hasil.innerHTML = "❌ Nomor Surat TIDAK TERDAFTAR.";

        Swal.fire({
          icon: 'error',
          title: 'Nomor Tidak Ditemukan',
          text: 'Nomor surat tidak terdaftar. Cek kembali input Anda.',
          showConfirmButton: false,
          timer: 2000
        });
      }
    });
  </script>
</body>
</html>
